---
description: https://hub.docker.com/_/mysql/
---

# Instalasi MySQL dengan Docker Desktop

Jalankan docker desktop, lalu buka tab search dan cari image MySQL.

<figure><img src="../../.gitbook/assets/docker mysql.png" alt=""><figcaption></figcaption></figure>

Selanjutnya pull image MySQL dan tunggu sampai proses download selesai. Setelah proses download selesai, image MySQL akan otomatis muncul di tab Images.

<figure><img src="../../.gitbook/assets/Docker mysql images.png" alt=""><figcaption></figcaption></figure>

Selanjutnya klik tombol run di sebelah kanan image MySQL dan klik drop down optional setting.&#x20;

<figure><img src="../../.gitbook/assets/mysql optional setting.png" alt=""><figcaption></figcaption></figure>

Definisikan environment variable MYSQL\_ROOT\_PASSWORD dan MYSQL\_DATABASE dan isi sesuai keinginan.

<figure><img src="../../.gitbook/assets/docker mysql run.png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/docker mysql env.png" alt=""><figcaption></figcaption></figure>

Lalu klik run dan cek tab container untuk memastikan container MySQL sudah berjalan.

<figure><img src="../../.gitbook/assets/docker mysql image.png" alt=""><figcaption></figcaption></figure>

Gunakan GUI seperti DBeaver untuk cek koneksi MySQL. Untuk URL dapat diisi dengan format di bawah ini. Nama database diisi dengan nama database yang sama saat mengisi optional setting env saat ingin running image MySQL.  Lalu klik Test Connection terlebih dahulu, lalu klik OK untuk membuka database.

```
jdbc:mysql://localhost:3306/nama_database?allowPublicKeyRetrieval=true
```

<figure><img src="../../.gitbook/assets/Dbeaver.png" alt=""><figcaption></figcaption></figure>
