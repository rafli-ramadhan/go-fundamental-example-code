---
description: https://www.rabbitmq.com/tutorials/tutorial-two-go.html
---

# Publisher dan Multi Consumer

## Konsep

<figure><img src="../../.gitbook/assets/p1.png" alt=""><figcaption><p><a href="https://www.rabbitmq.com/tutorials/tutorial-two-go.html">https://www.rabbitmq.com/tutorials/tutorial-two-go.html</a></p></figcaption></figure>

Ide utama yang dimiliki oleh RabbitMQ yakni publish/subscribe, publish subscribe berarti mengirimkan pesan ke beberapa consumer. Konsep pada gambar di atas mirip dengan bahasan sebelumnya, perbedaannya pada jumlah konsumer. Untuk membuat lebih dari satu consumer, bisa dengan menjalankan 1 _code_ consumer di beberapa terminal yang berbeda.

## Tutorial

* Copy code worker sebagai consumer (receiver) dari link di bawah ini di file consumer.go.&#x20;

{% embed url="https://github.com/rabbitmq/rabbitmq-tutorials/blob/main/go/worker.go" %}

* Copy code new\_task sebagai publisher (sender) dari link di bawah ini di file publisher.go

{% embed url="https://github.com/rabbitmq/rabbitmq-tutorials/blob/main/go/new_task.go" %}

* Struktur folder akan tampak seperti di bawah ini.

<figure><img src="../../.gitbook/assets/p1 (3).png" alt=""><figcaption></figcaption></figure>

* Buka 3 terminal (bisa CMD/powershell/git bash)
* Jalankan consumer.go (consumer / receiver) terlebih dahulu di terminal ke-1 dan terminal ke-2 menggunakan command di bawah ini, sehingga ada 2 consumer yang berjalan.

```
go run consumer/consumer.go
```

<figure><img src="../../.gitbook/assets/terminal.png" alt=""><figcaption><p>Menjalankan publisher dan consumer di 3 terminal yang berbeda</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/p (1).png" alt=""><figcaption><p>Terminal publisher</p></figcaption></figure>

* Selanjutnya baru jalankan publisher.go (publisher / sender) dengan command di bawah ini di terminal ke-3.

```
go run publisher/publisher.go
```

* Amati juga log yang tampil di terminal kedua consumer seperti di bawah ini. Pesan dari publisher diterima oleh kedua consumer secara bergantian (disebut Round Robin).

<figure><img src="../../.gitbook/assets/consumer1.png" alt=""><figcaption><p>Terminal consumer 1</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/consumer2.png" alt=""><figcaption><p>Terminal consumer 2</p></figcaption></figure>
