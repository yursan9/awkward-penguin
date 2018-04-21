+++
title = "Regular Expression: Menangkap *man dalam Kalimat"
date = "2017-07-23T20:07:55+07:00"
tags = [
  "python",
  "tutorial",
  "regex"
]
+++

Memasuki masa tenang libur kuliah...blog ini, mungkin, akan banyak mendapatkan tulisan baru. Salah satu materi kuliah paling menarik di semester yang lalu adalah mata kuliah Teori Bahasa dan Otomata. Jika tahu lebih banyak tentang saya, mungkin aneh jika saya memilih mata kuliah teori tis sebagai mata kuliah favorit. Tapi, kenyataannya memang mata kuliah ini sangat menarik.

Teori Bahasa dan Otomata (TBO) membahas tentang membangun kalimat dengan peraturan yang sudah ada. Salah satu materinya, adalah membahas tentang *Regular Expression*. Namun sayang, di saat kuliah materinya tidak sampai dengan membahas *regular expression* atau biasa disebut **Regex**.

![Focus](https://source.unsplash.com/ywqa9IZB-dU/720x405)

Hari ini, saya akan bahas cara menggunakan *regex* secara sederhana dalam bahasa pemrograman *Python*. Ini bisa dilakukan di sistem operasi manapun yang sudah terpasang *interpreter* Python. Kita akan mulai dengan sedikit salinan kode sederhana untuk melihat bagaimana cara kerjanya.

```python
import re
pola = re.compile(r'batman')
```

Di baris pertama, kita mengimpor `re`, pustaka untuk melakukan *regex* di bahasa pemrograman Python. Lalu, kita harus mengkompilasi pola untuk *regex*, seperti yang ditunjukkan oleh baris kedua. Jika kita lihat kode diatas kita membuat pola yang dapat menyamakan kata `batman`.

Untuk mulai melakukan pencocokan kita bisa menggunakan *method* dibawah ini;

| *Method*   | Tujuan                                                                 |
|------------|------------------------------------------------------------------------|
| match()    | Menentukan apakah awal kalimat sama dengan pola                        |
| search()   | Pindai sebuah kalimat, dan cari lokasi dimana pola ini cocok           |
| findall()  | Temukan semua lokasi dimana pola cocok, dan menghasilkan sebuah *list* |
| finditer() | Sama seperti findall(), tapi menghasilkan sebuah [Iterator](https://docs.python.org/3/tutorial/classes.html#iterators)|

Jika *method* `match()` atau `search()` menemukan kecocokan dia akan mengembalikan sebuah objek **match**. Jika tidak menemukan apapun dia akan mengembalikan `None`.

```python
ketemu = pola.match("batman")
print(ketemu)
ketemu = pola.match("spiderman dan batman")
print(ketemu)                                # Hasilnya akan None
ketemu = pola.search("spiderman dan batman")
print(ketemu)                                # Tidak None
```

Objek **match** juga punya beberapa fungsi atau *method* sendiri, contohnya seperti dibawah ini;

```python
ketemu = pola.match("batman")
print(ketemu.group())   # Menampilkan kata dalam kalimat yang cocok dengan pola
print(ketemu.start())   # Menampilkan posisi awal kata yang cocok dengan pola
print(ketemu.end())     # Menampilkan posisi akhir kata yang cocok dengan pola
print(ketemu.span())    # Menampilkan tuple dengan 2 nilai posisi (awal, akhir)
```

Apa yang terjadi jika kita mengganti kata yang ingin dicocokan dari `batman` menjadi `Batman`? Tentu saja akan gagal. Karena pola awal kita hanya untuk mencocokan `batman` saja.

Untuk memperbaiki pola kita sebelumnya, ada sesuatu dalam *regex* yang namanya adalah kelas karakter. Kelas karakter adalah jika kita ingin menetukan sebuah karakter itu memiliki kumpulan alternatif kecocokan yang lain. Cara membuatnya hanyalah dengan memasukkan karakter di antara `[` dan `]`.

```python
pola = re.compile(r'[bB]atman')
ketemu = pola.match("Batman")
print(ketemu)
```

Pada kode diatas, kita mengganti pola kita sehingga kata `batman` atau `Batman` dapat dicocokan. Setelah melihat ini, mungkin kalian berpikir bagaimana jika kita ingin alternatifnya tidak hanya 2 karakter. Pasti melelahkan menuliskan `[abcde...zABCDE...Z]`, jika kita ingin alternatifnya semua huruf abjad. Seperti dalam bahasa tulisan sehari-hari, kita bisa menuliskan kelas karakter yang ribet sebelumnya menjadi seperti ini, `[a-zA-Z]`, dan Python akan tahu kalian ingin menyamakan huruf a sampai z atau huruf A sampai Z.

![Don't give up](https://source.unsplash.com/feeredToXK4/720x405)

Sebelum berakhir tutorial sederhana ini, ada satu hal lagi yang harus dibicarakan. Jika yang *regex* bisa lakukan hanyalah mencocokan kata yang berbeda-beda, tentu *regex* ini sangat tidak terlalu berguna untuk dituliskan tutorial seperti ini. Kemampuan *regex* yang lain adalah mencocokan sesuatu secara berulang sebanyak yang dibutuhkan.

Untuk melakukan pengulang dalam *regex* kita hanya perlu menambahkan `*` atau `+` di posisi setelah karakter atau kelas karakter yang ingin diulang. Karakter `*` akan melakukan pengulangang nol atau tak hingga dan karakter `+` akan melakukan pengulang minimal satu atau tak hingga. Misal kita punya pola `ca*t`, pola tersebut akan menerima kalimat `ct` (tidak ada `a`), `cat` (ada 1 `a`), `caaat` (ada 3 `a`). Oh iya, kita juga dapat menggunakan karakter `?` untuk mencocokan nol atau satu karakter.

Selain itu kita juga bisa melakukan pengulangan dengan menentukan secara eksak berapa kali pengulangan itu terjadi. Caranya adalah menambahkan `{m,n}` dimana *m* dan *n* adalah sebuah angka bulat. Untuk contoh, pola `ah{2,4}` akan menerima kalimat `ahh`, `ahhh`, dan `ahhhh`. Tetapi tidak dengan `ah` atau `ahhhhh` yang mengulang huruf `h` satu dan lima kali.

Terima kasih sudah melihat tutorial ini, kirim surel atau cuitan di Twitter jika ingin mengobrol, bertanya, atau memberi masukkan. Sebagai bonus, ada pola untuk mencocokan nama *Superhero* yang berakhiran dengan *-man* atau *man*.

```python
import re
pola = re.compile(r'[a-zA-Z]+-?man')
ketemu = pola.findall("Saya sudah melihat film Antman dan Spider-man.")
```

*Sayōnara!*
