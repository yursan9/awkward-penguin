---
title: 'Gnome Builder: Sebuah IDE untuk pengembangan desktop Linux'
date: 2019-09-15T02:55:21.137Z
tags:
  - linux
  - application
  - gtk
  - gnome
---
Kali ini, saya ingin memperkenalkan sebuah aplikasi yang cukup sering saya pakai; yaitu, [Gnome Builder](https://wiki.gnome.org/Apps/Builder). Pertama dirilis pada Maret 2015, Builder langsung menjadi IDE yang saya suka untuk membuat aplikasi _desktop_ Linux yang berbasis [GTK](https://www.gtk.org/). GTK sendiri adalah pustaka _toolkit_ yang digunakan untuk membuat Gnome Builder dan aplikasi lainnya pada _desktop_ Linux.

## Fitur Builder

Builder memiliki fitur seperti IDE pada umumnya, yaitu:

* _Autocompletion_ untuk token dan fungsi
* Pencarian Global untuk deklarasi fungsi atau variabel
* Peta mini untuk melihat keseluruhan kode
* Terintegrasi dengan dokumentasi
* _Debugger_
* _Profiling_ untuk melihat penggunaan sistem saat aplikasi berjalan
* Pendesain UI

## Tampilan Awal Builder

![Tampilan awal Builder; terdapat daftar proyek dan juga daftar pilihan seperti; buat proyek baru, pilih proyek dari folder, dan lain-lain](/images/uploads/builder-greeter.png)

Pertama kali dibuka, Builder akan menampilkan tampilan awal untuk memilih proyek yang akan dikembangkan. Selain itu, di jendela awal ini kita juga bisa meng-_clone_ proyek aplikasi Gnome yang lain untuk berkontribusi atau belajar. Bila kalian memilih _Start New Project_, kalian akan ditampilkan jendela seperti di bawah ini:

![Tampilan membuat proyek aplikasi baru](/images/uploads/builder-new-project.png)

Kalian dapat membuat proyek aplikasi baru dan memberikan informasi tentang proyek tersebut. Kita juga dapat memilih cetakan untuk memudahkan dalam memulai. Beberapa jenis bahasa pemrograman bisa dipilih di sini, seperti:

* C
* Javascript
* Python
* Vala
* C++
* C#

Setelah itu, pilih lisensi untuk program yang dibuat. Jika kalian mengklik tombol Create Project, kalian secara otomatis akan dibuatkan proyek yang sudah siap untuk kalian utak-atik. Berkas yang ada pada proyek, akan otomatis sesuai dengan pilihan bahasa pemrograman yang kalian pilih.

## Tampilan Editor

![](/images/uploads/builder-main-view.png)

Di sisi kiri terdapat sidebar yang berisi tentang daftar berkas-berkas yang ada pada proyek. _Sidebar_ ini juga memiliki tampilan lain untuk melihat _TODO_ atau barisan _error_ pada proyek yang dapat diakses dengan 3 tombol yang berjejer di atasnya.

Di sisi bawah terdapat pusat informasi dan terminal. Setiap log pasti akan ditampilkan disini dan jika ingin mengakses terminal juga bisa langsung dari sini tanpa perlu membuka terminal emulator yang baru.

Di sisi atas adalah kumpulan tombol untuk mengubah pengaturan editor. Selain itu, ada juga tombol untuk menjalankan program dan mencari file secara global dalam proyek. Di pojok paling kiri, kita bisa mengakses tampilan pengaturan dan _profilling_ dengan mengklik tombol dan mengakses tampilan yang dilihat.

## Tampilan Editor GUI

Untuk membuat tampilan grafis pada program, kita dapat menggunakan XML dengan ekstensi \`.ui\` di Gnome Builder. Namun, kita juga bisa membuat tampilan secara grafis tanpa perlu mengetahui notasi XML yang digunakan.

![Di bagian kanan atas editor terdapat tombol View Design yang bisa digunakan untuk melihat hasil desain dari XML](/images/uploads/builder-ui-source.png)

Di bagian kanan atas editor terdapat tombol _View Design_ yang bisa digunakan untuk melihat hasil desain dari XML dan juga untuk mendesain tampilan secara grafik.

![](/images/uploads/builder-ui-design.png)

Jika menekan _View Design_, tampilan editor akan berubah sehinga lebih cocok untuk membuat tampilan untuk membuat GUI aplikasi. Di sisi kanan terdapat _sidebar_ yang berisi pengaturan sifat dari _widget_ yang sedang dipilih. Selain itu, di bawah ada deretan tombol untuk menambahkan _widget_ sesuai jenisnya; misal _Toplevels_, _Containers_, dan lain-lain.

\## Penutup

Sekian perkenalan program kali ini. Lain kali, mungkin akan saya buatkan seri tutorial untuk membuat aplikasi dengan Gnome Builder. Sampai jumpa di tulisan selanjutnya.
