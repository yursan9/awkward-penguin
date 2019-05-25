---
title: Trik Mengingat Kata Sandi Git di Linux
date: 2019-05-25T04:58:29.270Z
tags:
  - git
  - secret
  - linux
draft: false
---
Pernahkah kalian setiap saat ingin melakukan \`git push\` dan kalian merasa muak memasukkan kata sandi setiap saat? Tutorial ini akan memberikan solusi mudah untuk mengurangi waktu yang kita butuhkan dalam memasuki kata sandi. 

Tutorial ini berguna untuk semua distro Linux yang memiliki pustaka [libsecret](https://wiki.gnome.org/Projects/Libsecret). (Hampir semua Linux distro menggunakan `libsecret`)

## Tutorial

Jalankan program di bawah ini pada terminal:

```
git config --global credential.helper libsecret
```

Setelah dijalankan, `git` tidak akan pernah meminta kata sandi untuk kedua kalinya.

## Penutup

Tulisan ini sangat pendek, saya bahkan tidak ingin membuatnya tadi. Tapi semoga ada yang terbantu!
