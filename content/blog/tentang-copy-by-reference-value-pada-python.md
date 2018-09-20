---
title: Tentang Copy By Reference/Value pada Python
date: 2018-09-20T11:49:21.929Z
tags:
  - python
draft: true
---
Jika memanipulasi nilai *mutable* pada Python, pertama kali saya melakukannya saya tersandung dengan konsep *Copy by Reference*. Di kampus saya tidak ada yang berpikir untuk memberitahu konsep ini di bagian konsep pemrograman pada awal saya masuk kuliah. Setelah ditelesuri, konsep ini ternyata ada pada bahasa pemrograman lain dan sering digunakan.

Setiap nilai yang disimpan pada variabel di Python itu menunjuk ke *pointer* tempat di mana nilai itu disimpan pada memori. Jika ada sebuah ekspresi seperti di bawah ini:

```
nama = 'Yurizal Susanto'
```

Variabel `nama` menyimpan *pointer* yang menunjuk nilai `'Yurizal Susanto'` di memori.

Untuk nilai bertipe data *immutable* seperti *integer*, *float*, *string*, atau *boolean*; saat kita menyalin nilai sebuah 
