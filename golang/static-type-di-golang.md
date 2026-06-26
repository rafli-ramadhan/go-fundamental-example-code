---
coverY: 0
---

# Static Type di Golang

Salah satu keunggulan golang yaitu adanya _static type_. _**Static type**_ pada golang menyebabkan suatu variabel hanya dapat di inisiasi dengan 1 tipe data dan tipe data tersebut tidak dapat di ubah. Keunggulan dari static type diantaranya adalah:&#x20;

1. Meminimalisir bug -> Pengecekan tipe data oleh kompiler dapat menghindari bug remeh yang berkaitan dengan tipe data. Jika ada kesalahan tipe data pasti akan ada error pada compiler.
2. Self documented code -> Dengan tipe data pada setiap variabel, kita jadi punya gambaran yang jelas bagaimana variabel tersebut harus diperlakukan. Hal ini juga memungkinkan scaling program yang lebih mudah.
3. Meningkatkan DX -> Fitur IDE seperti code completion dan code suggestion yang aktif tentunya dapat meningkatkan developer experience (DX). Belum lagi beberapa bahasa yang menyediakan formatter dan linter secara bawaan.
4. Performa lebih cepat -> Karena ketika eksekusi tidak lagi dilakukan pengecekan, perintah kode bisa berjalan dengan lebih cepat. Hal ini juga berlaku untuk compiled language pada umumnya.

Informasi lainnya dapat diakses di link berikut [https://forum.golangbridge.org/t/static-types-and-statically-typed/9777](https://forum.golangbridge.org/t/static-types-and-statically-typed/9777).
