# Instalasi Package RabbitMQ di Golang

Package RabbitMQ di Golang digunakan supaya pesan dari suatu aplikasi bisa dikirim ke RabbitMQ yang kemudian juga bisa diterima oleh suatu aplikasi.

1. Buat folder baru dan inisiasi go module dengan command berikut.

```
go mod init nama_project
```

2. Instalasi package RabbitMQ di Golang dapat menggunakan command berikut.

```bash
go get github.com/rabbitmq/amqp091-go
```

3. Setelah proses install selesai, selanjutnya adalah membuat _code_ untuk sender dan receiver yang akan dibahas setelah ini.
4. Jangan lupa untuk menjalankan server RabbitMQ yang telah di install di docker.
