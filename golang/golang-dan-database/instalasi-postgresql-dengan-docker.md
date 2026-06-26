---
description: https://hub.docker.com/_/postgres/
---

# Instalasi PostgreSQL dengan Docker

Jalankan docker desktop, lalu buka tab search dan cari image PostgreSQL. Pada tutorial ini digunakan image PostgreSQL dengan tag alpine3.18.

<figure><img src="../../.gitbook/assets/postgres tag.png" alt=""><figcaption></figcaption></figure>

Selanjutnya pull image PostgreSQL dan tunggu sampai proses download selesai. Setelah proses download selesai, image PostgreSQL akan otomatis muncul di tab Images.

<figure><img src="../../.gitbook/assets/postgres images.png" alt=""><figcaption></figcaption></figure>

Selanjutnya klik tombol run di sebelah kanan image PostgreSQL dan klik drop down optional setting.

<figure><img src="../../.gitbook/assets/postgres optional setting.png" alt=""><figcaption></figcaption></figure>

Definisikan environment variable POSTGRES\_PASSWORD dan isi sesuai keinginan.

<figure><img src="../../.gitbook/assets/postgres optional setting true.png" alt=""><figcaption></figcaption></figure>

Lalu klik run dan cek tab container untuk memastikan container PostgreSQL sudah berjalan.

<figure><img src="../../.gitbook/assets/postgres container.png" alt=""><figcaption></figcaption></figure>

Gunakan GUI seperti DBeaver untuk cek koneksi PostgreSQL. Untuk setting bisa mengikuti gambar di bawah ini. Lalu klik Test Connection terlebih dahulu, lalu klik OK untuk membuka database.

<figure><img src="../../.gitbook/assets/postgres Dbeaver.png" alt=""><figcaption></figcaption></figure>
