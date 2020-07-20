---
title: Memperbaiki Bluetooth Realtek RTL8723BE di Linux
date: 2020-07-16T12:21:44.017Z
tags:
  - tutorial
  - bluetooth
  - udev
---
Siapa yang pernah merasakan kepasrahan saat tidak bisa pakai Bluetooth di laptop saat menggunakan Linux? *Well*, saya baru saja merasakannya sebelum menulis blog ini. Ceritanya saya ingin menyandangkan *keyboard* bluetooth yang baru saya beli, tapi Gnome hanya bisa diklik tombol aktivasi bluetooth lalu otomatis mati lagi.

Ternyata kesalahan ada di *firmware* bluetooth yg digunakan laptop saya (Realtek memang punya dukungan payah untuk Linux). Isi blog ini terinspirasi dari [blog lain](https://patiladitya.gitlab.io/posts/2017-12-09-rtl8723be-fix/), namun dengan penanganan yang berbeda.

## Permasalahan

Perangkat bluetooth ini terkena sistem *auto-suspend* Linux, kernel linux biasanya akan meregulasi segala penggunaan daya di perangkat komputer dan kalau tidak digunakan dia akan mematikan perangkat tersebut. Karena dukungan *firmware/driver* yang jelek untuk beberapa perangkat, perangkat tidak bisa memberitahu linux bahwa dia sedang digunakan. Kita harus secara manual memberitahu Linux untuk tidak mematikan perangkat bluetooth secara otomatis.

## Mulai memperbaiki

Jalankan perintah `lsusb` di terminal:
```
$ lsusb
Bus 001 Device 002: ID 8087:8000 Intel Corp. 
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 003 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 002 Device 005: ID 0bda:b728 Realtek Semiconductor Corp. Bluetooth Radio 
Bus 002 Device 004: ID 5986:014f Acer, Inc Lenovo EasyCamera
Bus 002 Device 003: ID 0bda:0129 Realtek Semiconductor Corp. RTS5129 Card Reader Controller
Bus 002 Device 002: ID 046d:c52f Logitech, Inc. Unifying Receiver
Bus 002 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
```

Kita bisa lihat ID dari perangkat bluetooth kita—lihat yang memiliki tulisan bluetooth—perangkat bluetooth saya adalah `0bda:b728 Realtek Semiconductor Corp. Bluetooth Radio`.

Selanjutnya kita akan cari *file* yang merepresentasikan perangkat kita (ingat segala di linux adalah *file*).

Di dalam direktori `/sys/bus/usb/devices/` terdapat daftar perangkat yg terhubung dengan USB (internal/eksternal). Di bawah ini adalah contoh perangkat yang terhubung di laptop saya.
```
$ ls /sys/bus/usb/devices/
1-0:1.0@  2-0:1.0@  2-1:1.1@  2-6@      2-7@      3-0:1.0@  usb3@
1-1@      2-1@      2-4@      2-6:1.0@  2-7:1.0@  usb1@
1-1:1.0@  2-1:1.0@  2-4:1.0@  2-6:1.1@  2-7:1.1@  usb2@
```

Tampilannya memang berbeda dengan hasil perintah `lsusb`. Tapi kita bisa tahu perangkat yg kita mau dengan menggunakan perintah `cat`. Panggil `cat` satu persatu ke daftar perangkat sampai menemukan pasangan `idVendor` dan `idProduct` yang sesuai dengan hasil `lsusb`.
```
$ cat /sys/bus/usb/devices/2-7/idVendor 
0bda
$ cat /sys/bus/usb/devices/2-7/idProduct 
b728
```

Biasanya di setiap perangkat ada jalur `power/control`, yang isinya adalah mode pengatur daya yang digunakan oleh linux. Biasanya isi dari ini adalah `auto`, supaya linux dapat otomatis menghidupkan dan mematikan perangkat secara otomatis.
```
$ cat /sys/bus/usb/devices/usb2/2-7/power/control
auto
```

Mari kita ubah nilai `auto` ini menjadi `on`.
```
$ echo 'on' | sudo tee /sys/bus/usb/devices/usb2/2-7/power/control
```

Kalau sudah diganti, harusnya perangkat bluetooth kita sudah bisa digunakan. Sekarang hanya perlu memastikan perubahan kita disimpan selamanya.

## Solusi Permanen

Untuk membuat perubahan ini permanen, kita harus menambah *rules* baru untuk `udev`.

> Lihat juga [Konfigurasi Joystick Ipega](https://yursan.id/blog/konfigurasi-joystick-ipega-di-linux/) yang menggunakan `udev`

Buat sebuah *file* baru:
```
$ sudo $EDITOR /etc/udev/rules.d/usb-power.rules
```

Lalu masukkan isi kira-kira mirip seperti di bawah ini:
```
#Realtek Semiconductor Corp. Bluetooth Radio
ACTION=="add", SUBSYSTEM=="usb", ATTR{idVendor}=="0bda", ATTR{idProduct}=="b728", TEST=="power/control", ATTR{power/control}="on"
```

Pastikan `idVendor` dan `idProduct` sesuai dengan perangkat bluetooth terpasang dan format keluaran `lsusb`.

## Penutup

Harusnya setelah ini perangkat bluetooth akan mudah dinyalakan setiap kali dibutuhkan.

Sampai jumpa.
