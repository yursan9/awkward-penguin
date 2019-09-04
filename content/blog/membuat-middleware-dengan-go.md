---
title: Membuat Middleware dengan Go
date: 2019-09-04T03:58:41.370Z
tags:
  - go
  - middleware
  - tutorial
---
Pernah mendengar kata *middleware* saat menggunakan bahasa pemrograman Go? Biasanya konteks dari kata tersebut adalah saat membuat sesuatu yang berhubungan dengan server web.

Biasanya orang akan mengatakan untuk membuat *middleware* otentikasi, atau terkadang juga *logging*. Sebenarnya apa sih *middleware*?

## Definisi

*Middleware* biasanya adalah fungsi yang menerima argumen berupa fungsi dan mengeluarkan fungsi yang bisa digunakan sebagai pengganti fungsi yang menjadi argumen sebelumnya. Jadi, *middleware* bisa didefinisikan sebagai fungsi yang membungkus pemanggilan fungsi lain.

## Penjelasan

Kalau pernah menggunakan bahasa pemrograman Python, pola *middleware* ini bisa juga disebut sebagai pola *decorator*. Kenapa *middleware* bisa dibuat? Alasan utamanya adalah karena bahasa pemrograman yang mendukung pola ini menjadikan fungsi sebagai warga kelas satu. Artinya dalam konteks pemrograman, fungsi bisa digunakan sebagai nilai masukan dan keluaran.

```
package main

import (
	"fmt"
)

type MathFunc func(float64, float64) float64

func add(x, y float64) float64 {
	return x + y
}

func op(f MathFunc, x, y float64) float64 {
	return f(x, y)
}

func main() {
	fmt.Println(op(add, 5, 6))
}
```

Dalam program di atas ([playground](https://play.golang.org/p/IWcQas-qgmC)), fungsi `add` digunakan sebagai argumen untuk fungsi `op`. Kenapa go bisa menerima dan memanggil `add` di dalam fungsi `op`? Itu karena pola fungsi `add` sama dengan tipe `MathFunc` yang merupakan tipe dari variabel `f`.


## Contoh *Middleware*

Dalam go, ada sebuah tipe *interface* bernama `Handler`, dari paket `http`, yang memiliki pola seperti di bawah ini:

```
type Handler interface {
        ServeHTTP(ResponseWriter, *Request)
}
```

Tipe `Handler` adalah tipe yang diimplementasikan oleh fungsi yang melayani *endpoint*. Misal ada sebuah program seperti di bawah ini:

```
package main

import (
	"fmt"
	"html"
	"log"
	"net/http"
)

func indexHandler(w http.ResponseWriter, r *http.Request) {
	fmt.Fprintf(w, "Hello, World!")
}

func main() {
	h := http.HandlerFunc(indexHandler)
	http.Handle("/", h)
	log.Fatal(http.ListenAndServe(":8080", nil))
}
```

Program di atas akan membuat server web dan menampilkan kata "Hello, World!" jika dibuka pada browser; dengan url `localhost:8080`. Fungsi `indexHandler` sekarang memiliki tipe `http.Handler` karena sudah menjadi argumen dari panggilan `http.HandlerFunc`. Fungsi `http.HandlerFunc` merubah fungsi biasa menjadi sesuatu yang mengimplementasikan `http.Handler`.

> Lihat dokumentasi tentang [`http.HandlerFunc`](https://golang.org/pkg/net/http/#HandlerFunc) di situs web go.

Seperti yang sudah didefinisikan, *middleware* membungkus panggilan dari fungsi yang diterimanya. Misal, sebelum fungsi `indexHandler` dipanggil, kita ingin melakukan *logging* agar kita tahu fungsi `indexHandler` benar-benar dipanggil.

Jadi kita buat *middleware* yang berfungsi mencetak kata saat sebelum dan sesudah pemanggilan `indexHandler`.

```
func withLogging(next http.Handler) http.Handler {
	return html.HandlerFunc(func(w http.ResponseWriter, r *http.Request) {
		log.Println("Handler dipanggil")
		next.ServeHTTP(w, r)
		log.Println("Handler selesai")
	})
}
```

Fungsi `withLogging` adalah fungsi yang menerima argumen bertipe `http.Handler` dan mengeluarkan nilai `http.Handler`. Sehingga hasil dari fungsi ini bisa digunakan sebagai pengganti dari fungsi yang dijadikan sebagai masukan.

Lalu ubah penggunaan variabel `h`, yang merupakan fungsi `indexHandler`, menjadi seperti di bawah ini:

```
http.Handle("/", withLogging(h))
```

## Contoh *Middleware* Otentikasi

Di bawah ini adalah contoh *middleware* untuk otentikasi sederhana menggunakan *username* dan *password* yang diberikan melalui *header* Authorization:

```
func WithAuth(next http.Handler) http.Handler {
	return http.HandlerFunc(func(w http.ResponseWriter, r *http.Request) {
		username, password, ok := r.BasicAuth()
		if !ok {
			http.Error(w, "No API key provided", http.StatusUnauthorized)
			return
		}

		// Cek pengguna pada database
		ok := IsValid(username)
		if !ok {
			http.Error(w, "Invalid user", http.StatusForbidden)
			return
		}

		// Cek kata sandi pada database
		ok = IsPassValid(username, password)
		if !ok {
			http.Error(w, "Invalid password", http.StatusForbidden)
			return
		}

		next.ServeHTTP(w, r)
	})
}
```

## Penutup

Terima kasih sudah membaca sampai sejauh ini, jika ada pertanyaan atau ada sesuatu yang kurang dimengerti, bisa langsung kirim surel!
