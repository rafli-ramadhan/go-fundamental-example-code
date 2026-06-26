# Setting RabbitMQ (Durable, Auto Delete dan Ack)

## Durable

RabbitMQ akan menghapus queue dan pesan saat berhenti atau crash. Hal tersebut dapat dihindari dengan mengaktifkan message durability pada bagian QueueDeclare di sender.go atau publisher.go menjadi `true`. Dengan begitu pesan dan queue pada RabbitMQ akan dapat bertahan saat RabbitMQ di restart.

```go
        q, err := ch.QueueDeclare(
		"hello", // name
		false,   // durable
		false,   // delete when unused
		false,   // exclusive
		false,   // no-wait
		nil,     // arguments
	)
```

## Auto Delete

Auto delete merupakan setting dari RabbitMQ yang memungkinkan queue yang tidak terpakai akan langsung di delete. Setting auto delete bisa dilakukan dari sisi publisher atau consumer pada code QueueDeclare.

<pre class="language-go"><code class="lang-go"><strong>        q, err := ch.QueueDeclare(
</strong>		"task_queue", // name
		true,         // durable
		false,        // auto delete queue when unused
		false,        // exclusive
		false,        // no-wait
		nil,          // arguments
	)
	failOnError(err, "Failed to declare a queue")
</code></pre>



## Acknowledge

AutoAck bisa di setting di _code_ receiver atau consumer pada bagian Consume.

```go
        msgs, err := ch.Consume(
		q.Name, // queue
		"",     // consumer
		true,   // auto-ack
		false,  // exclusive
		false,  // no-local
		false,  // no-wait
		nil,    // args
	)
	failOnError(err, "Failed to register a consumer")
```

* Case 1, auto-ack di set true, maka hasil running consumer dan publisher akan seperti video di bawah ini. Publisher tidak akan peduli, apakah consumer mati atau hidup, data akan tetap dikirim.

{% embed url="https://drive.google.com/file/d/1BhHJ99J5WQlp02_3uTiINyEx_b9CnrEJ/view?usp=sharing" %}

* Case 2, auto-ack di set false dan d.Ack(false)

{% embed url="https://drive.google.com/file/d/1CJoVScX52ee2XgR6QFXEQ5U0aDAfoV2q/view?usp=sharing" %}

* Case 3, auto-ack di set false dan tidak ada d.Ack

{% embed url="https://drive.google.com/file/d/1bPnDWRIOFZCRl-ujXIzZHiZYA4jg1Ol-/view?usp=sharing" %}
