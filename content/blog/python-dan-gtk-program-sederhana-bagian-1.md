---
title: 'Python dan Gtk: Program Sederhana (Bagian 1)'
date: 2019-09-29T02:42:07.352Z
tags:
  - tutorial
  - python
  - gtk
---
Jika ingin membuat program komputer yang memiliki GUI (_Graphical User Interface_) pada Python, memerlukan pustaka khusus untuk menggambar GUI. Python sendiri menyiapkan pustaka Tkinter untuk membuat GUI sederhana, yang merupakan pembungkus pustaka bernama Tk.

Namun kali ini, kita akan membahas pustaka bernama [Gtk](https://www.gtk.org/). Gtk adalah pustaka untuk membuat GUI yang ditulis dengan bahasa C. Namun, Gtk memiliki banyak _bindings_ untuk bahasa pemrograman lain. Salah satunya adalah [PyGObject](https://pygobject.readthedocs.io/en/latest/index.html), _bindings_ Gtk untuk Python. Pada tulisan ini kita akan mengenal sedikit tentang struktur program Gtk di Python, dan juga konsep Gtk seperti _Callback_, _layout_, dan lain-lain.

> Tulisan ini tidak membahas cara instalasi Gtk di komputer anda, silahkan lihat [dokumentasi PyGObject](https://pygobject.readthedocs.io/en/latest/getting_started.html) untuk mengetahui cara menginstalasi Gtk di masing-masing sistem operasi yang anda gunakan.

## Program Sederhana

Saya akan menampilkan keseluruhan kode dan menjelaskannya satu per satu. Buat sebuah berkas dengan nama `greet.py` dan isi dengan program di bawah ini:

```python3
import gi
gi.require_version('Gtk', '3.0')

from gi.repository import Gtk


class Application(Gtk.Application):
    def __init__(self, **kwargs):
        super().__init__(application_id='com.example.myapp',
                         **kwargs)

    def do_activate(self):
        win = self.get_active_window()
        if not win:
            win = AppWindow(application=self)

        win.present()


class AppWindow(Gtk.ApplicationWindow):
    def __init__(self, **kwargs):
        super().__init__(**kwargs)
        box = Gtk.Box(spacing=8,
                      border_width=18,
                      orientation=Gtk.Orientation.VERTICAL)
        
        label = Gtk.Label(label='Hello!')
        box.add(label)

        button = Gtk.Button(label='Click Me')
        box.add(button)

        self.add(box)
        self.show_all()


if __name__ == '__main__':
    app = Application()
    app.run()
```

Kita mulai penjelasan dari impor modul:

```python3
import gi
gi.require_version('Gtk', '3.0')

from gi.repository import Gtk
```

Pertama, untuk mengimpor Gtk kita menggunakan modul bernama `gi`. Lalu, gunakan `gi.require_version()` untuk memastikan modul Gtk ada dan memiliki versi yang kita inginkan. Pada kode di atas, kita menginginkan pustaka Gtk versi `3.0`. Setelah itu baru kita impor Gtk dari modul `gi.repository`.

Pembuatan aplikasi Gtk dapat menggunakan kumpulan fungsi, namun menurut saya pembuatan dengan pendekatan objek lebih mudah karena biasanya fungsi untuk suatu _widget_ dapat dikumpulkan menjadi _method_ untuk _widget_ tersebut.

Kelas `Application` adalah anak dari [`Gtk.Application`](https://lazka.github.io/pgi-docs/Gtk-3.0/classes/Application.html#Gtk.Application) yang merupakan kelas yang memberikan kemudahan untuk memanajemen objek aplikasi dalam kode. `Gtk.Application` melakukan banyak fungsi aplikasi modern; misalnya instansiasi aplikasi, integrasi dengan OS, manajemen sesi, dan lain-lain; sehingga jika kita tidak menggunakannya kita akan melakukan banyak hal yang sudah diberikan oleh `Gtk.Application`.

```python3
class Application(Gtk.Application):
    def __init__(self, **kwargs):
        super().__init__(application_id='com.example.myapp',
                         **kwargs)
```

Pada konstruktor kita hanya menjalankan inisialisasi dari `Gtk.Application` dan memberikan parameter `application_id`. Setiap aplikasi Gtk memiliki sebuah `application_id` yang terbuat dari nama domain yang dibalik plus nama aplikasi.

```python3
class Application(Gtk.Application):
    ...
    def do_activate(self):
        win = self.get_active_window()
        if not win:
            win = AppWindow(application=self)

        win.present()
```

Metode `do_activate()` adalah sebuah _callback_ yang otomatis dipanggil saat aplikasi pertama kali dijalankan. Di dalam metode tersebut kita akan cek apakah ada jendela aplikasi sedang berjalan, jika tidak ada maka akan dibuat objek jendela aplikasi.

```python3
class AppWindow(Gtk.ApplicationWindow):
    def __init__(self, **kwargs):
        super().__init__(**kwargs)
        box = Gtk.Box(spacing=8,
                      border_width=18,
                      orientation=Gtk.Orientation.VERTICAL)
        
        label = Gtk.Label(label='Hello!')
        box.add(label)

        button = Gtk.Button(label='Click Me')
        box.add(button)

        self.add(box)
        self.show_all()
```

Kelas `AppWindow` adalah kelas yang membungkus semua tampilan objek aplikasi kita. `AppWindow` mewarisi sifat dari `Gtk.ApplicationWindow`.

Di awal metode konstruktor, seperti yang dilakukan pada kelas `Application`, kita memanggil konstruktor dari kelas yang diwarisi. Setelah itu, kita akan membuat para _widget_ yang akan ditampilkan pada jendela.

Dalam Gtk, untuk meletakan _widget_ perlu sebuah wadah. Wadah ini adalah sebuah _widget_ bertipe [`Gtk.Container`](https://lazka.github.io/pgi-docs/index.html#Gtk-3.0/classes/Container.html#Gtk.Container). [`Gtk.Box`](https://lazka.github.io/pgi-docs/Gtk-3.0/classes/Box.html#Gtk.Box) adalah salah satu tipe kontainer yang bisa digunakan. Kontainer `Gtk.Box` memiliki orientasi vertikal atau horizontal. Jika kita menambahkan sesuatu ke dalam `Gtk.Box` maka posisi _widget_ tersebut akan terletak di bawah atau di samping kiri dari _widget_ lain tergantung orientasinya.

[`Gtk.Label`](https://lazka.github.io/pgi-docs/index.html#Gtk-3.0/classes/Label.html#Gtk.Label) adalah _widget_ yang bertugas menampilkan tulisan. [`Gtk.Button`](https://lazka.github.io/pgi-docs/Gtk-3.0/classes/Button.html#Gtk.Button) adalah _widget_ yang menampilkan tombol yang bisa ditekan. Setiap pembuatan _widget_ kita dapat memberikan properti atau atribut yang ingin kita ganti seperti misalnya:

```python3
box = Gtk.Box(spacing=8,
              border_width=18,
              orientation=Gtk.Orientation.VERTICAL)
```

Lalu yang terakhir adalah baris perintah untuk menjalankan aplikasi:

```python3
if __name__ == '__main__':
    app = Application()
    app.run()
```

## Menjalankan Aplikasi

Gunakan perintah di bawah untuk menjalankan aplikasi:

```
$ python3 greet.py
```

Lalu akan tampil hasil seperti berikut:

![Tampilan Aplikasi](/images/uploads/greet-win.png)

Setelah aplkasi dapat ditampilkan, selanjutnya kita akan belajar membuat *callback* dan belajar tentang sinyal.

## Klik Tombol

Gtk menggunakan konsep sinyal untuk memberi tahu program akan kejadian yang terjadi. Misalnya saat kita mengklik tombol, atau saat jendela berubah posisi. Sinyal ini bisa ditangkap dan kita dapat memanggil fungsi saat sinyal terjadi (fungsi yang dipanggil itu disebut dengan *callback*).

Kita akan buat *callback* saat kita menekan tombol. *Callback* ini nantinya akan mengubah tulisan *Hello!* menjadi *Hello, Nama!*.

```python3
class AppWindow(Gtk.ApplicationWindow):
    def __init__(self, **kwargs):
        ...
        button = Gtk.Button(label='Click Me')
        button.connect('clicked', self.on_button_clicked)
        box.add(button)
        ...
```

Panggil metode `connect()` dari objek *widget*. Metode `connect()` menerima parameter nama sinyal yang akan ditangkap, serta fungsi yang dipanggil saat sinyal itu terjadi.

Buat metode `on_button_clicked` pada kelas `AppWindow`. Isi dengan perintah di bawah ini:

```python3
    def on_button_clicked(self, button):
        print('Tombol di klik')
```

Setiap *callback* menerima parameter paling sedikit adalah 1 yaitu, *widget* yang mengirim sinyal.

Jalankan aplikasi untuk mencoba, jika saat kalian menekan tombol muncul tulisan *Tombol di klik* di terminal atau CMD, berarti *callback* berhasil dibuat.

Selanjutnya untuk dapat mengubah tulisan *Hello!* menajadi *Hello, Nama!*, kita perlu mengubah pemanggilan metode `connect()` dan juga mengimpor modul `os` untuk mendapatkan *username*.

```
button.connect('clicked', self.on_button_clicked, label)
```

Tambahkan satu parameter lagi, yaitu label, karena kita ingin memanipulasi *widget* label yang kita buat.

```
def on_button_clicked(self, button, label):
    user = os.getlogin()
    label.set_label('Hello, {}!'.format(user.title()))
```

Ubah pola metode `on_button_clicked` dengan menambahkan satu parameter lagi untuk menerima label yang diberikan saat pemanggilan `connect()`. Lalu dapatkan *username* yang sedang dipakai dan masukkan ke dalam *widget* label.

Contoh kode akhir:

```
import os
import gi
gi.require_version('Gtk', '3.0')

from gi.repository import Gtk


class Application(Gtk.Application):
    def __init__(self, **kwargs):
        super().__init__(application_id='com.example.myapp',
                         **kwargs)

    def do_activate(self):
        win = self.get_active_window()
        if not win:
            win = AppWindow(application=self)

        win.present()


class AppWindow(Gtk.ApplicationWindow):
    def __init__(self, **kwargs):
        super().__init__(**kwargs)
        box = Gtk.Box(spacing=8,
                      border_width=18,
                      orientation=Gtk.Orientation.VERTICAL)
        
        label = Gtk.Label(label='Hello!')
        box.add(label)

        button = Gtk.Button(label='Click Me')
        button.connect('clicked', self.on_button_clicked, label)
        box.add(button)

        self.add(box)
        self.show_all()

    def on_button_clicked(self, button, label):
        user = os.getlogin()
        label.set_label('Hello, {}!'.format(user.title()))


if __name__ == '__main__':
    app = Application()
    app.run()
```

## Penutup

Silahkan jalankan program yang sudah dibuat. Setelah tulisan ini, saya akan membahas tentang membuat aplikasi sederhana lainnya dengan memanfaatkan [Glade](https://glade.gnome.org/), sebuah aplikasi untuk mendesain tampilan GUI. Jadi tunggu tulisan selanjutnya!
