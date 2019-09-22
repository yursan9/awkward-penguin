---
title: 'Threading dan Gtk: PyGObject'
date: 2019-09-22T12:48:32.720Z
tags:
  - tutorial
  - python
  - gtk
  - threading
---
Terkadang ada waktunya sebuah operasi memiliki waktu proses yang cukup lama. Operasi seperti ini harusnya tidak dijalankan di alur utama (*main thread*), karena dapat menahan alur eksekusi proses lain. Dalam pemrograman aplikasi GUI, alur utama biasanya bertugas mengatur proses masukan dan penggambaran tampilan, jika kita melakukan operasi yang lama di alur utama, tampilan GUI kita bisa *freeze* menunggu operasi tersebut.

Beberapa jenis operasi yang cukup lama adalah:

- Mencari sistem berkas
- Memuat sumber daya dari internet
- Menulis dan membaca berkas

## Penjelasan

Untuk membuat sebuah aplikasi dengan GUI, dibutuhkan pustaka yang digunakan untuk menggambarkan jendela dan *widget* ke layar. Gtk adalah salah satu *toolkit* yang banyak dipakai di Linux. Gtk dibuat dengan bahasa pemrograman C, namun menyediakan banyak *bindings* untuk bahasa pemrograman lain; diantaranya adalah Python.

Penggunaan Python dan Gtk harus melalui pustaka PyGObject yang dapat diunduh pada masing-masing sistem operasi. Kelemahan dari Python adalah adanya GIL, sebuah sistem mutex yang melindungi pengaksesan objek pada Python dari *thread* lain. Hal ini juga berlaku pada Gtk, karena Gtk tidak *thread-safe*, alias hanya dapat dijalankan pada satu alur saja.

> Lihat berkas [*Getting Started*](https://pygobject.readthedocs.io/en/latest/getting_started.html) dari PyGObject untuk proses instalasi.

Saat saya membuat aplikasi untuk melihat waktu shalat ([github](https://github.com/yursan9/arkan)), saya harus mengunduh berkas yang dihasilkan dari API yang saya gunakan. Setiap saya mengunduh, seluruh interaksi ke aplikasi menjadi tidak bisa dilakukan karena saya melakukan proses pengunduhan di alur utama. Sehingga tulisan ini akan membahas tentang penggunaan *thread* dan Gtk.
