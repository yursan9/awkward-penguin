---
title: 'Tutorial Argparse: Fish Shell'
date: 2019-05-06T03:26:53.493Z
tags:
  - tutorial
  - fish
draft: false
---
Beberapa hari yang lalu saya butuh sebuah aplikasi sederhana untuk mengubah `tag` pada file audio. Karena belum pernah membuat aplikasi CLI menggunakan Fish, saya jadi tertantang untuk membuatnya. Awalnya saya berpikir untuk memanipulasi variabel `argv` dengan _loop_ dan _switch_, namun saya menemukan cara yang mudah untuk mengelola parameter dan _flag_ untuk aplikasi CLI. Yaitu, dengan `argparse`.

## Argparse

> TLDR: Jika hanya ingin melihat _scripts_ yang saya buat, silahkan buka [link ini](https://gist.github.com/yursan9/f96d48d9e4141c8b803fccb16964ed11).

`argparse` ini bukan sesuatu yang aneh atau asing. Beberapa bahasa pemrograman atau _scripting_ lain juga memberikan kemampuan `argparse` (_Argument Parsing_) dengan nama yang berbeda. Terutama jika ingin membuat aplikasi CLI yang mengikuti standar.

Biasanya orang menggunakan `argparse` di fish seperti di bawah ini:

```
argparse --name "spam" "n/number=" "h/help" -- $argv
or exit
```

_Flag_ `name` digunakan untuk menunjukan nama perintah yang akan dimasukkan saat terjadi error. Kalau tidak ada akan menggunakan kata `argparse` sebagai nama. Maksud dari `n/number=` adalah nantinya perintah dapat menerima _flag_ `-n` dan `--number` dan maksud dari `h/help` juga artinya sama yaitu dapat menerima `-h` dan `--help`. Bedanya _flag_ `-n` atau `--number` butuh sebuah
parameter.

Jika `argparse` berhasil menemukan _flag_, dia akan membuat sebuah variabel untuk menyimpan nilai paramaeter. Nama dari variabel tersebut biasanya adalah `_fish_X`, di mana `X` itu nama _flag_.

```
#!/usr/bin/fish

argparse --name "halo" "h/help" -- $argv
or exit

# Cek apakah ada flag h/help. Jika ya, tampilkan manual dan keluar
if set -q _fish_h; or set -q _fish_help
    echo "Cara Menggunakan Perintah ini adalah: halo [option]"
    exit
end

echo "Halo Dunia!"
```

Contoh hasil dari perintah di atas jika disimpan dalam sebuah file bernama `halo` adalah:

```
$ ./halo
Halo Dunia!
$ ./hello --help
Cara Menggunakan Perintah ini adalah: halo [option]
```

Jika *flag* memiliki parameter, contohnya seperti di bawah ini:

```
#!/usr/bin/fish

argparse --name "halo" "n-name=" "h/help" -- $argv
or exit

# Cek apakah ada flag h/help. Jika ya, tampilkan manual dan keluar
if set -q _fish_h; or set -q _fish_help
    echo "Cara Menggunakan Perintah ini adalah: halo [option]"
    exit
end

if set -q _fish_n; or set -q _fish_name
    echo "Halo $_fish_name!"
else
    echo "Halo Dunia!"
end
```

Hasil dari perintah yang baru adalah:

```
$ ./halo
Halo Dunia!
$ ./halo --name=Steve
Halo Steve!
```

## Penutup

Ini adalah sebuah tutorial sederhana. Banyak opsi yang diberikan oleh fish dalam melakukan _argument parsing_, sehingga lebih baik membaca dokumentasinya saja. Untuk melihat penggunaan `argparse` secara lengkap, bisa membaca halaman manual untuk `argparse` di [situs resmi](https://fishshell.com/docs/current/commands.html#argparse) Fish Shell. 
