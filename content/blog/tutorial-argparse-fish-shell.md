---
title: 'Tutorial Argparse: Fish Shell'
date: 2019-03-02T03:26:53.493Z
tags:
  - tutorial
  - fish
draft: true
---
Beberapa hari yang lalu saya butuh sebuah aplikasi sederhana untuk mengubah `tag` pada file audio. Karena belum pernah membuat aplikasi CLI menggunakan Fish, saya jadi tertantang untuk membuatnya. Awalnya saya berpikir untuk memanipulasi variabel `argv` dengan *loop* dan *switch*, namun saya menemukan cara yang mudah untuk mengelola parameter dan *flag* untuk aplikasi CLI. Yaitu, dengan `argparse`.

## Argparse

> TLDR: Jika hanya ingin melihat *scripts* yang saya buat, silahkan buka [link ini](https://gist.github.com/yursan9/f96d48d9e4141c8b803fccb16964ed11).

Untuk melihat penggunaan `argparse` secara lengkap, bisa membaca halaman manual untuk `argparse`. `argparse` ini bukan sesuatu yang aneh. Beberapa bahasa pemrograman atau *scripting* lain juga memberikan kemampuan `argparse` (*Argumen Parsing*) dengan nama yang berbeda.

Biasanya orang menggunakan `argparse` seperti di bawah ini:

```
argparse --name "spam" "n/number=" "h/help" -- $argv
or exit
```

*Flag* `name` digunakan untuk menunjukan nama perintah yang akan dimasukkan saat terjadi error. Kalau tidak ada akan menggunakan kata `argparse` sebagai nama. Maksud dari `n/number=` adalah nantinya perintah dapat menerima *flag* `-n` dan `--number` dan maksud dari `h/help` juga artinya sama yaitu dapat menerima `-h` dan `--help`. Bedanya *flag* `-n` atau `--number` butuh sebuah
parameter.

Jika `argparse` berhasil menemukan *flag*, diakan membuat sebuah variabel untuk menyimpan nilai paramaeter. Nama dari variabel tersebut biasanya adalah `_fish_X`, di mana `X` itu nama *flag*.

```
#!/usr/bin/fish

argparse --name "hello" "h/help" -- $argv
or exit

if set -q _fish_h; or set -q _fish_help
    echo "Cara Menggunakan Perintah ini adalah: hello [option]"
    exit
end

echo "Hello World!"
```
