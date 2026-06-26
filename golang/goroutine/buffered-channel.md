# Buffered Channel

Default channel hanya bisa menerima 1 data -> jika ditambah data ke-2, maka kita akan diminta menunggu sampai data ke-1 ada yang mengambil.

Kadang-kadang ada kasus dimana pengirim lebih cepat dibanding penerima, dalam hal ini jika kita menggunakan channel, maka otomatis pengirim akan ikut lambat juga.

Buffered Channel -> buffer yang bisa digunakan untuk menampung data antrian di Channel.

{% embed url="https://th.bing.com/th/id/OIP.VdZlb_xgxtUYe10p1IPewQHaDx?pid=ImgDet&rs=1" %}
[https://th.bing.com/th/id/OIP.VdZlb\_xgxtUYe10p1IPewQHaDx?pid=ImgDet\&rs=1](https://th.bing.com/th/id/OIP.VdZlb\_xgxtUYe10p1IPewQHaDx?pid=ImgDet\&rs=1)
{% endembed %}

## Buffer Capacity

Jika di set misal 5, artinya channel bisa menerima 5 data di buffer.&#x20;

Jika dikirim data ke 6, maka kita diminta untuk menunggu sampai buffer ada yang kosong. Buffer channel cocok digunakan apabila goroutine yang menerima data lebih lambat dari yang mengirim data

```go
package main

import (
	"fmt"
	"time"
)

func write(ch chan int) {
	for i := 0; i < 20; i++ {
	        // write value
	        ch <- i
	        fmt.Printf("write%d ", i)
	}
	close(ch)
}

func main() {
	ch := make(chan int, 12)

	go write(ch)

    	for i := range ch {
        	// read value
        	fmt.Printf("%d ", i)
		time.Sleep(700 * time.Millisecond)
	}
}
```

```
write0 write1 write2 write3 write4 write5 write6 write7 write8 write9 write10 0 1 write11 2 write12 write13 3 4 write14 5 write15 6 write16 7 write17 8 write18 9 write19 10 11 12 13 
14 15 16 17 18 19 
```
