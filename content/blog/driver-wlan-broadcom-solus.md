---
title: 'Driver WLAN Broadcom: Solus'
date: 2019-02-12T04:12:46.463Z
tags:
  - tutorial
  - solus
  - linux
draft: false
---
Perkembangan pesat yang dialami dalam masalah *driver* perangkat keras pada Linux, tidak mengurangi ketergantungan kita pada vendor perangkat keras. Meskipun banyak perangkat yang hanya perlu dipasang lalu digunakan...beberapa masih perlu *driver* pihak ketiga yang bersifat bukan sumber terbuka. Biasanya sih ini merk, Nvidia dan Broadcom.

Kali ini sedikit tutorial pendek tentang pemasangan *driver* WLAN dari Broadcom pada Solus. Jika sama-sama tidak beruntung memiliki WLAN dengan merk Broadcom, silahkan ikuti. Untuk memastikan gunakan perintah `inxi` untuk melihat perangkat jaringan yang ada pada laptop masing-masing.

```
$ inxi -n
Network:
  Device-1: Realtek RTL810xE PCI Express Fast Ethernet driver: r8169 
  IF: enp1s0 state: down mac: <redacted> 
  Device-2: Broadcom and subsidiaries BCM43142 802.11b/g/n driver: wl 
  IF: wlp2s0 state: dormant mac: 38:b1:db:da:da:3b 
  IF-ID-1: enp0s20u1 state: unknown speed: N/A duplex: N/A 
  mac: <redacted>
```

## Tutorial

Pastikan kernel Linux sudah paling mutakhir. Karena *driver* pada Solus tidak mendukung DKMS. Jadi antara *driver* dan kernel harus memiliki seri yang sama.

```
sudo eopkg up -y
```

Setelah itu, pasang *driver* dengan nama `broadcom-sta` atau `broadcom-sta-current`. Jika menggunakan kernel versi stabil, gunakan `broadcom-sta`. Selain itu gunakan yang `broadcom-sta-current`.

```
sudo eopkg it broadcom-sta-current
```

Seharusnya WLAN sudah dapat menerima pancaran *wi-fi*. Namun jika belum, kita bisa memuat *driver* secara manual.

```
sudo depmod -a
sudo modprobe wl
```

Perintah `depmod` digunakan untuk memuat *driver*, lalu dengan perintah `modprobe` kita dapat mengaktifkan *driver*.

## Penutup

Saya sengaja menulis ini, karena terkadang saya juga lupa langkah untuk memasang *driver* WLAN di laptop. Semoga ada yang terbantu.
