---
title: Konfigurasi Joystick Ipega PG-9025 di Linux
date: 2017-09-19T09:21:21+07:00
tags:
  - gaming
  - tutorial
  - linux
  - udev
---

*Joystick* adalah aksesoris penting bagi mereka yang senang bermain permainan video (*video game*). Berkembang pesatnya dukungan permainan video di Linux, membuat banyak orang mulai bermain *game* menggunakan Linux. Namun, biasanya dukungan perangkat *joystick* terbatas di Linux. Seperti halnya *joystick* Ipega PG-9025 yang baru saya beli.

![Penampakan Joystick Ipega PG-9025](https://images-na.ssl-images-amazon.com/images/I/61qcHX94RjL._SL1200_.jpg)

Secara teori, seharusnya *joystick* Ipega ini bekerja dengan segala perangkat yang memiliki dukungan *bluetooth*. Ipega sendiri mengiklankan *joystick* ini untuk Android, Iphone, dan PC (*Personal Computer*). Tapi...mereka tidak menyadari bahwa PC bukan berarti komputer dengan sistem operasi Windows. Sehingga jika digunakan dengan *notebook* saya, semua tombolnya jadi kacau. Jadi di sinilah saya, mencoba mengakali hal ini di sistem operasi berbasis Linux yang saya gunakan.

> CATATAN: Jika anda menggunakan *joystick* standar seperti XBOX Controller, DualShock, atau Steam Controller mungkin pengalaman anda akan lurus dan tenang. Karena dukungan untuk *joystick* yang disebutkan tadi itu sangat baik.

Sejarah manajemen *joystick* di Linux itu penuh pertikaian di pertengahannya. Kini standar yang digunakan cuma satu, yaitu **evdev**. Pengaturan evdev sendiri tidak terlalu sulit. Untuk mengaturnya kita hanya perlu mengatur *rules* dari *udev*.

Pertama, pasangkan Ipega PG-9025 dengan komputer Linux anda. Nyalakan Ipega pada mode *joystick* dengan menekan tombol `HOME`+`X`, seperti pada buku panduan. Lalu, di komputer anda pasangkan perangkat sesuai dengan tampilan masing-masing. Setelah terpasang, ikuti langkah di bawah secara seksama.

Pastikan direktori `/etc/udev/rules.d` ada di sistem berkas anda, jika tidak ada silahkan buat dengan perintah dibawah ini;
```
sudo mkdir /etc/udev/rules.d
```

Lalu, buat sebuah file baru di direktori yang sebelumnya, dengan nama `64-ipega.rules`. Ganti `$EDITOR` dengan aplikasi pengubah teks favorit anda.
```
sudo $EDITOR /etc/udev/rules.d/64-ipega.rules
```

Isi file tersebut dengan teks di bawah ini;
```
ACTION=="add", SUBSYSTEM=="input", ATTRS{name}=="NAMA JOYSTICK", ATTRS{uniq}=="NOMOR UNIK", SYMLINK+="ipega", MODE="0666"
```

> Ganti `NAMA JOYSTICK` dan `NOMOR UNIK` sesuai dengan attribut `name` dan `uniq`, hasil perintah `cat /proc/bus/input/devices`. Jika *joystick* tidak terpasang dengan komputer, di hasil perintah `cat` sebelumnya tidak akan ada *joystick* yang tertera.

Kemudian, pasang aplikasi `xboxdrv` dari masing-masing manajemen paket anda. Jika anda pakai sistem operasi Solus, gunakan perintah dibawah ini;
```
sudo eopkg install xboxdrv
```

Buat file konfigurasi di `$HOME/.config/xboxdrv/ipega.conf`, jika folder tidak ada silahkan buat terlebih dahulu. Isi dengan pengaturan dibawah ini;
```ini
#iPEGA PG-9025 Config 

[xboxdrv]
evdev-debug = false
evdev-grab = true
rumble = false
mimic-xpad = true

[evdev-absmap]
ABS_HAT0X = dpad_x
ABS_HAT0Y = dpad_y

ABS_X = X1
ABS_Y = Y1

ABS_Z  = X2
ABS_RZ = Y2

[axismap]
-Y1 = Y1
-Y2 = Y2

[evdev-keymap]
BTN_A=a
BTN_B=b
BTN_Y=y
BTN_X=x
BTN_TR=rb
BTN_TR2=rt
BTN_TL=lb
BTN_TL2=lt
BTN_THUMBR=tr
BTN_THUMBL=tl
BTN_START=start
BTN_SELECT=back
BTN_MODE = guide
```

Setelah semua file konfigurasi sudah dibuat, anda harus menjalankan program `xboxdrv`. Mungkin ada yang bertanya, "Apa sih xboxdrv? Kenapa harus pakai xboxdrv?" Pertama, di atas sudah disebutkan bahwa dukungan untuk *contoller* seperti milik Xbox itu sangat bagus di Linux. Jadi kita akan mensimulasikan *joystick* Ipega ini menjadi *joystick* Xbox. Sehingga lebih banyak *game* yang dapat dimainkan menggunakan *joystick* Ipega.

Jalankan `xboxdrv` di Terminal dengan perintah dibawah ini;
```
xboxdrv --evdev /dev/ipega --config $HOME/.config/xboxdrv/ipega.conf --silent
```

Selama `xboxdrv` berjalan di komputer anda, komputer anda akan mengenali *joystick* Ipega sebagai *joystick* Xbox. Untuk mematikan programnya, gunakan tombol `Ctrl`+`C` di Terminal.

Selamat! Anda menyelesaikan tutorial ini. Silahkan coba untuk bermain *game* di Steam atau emulator dengan *joystick* anda. Jika ada kebingungan atau ada masalah, kirim cuitan melalui Twitter atau surel.

