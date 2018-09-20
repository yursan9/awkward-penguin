---
title: Tentang Copy By Reference/Value pada Python
date: 2018-09-20T11:49:21.929Z
tags:
  - python
draft: true
---
Jika memanipulasi nilai *mutable* pada Python, pertama kali saya melakukannya saya tersandung dengan konsep *Copy by Reference*. Di kampus saya tidak ada yang berpikir untuk memberitahu konsep ini di bagian konsep pemrograman pada awal saya masuk kuliah. Setelah ditelesuri, konsep ini ternyata ada pada bahasa pemrograman lain dan sering digunakan.

## *Copy by Value*

Setiap nilai yang disimpan pada variabel di Python itu menunjuk ke *pointer* tempat di mana nilai itu disimpan pada memori. Jika ada sebuah ekspresi seperti di bawah ini:

```python
nama = 'Monkey D. Luffy'
```

Variabel `nama` menyimpan *pointer* yang menunjuk nilai `'Monkey D. Luffy'` di memori.

Untuk nilai bertipe data *immutable* (tidak dapat diubah isinya) seperti *integer*, *float*, *string*, atau *boolean*; saat kita menyalin nilai sebuah variabel, Python akan melakukan *deep copy*, menduplikasi nilai dalam memori dan menggunakan nilai baru tersebut saat menyalin.

```python
nama = 'Monkey D. Luffy'
id = nama
```

## Nilai *Mutable*

Untuk nilai dengan tipe data *mutable* (dapat diubah isinya), Python melakukan sesuatu yang berbeda dari nilai bertipe *immutable* saat melakukan penyalinan. Python sengaja melakukan *shallow copy* atau *copy by reference* untuk meningkatkan performa.

```python
angka = [1, 2, 3, 4]
nomor = angka
nomor.append(5)
print(angka)
print(nomor)
```

Sehingga jika kita memanipulasi nilai variabel dengan salah satu nama variabel, keduanya akan sama-sama diperbarui karena menunjuk hal yang sama.

## Paksa *Copy by Value*

Kita dapat memaksa Python melakukan *copy by value* saat menyalin nilai variabel. Sehingga jika kita misalnya ingin mengurutkan *list*, tetapi kita juga ingin bisa menyimpan *list* yang tanpa diurutkan nilainya, kita tidak perlu lagi kebingungan.

```python
angka = [1, 2, 3, 4]
nomor = angka[:]
# atau
#nomor = angka.copy()
nomor.append(5)
print(angka)
print(nomor)
```
## Penutup

Saya senang sekali bila ada yang terbantu dengan tulisan di atas. Pertama saya belajar bahasa pemrograman Python, hal di atas terasa sangat membingungkan. Apalagi saya juga tidak mengerti konsep *pointer* pada bahasa pemrograman seperti C pada awalnya.

Sekian tulisan ini, jika ada yang ditanyakan dapat menghubungi melalui alamat surel yang ada kumpulan tombol di bagian *footer* halaman ini.

Te visurum!
