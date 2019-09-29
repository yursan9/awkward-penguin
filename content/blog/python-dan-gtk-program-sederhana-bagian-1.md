---
title: 'Python dan Gtk: Program Sederhana (Bagian 1)'
date: 2019-09-29T02:42:07.352Z
tags:
  - tutorial
  - python
  - gtk
---
Jika ingin membuat program komputer yang memiliki GUI (*Graphical User Interface*) pada Python, memerlukan pustaka khusus untuk menggambar GUI. Python sendiri menyiapkan pustaka Tkinter untuk membuat GUI sederhana, yang merupakan pembungkus pustaka bernama Tk.

Namun kali ini, kita akan membahas pustaka bernama [Gtk](https://www.gtk.org/). Gtk adalah pustaka untuk membuat GUI yang ditulis dengan bahasa C. Namun, Gtk memiliki banyak *bindings* untuk bahasa pemrograman lain. Salah satunya adalah [PyGObject](https://pygobject.readthedocs.io/en/latest/index.html), *bindings* Gtk untuk Python. Pada tulisan ini kita akan mengenal sedikit tentang struktur program Gtk di Python, dan juga konsep Gtk seperti *Callback*, *layout*, dan lain-lain.

> Tulisan ini tidak membahas cara instalasi Gtk di komputer anda, silahkan lihat [dokumentasi PyGObject](https://pygobject.readthedocs.io/en/latest/getting_started.html) untuk mengetahui cara menginstalasi Gtk di masing-masing sistem operasi yang anda gunakan.

## Program Sederhana
Saya akan menampilkan keseluruhan kode dan menjelaskannya satu per satu.

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

Pembuatan aplikasi Gtk dapat menggunakan kumpulan fungsi, namun menurut saya pembuatan dengan pendekatan objek lebih mudah karena biasanya fungsi untuk suatu *widget* dapat dikumpulkan menjadi *method* untuk *widget* tersebut.

Kelas `Application` adalah anak dari [`Gtk.Application`](https://lazka.github.io/pgi-docs/Gtk-3.0/classes/Application.html#Gtk.Application) yang merupakan kelas yang memberikan kemudahan untuk memanajemen objek aplikasi dalam kode. `Gtk.Application` melakukan banyak fungsi aplikasi modern; misalnya instansiasi aplikasi, integrasi dengan OS, manajemen sesi, dan lain-lain; sehingga jika kita tidak menggunakannya kita akan melakukan banyak hal yang sudah diberikan oleh `Gtk.Application`.

```
class Application(Gtk.Application):
    def __init__(self, **kwargs):
        super().__init__(application_id='com.example.myapp',
                         **kwargs)
```

Pada konstruktor kita hanya menjalankan inisialisasi dari `Gtk.Application` dan memberikan parameter `application_id`. Setiap aplikasi Gtk memiliki sebuah `application_id` yang terbuat dari nama domain yang dibalik plus nama aplikasi.

```

class Application(Gtk.Application):
    ...
    def do_activate(self):
        win = self.get_active_window()
        if not win:
            win = AppWindow(application=self)

        win.present()
```

Metode `do_activate()` adalah sebuah 
