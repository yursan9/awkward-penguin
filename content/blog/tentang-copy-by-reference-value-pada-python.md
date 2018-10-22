---
title: Copy By Reference/Value pada Python
date: 2018-09-20T11:49:21.929Z
tags:
  - python
draft: false
---
Jika memanipulasi nilai _mutable_ pada Python, pertama kali saya melakukannya saya tersandung dengan konsep _Copy by Reference_. Di kampus saya tidak ada yang berpikir untuk memberitahu konsep ini di bagian konsep pemrograman pada awal saya masuk kuliah. Setelah ditelesuri, konsep ini ternyata ada pada bahasa pemrograman lain dan sering digunakan.

## _Copy by Value_

Setiap nilai yang disimpan pada variabel di Python itu menunjuk ke _pointer_ tempat di mana nilai itu disimpan pada memori. Jika ada sebuah ekspresi seperti di bawah ini:

```python
nama = 'Monkey D. Luffy'
```

Variabel `nama` menyimpan _pointer_ yang menunjuk nilai `'Monkey D. Luffy'` di memori.

Untuk nilai bertipe data _immutable_ (tidak dapat diubah isinya) seperti _integer_, _float_, _string_, atau _boolean_; saat kita menyalin nilai sebuah variabel, Python akan melakukan _deep copy_, menduplikasi nilai dalam memori dan menggunakan nilai baru tersebut saat menyalin.

```python
nama = 'Monkey D. Luffy'
id = nama
```

![null](/images/uploads/immutable_copy.png)

## Nilai _Mutable_

Untuk nilai dengan tipe data _mutable_ (dapat diubah isinya), Python melakukan sesuatu yang berbeda dari nilai bertipe _immutable_ saat melakukan penyalinan. Python sengaja melakukan _shallow copy_ atau _copy by reference_ untuk meningkatkan performa.

```python
angka = [1, 2, 3, 4]
nomor = angka
nomor.append(5)
print(angka)
print(nomor)
```

Sehingga jika kita memanipulasi nilai variabel dengan salah satu nama variabel, keduanya akan sama-sama diperbarui karena menunjuk hal yang sama.

![](/images/uploads/shallow_copy.png)

## Paksa _Copy by Value_

Kita dapat memaksa Python melakukan _copy by value_ saat menyalin nilai variabel. Sehingga jika kita misalnya ingin mengurutkan _list_, tetapi kita juga ingin bisa menyimpan _list_ yang tanpa diurutkan nilainya, kita tidak perlu lagi kebingungan.

```python
angka = [1, 2, 3, 4]
nomor = angka[:]
# atau
#nomor = angka.copy()
nomor.append(5)
print(angka)
print(nomor)
```

![](/images/uploads/deep_copy.png)

## Penutup

Saya senang sekali bila ada yang terbantu dengan tulisan di atas. Pertama saya belajar bahasa pemrograman Python, hal di atas terasa sangat membingungkan. Apalagi saya juga tidak mengerti konsep _pointer_ pada bahasa pemrograman seperti C pada awalnya.

Sekian tulisan ini, jika ada yang ditanyakan dapat menghubungi melalui alamat surel yang ada kumpulan tombol di bagian _footer_ halaman ini.

Te visurum!
