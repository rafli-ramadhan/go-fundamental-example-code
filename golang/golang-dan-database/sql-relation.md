# SQL Relation

## One To One

Satu baris data di tabel A berhubungan dengan satu baris data di tabel B. Contohnya misal ada 1 baris data di tabel User yang memiliki informasi 1 baris data dari tabel Status.

<figure><img src="../../.gitbook/assets/one to one (1).png" alt=""><figcaption></figcaption></figure>

## One To Many

Satu baris data di tabel A berhubungan dengan beberapa baris data di tabel B. Contohnya misal pada Tabel Item\_Penjual berikut terdapat 2 baris data dengan Id\_Penjual sama dengan 1.

<figure><img src="../../.gitbook/assets/one to many (1).png" alt=""><figcaption></figcaption></figure>

## Many to Many

Beberapa baris data di tabel A berhubungan dengan beberapa baris data di tabel B. Untuk kasus tabel many to many diperlukan tabel perantara antara tabel A dan B. Contohnya misal ada data user yang membeli beberapa item yang kemudian disimpan dalam Tabel User\_Item, maka beberapa baris di Tabel A bisa dikatakan berhubungan dengan beberapa baris di Tabel B.

<figure><img src="../../.gitbook/assets/many to many (1).png" alt=""><figcaption></figcaption></figure>

## Has Many and Belongs To

_Has many_ merupakan istilah yang dapat digunakan untuk mendiskripsikan relasi one to many (1:n) dan many to many (n:n). Sementara belongs to dapat digunakan untuk mendiskripsikan relasi one to one (1:1) dan many to one(n:1). Sebagai catatan untuk many to one merupakan kebalikan dari one to many.

Referensi :

{% embed url="https://medium.com/@fahmisyaifudin35/relasi-tabel-database-one-to-one-one-to-many-many-to-many-44010f703f57" %}

{% embed url="https://softwareengineering.stackexchange.com/questions/152731/what-is-the-main-difference-between-has-many-and-belongs-to-relationship-in-mysq" %}
