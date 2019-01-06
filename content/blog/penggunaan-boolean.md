---
title: Penggunaan Boolean
date: 2019-01-06T05:53:28.456Z
tags:
  - logika
  - boolean
  - tutorial
  - python
draft: false
---
Logika *boolean* adalah hal yang sering ditemukan saat pembuatan program. Jika berhubungan dengan `if` atau operator logika; kita akan menemui logika *boolean*. Sehingga konsep ini harus sudah dikuasai diawal pembelajaran pemrograman.

Tulisan ini akan membahas sedikit tentang *boolean* dengan menggunakan bahasa pemrograman Python 3. Meskipun begitu, konsepnya dapat diterapkan di berbagai macam bahasa pemrograman.

## Pendahuluan

Dalam bahasa pemrograman, *boolean* selain sebagai konsep, digunakan juga sebagai nama tipe data. Tipe data *boolean* biasanya berhubungan dengan kebenaran, *True* atau *False*. Di Python, tipe data *boolean* dapat memiliki nilai `True` atau `False`.

Tipe data *boolean* terkadang bisa digantikan dengan tipe data numerik untuk menyatakan kebenaran. Misalnya, *integer* `0` dan *float* `0.0` biasanya dianggap sebagai `False` dan nilai selain itu otomatis dianggap `True`.

Untuk di Python sendiri, tipe data lain seperti *string*, atau tipe data yang bisa menyimpan banyak nilai (*list*, *set*, dll) jika kosong, atau hasil dari `len(var) == 0` maka otomatis dianggap memiliki nilai *boolean* `False`.

## Percabangan

Percabangan biasanya terjadi akibat pengujian nilai kebenaran. Pengujian biasa digunakan dengan operator relasi.

```python3
if x % 2 == 0:
    print("X adalah Genap")
```

Namun, terkadang sering sekali orang menulis kode yang melakukan pengujian pada nilai *boolean* dengan operator relasi.

```python3
selesai = True

if selesai == True:
    print("Program sudah selesai")
```

Operator relasi seharusnya tidak perlu digunakan pada contoh di atas, karena nilai `selesai` sudah memiliki tipe *boolean*. Operator relasi sebaiknya digunakan untuk menghasilkan nilai *boolean* untuk sebuah ekspresi non-*boolean* (seperti di contoh pertama).

```python3
selesai = True

if selesai:
    print("Program sudah selesai")
```

## Logika *Boolean*

```python3
if x >= 0:
    if x <= 10:
        print("X di antara 0-10")
    else:
        print("X di luar 0-10")
else:
    print("X di luar 0-10")
```

Kode di atas dapat dengan mudah disederhanakan jika kita mengerti cara kerja operator logika. Pernyataan `if` bersarang dapat disederhanakan jika kita tau bahwa nilai `x` harus lebih besar sama dengan `0` dan lebih kecil sama dengan `10` dapat ditulis dalam satu baris.

```python3
if x >= 0 and x <= 10:
    print("X di antara 0-10")
else:
    print("X di luar 0-10")
```

Selain cara penggunaan operator logika, karakteristik operator logika adalah *short-circuit* (pemutusan hubungan). Terutama untuk operator `and` dan `or`.

```python3
if x % 3 == 0 and x % 2 == 0:
    print("X dapat dibagi habis 3 dan 2")

if x % 3 == 0 or x % 2 == 0:
    print("X dapat dibagi habis 3 atau 2")
```

Di contoh pernyataan `if` yang pertama, jika pernyataan relasi `x % 3 == 0` menghasilkan nilai salah, maka pernyataan dibelakang operator `and` tidak akan dijalankan, dan program akan keluar dari `if`. Di contoh yang kedua, jika pernyataan relasi pertama menghasilkan nilai benar, maka pernyataan relasi selanjutnya tidak akan dijalankan, dan program akan menjalankan instruksi pada blok `if`.

## Beralih Nilai *Boolean*

Pernahkah menulis kode seperti di bawah ini:

```python3
nyala = True

if nyala:
    nyala = False
else:
    nyala = True
```

Saya pernah menulis kode seperti di atas saat saya berkontribusi pada repositori github [Solus Project](https://getsol.us/home/). Lalu ada seorang kontributor senior yang memperbaiki kode tersebut. Dia mengatakan jika ingin menulis kode yang mengganti nilai *boolean* seperti dicontoh, lebih baik menggunakan operator logika `not`. Sehingga penyataan `if` di atas berubah menjadi pernyataan satu baris seperti di bawah ini:

```python3
nyala = not nyala
```

## Penutup

Ok, semoga tulisan di atas berguna. Sebenarnya tulisan ini didedikasikan untuk praktikan praktikum di kampus saya. Karena banyak sekali dari mereka yang tidak menggunakan logika *boolean* untuk menyederhanakan program mereka. Sehingga mereka sering menulis pernyataan `if` yang tidak perlu atau bahkan `if` yang bersarang sangat dalam.

Adios!
