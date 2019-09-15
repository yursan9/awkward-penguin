---
title: Menulis Tes Unit pada Go
date: 2019-09-14T08:02:28.582Z
tags:
  - test
  - go
  - tutorial
---
*Unit Test* atau tes unit adalah sebuah rangkaian tes yang ditulis untuk menguji suatu unit terkecil dalam program (biasanya fungsi). Guna dari tes unit sendiri adalah memastikan bahwa sebuah unit berjalan sebagai mana mestinya. Selain itu, tes unit juga digunakan sebagai tolak ukur dalam proses *refactoring*. Meskipun mekanisme sebuah unit diganti, jika itu masih dapat melewati tes, unit tersebut tidak akan merubah integrasi dengan fungsi atau bagian program lain.

Dalam *Test Driven Development* (TDD), tes unit ditulis di awal penulisan program, setelah itu baru ditulis fungsi yang dapat melewati tes tersebut. Jika ingin menambah fungsionalitas pada fungsi, kita harus merubah tesnya terlebih dahulu.

## Tes Unit Sederhana

Sebuah tes unit biasanya disimpan pada berkasnya sendiri dalam bahasa pemrograman Go. Jika ada berkas bernama `math.go`, tes unit akan disimpan pada berkas `math_test.go`.

Buat sebuah berkas `util.go` dengan isi di bawah ini:

```
package main

func Spam(w string, n int) string {
	r := ""
	for i := 0; i < n; i++ {
		r += w
	}
	
	return r
}
```

Jalankan tes dengan perintah di bawah (karena kita belum buat tes unitnya, perintah akan gagal):
```
$ go test
?   	~/Documents/go-test	[no test files]
```

Sekarang kita buat tes unitnya, buat sebuah berkas dengan nama `util_test.go` dengan isi di bawah ini:

```
package main

import (
	"testing"
)

func TestSpam(t *testing.T) {
	w := "Spam"
	n := 3
	expected := "SpamSpamSpam"
	
	r := Spam(w, n)
	if r != expected {
		t.Errorf("Ingin %s dapat %s", expected, r)
	}
}
```

Tes unit dalam go adalah sebuah fungsi yang memiliki pola `TestXXX(t *testing.T)`, `XXX` adalah nama fungsi yang akan diuji. Biasanya dalam penulisan tes, saya membuat variabel yang akan menampung nilai masukan dan nilai yang ingin dikeluarkan. Jika nilai keluaran fungsi dan yang diinginkan tidak sama, panggil `t.Errorf()` untuk menandakan bahwa fungsi tidak lulus tes unit.

## Tes dengan Tabel Data

Terkadang sebuah fungsi memiliki banyak kemungkinan nilai keluaran; jika kita harus menulis tes unit seperti di atas, kita menghabiskan banyak waktu menulis ulang barisan kode. Karena itu biasanya digunakan tabel data untuk setiap kemungkinan masukan dan keluaran.

Tabel data biasanya saya buat dengan memanfaatkan *annonymous struct*. Ubah berkas `util_test.go` yang sebelumnya kita tulis menjadi seperti di bawah ini:

```
func TestSpam(t *testing.T) {
        testCase := []struct {
                w        string
                n        int
                expected string
        }{
                {"Spam", 3, "SpamSpamSpam"},
                {"", 2, ""},
                {"Halo Dunia", 1, "Halo Dunia"},
        }

        for _, v := range testCase {
                r := Spam(v.w, v.n)
                if r != v.expected {
                        t.Errorf("Ingin %s dapat %s", v.expected, r)
                }
        }
}
```

Dengan memanfaatkan *slice* yang berisi sebuah *struct*, kita bisa menulis setiap kasus pengujian. Menjalankan tes jadi lebih mudah dengan hanya perlu me-*loop* bagian kasus pengujiannya saja.

## Penutup

Tulisan di atas adalah pengenalan untuk menulis *unit test*. Beruntungnya go memiliki framework tes yang cukup baik menurut saya. Namun, masih banyak hal yang bisa ditulis tentang *testing*; misalnya *mocking* objek, tes HTTP server, *coverage*, dan lain-lain. Jadi tunggu tulisan selanjutnya dari saya!
