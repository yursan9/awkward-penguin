---
title: Kenapa membuat Résumé dengan LaTeX?
date: '2018-07-17'
tags:
  - latex
  - resume
draft: true
---
Memasuki akhir karir sebagai mahasiswa, saya mulai berpikir tentang membuat [résumé](https://en.wikipedia.org/wiki/R%C3%A9sum%C3%A9). Setelah mengubek internet tentang format résumé yang baik, kebanyakan menyarankan untuk membuat satu format tapi fleksibel.

Karena dasar itu saya berpikir untuk memanfaatkan [LaTeX](https://tug.org/texlive/). LaTeX (atau TeX) adalah sistem produksi dokumen. Kita membuat dokumen yang diberi tanda, _markup_, yang dikenali oleh LaTeX. Lalu dokumen tersebut diberikan ke _compiler_ LaTeX untuk dijadikan dokumen dalam bentuk PDF. Kalau dilihat dari cara kerjanya, LaTeX mirip seperti pemrograman biasa. Itu mengundang sisi _programmer_ saya untuk keluar dan mulai membuat résumé.

Menurut saya ada beberapa alasan bagus untuk membuat résumé dengan LaTeX diantaranya.

## Tampilan yang beda

Résumé seorang _programmer_ mungkin tidak harus seindah milik desainer, namun penampilan beda itu perlu. Yang paling membedakan dari résumé yang dibuat di LaTeX adalah pilihan fonta dan juga _justify_ yang dihasilkan oleh LaTeX terlihat lebih indah dari pada yang dihasilkan oleh _Office Suite_ seperti Microsoft Office atau Libre Office.

Résumé yang dibuat tidak akan lagi pakai fonta Times New Roman, Arial, atau Calibri (apalagi Comic Sans). Ini berpengaruh besar sebagai pembeda dari résumé lain. Saya sendiri menggunakan Tex Gyre Pagella dan Clear Sans.

## Format Sekali dan Ganti Isinya

Saya hanya perlu membuat format saya sekali saja dan membiarkan LaTeX yang mengurus lainnya. Saya tidak perlu memikirkan _line spacing_ yang diganti atau mungkin _indent_ yang sudah diatur sedemikian rupa. Lalu beberapa bulan selanjutnya saya ingin mengganti atau menambahkan isinya, dan format saya hancur berantakan karena panjang tulisannya berbeda dengan yang lama.

## Bisa menggunakan _Version Control_

Résumé biasanya dibuat sesuai dengan pekerjaan yang ingin dilamar. Jika kita ingin mendaftar di posisi yang berbeda, isi résumé biasanya diubah untuk menampilkan pengalaman atau ketrampilan yang sesuai dengan kebutuhan pekerjaan. Orang-orang biasanya akan membuat dokumen dengan nama, `resume-lamaran-sisadmin.docx`, `resume-lamaran-job fair (1).docx`, dan kombinasi nama aneh lainnya.

Namun dengan _version control_, biasanya saya pakai `git`, kita bisa membuat satu dokumen yang memiliki beberapa versi. Selain itu kita juga bisa dengan mudah melihat perbedaan dari setiap versi.

## Tips dan Trik

* Manfaatkan macro pada LaTeX untuk mengurangi penulisan sesuatu hal yang berulang.
* Gunakan _version control_, ini penting!

![Resume](/images/uploads/screenshot-from-2018-07-17-08-37-16.png)

Jika tertarik dan ingin bertanya bisa kirim surel ke alamat surel saya.
