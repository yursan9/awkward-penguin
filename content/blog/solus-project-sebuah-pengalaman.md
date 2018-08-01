---
title: 'Solus Project: Sebuah Pengalaman'
date: '2018-08-01'
tags:
  - solus
  - linux
draft: false
---
Tidak disangka sudah hampir 3 tahun lebih saya memulai memakai sistem operasi berbasis Linux. Dalam 3 tahun itu banyak pengalaman berharga, yang mungkin tidak saya dapatkan sampai sekarang; jika saya tidak menggunakan Linux. Salah satu pengalaman yang paling berharga adalah saat menggunakan distro, distribusi Linux, [Solus](https://solus-project.com/).

## Pengalaman Awal dengan Linux

Awal mula memakai distro Linux, saya menggunakan distro [Xubuntu](https://xubuntu.org/). Kebetulan waktu itu saya mulai memakai Linux bulan Agustus 2015. Banyak keluh kesah yang muncul selama penggunaan, namun semua saya coba singkirkan untuk memulai belajar menggunakan sistem operasi baru. Beruntung atau kurang beruntung, kalian bisa pilih, saat saya pasang Xubuntu di *netbook* 17 juta, yang saya dapatkan dari tempat saya kuliah, semua berjalan dengan baik. Saya punya jaringan internet, browser favorit saya (Firefox) sudah terpasang, dan saya juga punya kumpulan aplikasi kantor (LibreOffice). Hal tersebut membuat saya merasa Linux sama saja mudahnya dengan Windows. Jadi waktu itu saya tidak dapat pelajaran apapun.

Hei, bagaimana kalau pakai distro Debian? atau Ubuntu? (Ya, pada akhirnya saya tahu Xubuntu itu keluarga Ubuntu, saya di tahun 2015 tidak mengerti yang namanya kernel ataupun distro.)

![Do What Is Great](https://source.unsplash.com/5Xwaj9gaR0g/720x405)

## Bertemu Solus Project

Di akhir tahun 2015, saya menemukan sebuah berita tentang distro Linux yang memiliki waktu *booting* yang cepat; dan berita itu tentang Solus Project. Solus Project adalah nama organisasi yang membangun sistem operasi Solus, organisasi ini pertama kali dibangun oleh Ikey Doherty. Tidak lama setelah itu Solus Project melakukan pelepasan seri Solus 1.1, yang membuat saya akhirnya mencobanya.

Pertama memasang, hampir semua berjalan lancar. Klaim waktu *booting* yang cepat pun bukan berita bohong, waktu itu. Tapi saya tidak punya jaringan internet. Ini membuat saya gila, dan akhirnya waktu itu ada yang membantu dan mengatakan, “Coba tunjukkan hasil program `inxi -n`.” Lalu orang tersebut mengatakan bahwa saya punya chip *wireless* merk Broadcom yang terkenal sulit dengan Linux. Agak kecewa, tapi dia bilang coba pasang *driver* dengan aplikasi `docflicky`. Tetapi, bagaimanapun saya mencobanya, jaringan internet tetap tidak digenggamanan.

Pengalaman pertama memang tidak mulus, namun pada akhirnya saya bisa menggunakan internet dengan memuat *driver* Broadcom dengan perintah `modprobe`. Namun dari masalah itu dan yang lainnya, saya belajar *troubleshooting* sederhana untuk Linux.

## Kontribusi ke Solus Project

Setelah itu saya memulai memakai Solus untuk kegiatan sehari-hari. Namun, ada masalah perangkat lunak yang saya gunakan tidak ada di lumbung aplikasi Solus (ini sekitar akhir 2016). Seseorang di forum Solus mengatakan untuk coba memaketkannya sendiri. Akhirnya saya belajar memakai `git` untuk memulai memaketkan. Waktu itu Phabricator tidak digunakan untuk memanajemen paket, kita harus menggunakan `git format-patch` lalu hasilnya dikirim ke pengembang Solus.

Infrastruktur Solus Project berganti, Solus mulai menggunakan Phabricator dan lainnya. Saya mulai berpikir, untuk kontribusi ke Budgie Desktop. Saya bisa menggunakan bahasa pemrograman Python, apa yang bisa saya kontribusikan? Akhirnya saya buat *applet*, mirip *widget* Android, pertama saya untuk Budgie. Tapi *applet* tersebut tidak pernah saya publikasikan karena malu dengan kualitas kodenya. Pengalaman itu memberikan saya ilmu tentang Git, Python, distribusi kode dengan Meson, dan lain-lain.

Pengalaman kontribusi ke Solus Project memberikan banyak ilmu baru. Selain yang disebutkan di atas, saya juga belajar tentang lisensi perangkat lunak sumber bebas terbuka (FOSS); menggunakan IRC (ya, Internet Relay Chat, awalnya saya kira saya bermimpi); menggunakan Makefile atau yang sejenisnya seperti CMake, Meson, dan setuptools; dan paling penting adalah memperbaiki bahasa inggris saya yang cukup untuk membaca, tetapi payah saat menulis atau bercakap.

## Di Masa Depan

Saya berharap bisa terus berkontribusi ke Solus Project, bukan dengan materi (saya bahkan tidak punya penghasilan), tetapi dengan kode dan membantu anggota komunitas Solus yang lain (terutama dari Indonesia). Sebelum tulisan ini dipublikasikan, [kontribusi saya](https://github.com/solus-project/budgie-desktop/commit/e3f69e25a33df95bac09f00dc7e6e6a0c24014cd) baru diterima untuk memasukkan *applet* buatan saya ke dalam Budgie Desktop. Kontribusi seperti ini yang ingin bisa terus saya berikan.
