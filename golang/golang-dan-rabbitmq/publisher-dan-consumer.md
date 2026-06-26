---
description: https://www.rabbitmq.com/tutorials/tutorial-one-go.html
---

# Publisher dan Consumer

## Konsep

Konsep publisher (sender) dan sender (receiver) dapat diamati pada gambar berikut. Publisher dan Consumer bisa diasumsikan file.go yang berbeda, sementara blok merah merupakan queue yang merupakan data yang dikirim mengikuti aturan FIFO (first in first out).

<figure><img src="../../.gitbook/assets/p1 (4).png" alt=""><figcaption><p><a href="https://www.rabbitmq.com/tutorials/tutorial-one-go.html">https://www.rabbitmq.com/tutorials/tutorial-one-go.html</a></p></figcaption></figure>

## Tutorial

* Buat file misal sender.go di folder sender dan _copy code_ pada link di bawah ini. Data yang dikirim dari sender.go adalah data dengan tipe data byte. Data tersebut bisa dilihat pada variabel body.

{% embed url="https://github.com/rabbitmq/rabbitmq-tutorials/blob/main/go/send.go" %}

* Buat file misal receiver.go di folder receiver dan _copy code_ pada link berikut

{% embed url="https://github.com/rabbitmq/rabbitmq-tutorials/blob/main/go/receive.go" %}

* Struktur folder dan file yang dibuat bisa seperti di bawah ini.

<figure><img src="../../.gitbook/assets/d (2).png" alt=""><figcaption></figcaption></figure>

* Sebelum data dikirim dari sender, tampilan UI RabbitMQ akan seperti ini

<figure><img src="../../.gitbook/assets/o1.png" alt=""><figcaption></figcaption></figure>

* Selanjutnya coba jalankan sender.go dengan command berikut.

```
go run sender/sender.go
```

* Grafik pada UI RabbitMQ akan naik menjadi 1, artinya ada 1 queue yang masuk namun belum ada penerima.

<figure><img src="../../.gitbook/assets/o2.png" alt=""><figcaption></figcaption></figure>

&#x20;

* Selanjutnya jalankan lagi go run sender.sender.go, maka grafiknya akan naik menjadi 2, artinya ada 2 queue yang masuk.

<figure><img src="../../.gitbook/assets/o3.png" alt=""><figcaption></figcaption></figure>

* Selanjutnya coba jalankan receiver dengan command berikut.

```
go run receiver/receiver.go
```

* Receiver akan menerima semua data queue yang telah dikirim dari sender. Sehingga grafik di UI RabbitMQ akan menurun menjadi 0, artinya pesan sudah di terima oleh receiver.go. Log dari pesan juga akan ditampilkan di terminal.

<figure><img src="../../.gitbook/assets/r (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/o4.png" alt=""><figcaption></figcaption></figure>
