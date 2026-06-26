# Deadlock - All goroutines are asleep

Deadlock -> kondisi dimana go routine saling tunggu -> alhasil tidak ada go routine yang berjalan.

## Contoh Kasus #1

Jika channel in (pengirim) di inisisasi terlebih dahulu dan channel out (penerima) di inisiasi setelah channel in -> deadlock -> karena belum ada penerimanya.

Channel in dan channel out harus berjalan bersama -> caranya salah satu di inisiasi terlebih dahulu dan yang pertama di inisiasi dimasukkan ke dalam go routine.

### Program #1

```go
package main

import "fmt"

func main() {
        ch := make(chan int)
        // channel in (pengirim)
        ch <- 1
        // channel out (penerima)
        go func() {
            result := <- ch
            fmt.Println(result)
        }()
}
```

<pre><code>fatal error: all goroutines are asleep - deadlock!
<strong>goroutine 1 [chan send]:
</strong>main.main()
/tmp/uv1yQwKDgN.go:7 +0x37
exit status 2
</code></pre>

```go
package main

import "fmt"

func main() {
        ch := make(chan int)
        // channel out (penerima)
        go func() {
            result := <- ch
            fmt.Println(result)
        }()
        // channel in (pengirim)
        ch <- 1
}
```

```
1
```

```go
package main

import "fmt"

func main() {
    ch := make(chan int)
    // channel in (pengirim)
    go func() {
	ch <- 1
    }()
    // channel out (penerima)
    result := <- ch
    fmt.Println(result)
}
```

```
1
```

### Program #2

```go
package main
  
import "fmt"

func f(value chan int) {
    result := 100 + <- value
    fmt.Printf("%d ", result)
}

func main() {
    fmt.Println("Start")
    value := make(chan int)

    for i := 0; i < 10; i++ {
        // channel in (pengirim)
        value <- i
        // channel out (penerima)
        go f(value)
    }
    
    fmt.Println("\nEnd")
    close(value)
}
```

```
Start
fatal error: all goroutines are asleep - deadlock!

goroutine 1 [chan send]:
main.main()
        D:/go-server/main.go:15 +0x9e
exit status 2
```

```go
package main
  
import "fmt"

func f(value chan int) {
    result := 100 + <- value
    fmt.Printf("%d ", result)
}

func main() {
    fmt.Println("Start")
    value := make(chan int)

    for i := 0; i < 10; i++ {
        //channel out (penerima)
        go f(value)
        // channel in (pengirim)
        value <- i
    }
    
    fmt.Println("\nEnd")
    close(value)
}
```

```
Start
100 101 102 103 104 105 106 107 108 109 
End
```

```go
package main
  
import "fmt"

func f(value chan int) {
    result := 100 + <- value
    fmt.Printf("%d ", result)
}

func main() {
    fmt.Println("Start")
    value := make(chan int)

    for i := 0; i < 10; i++ {
        // channel in (pengirim)
	go func() {
	        value <- i
	}()
	//channel out (penerima)
        f(value)
    }
    
    fmt.Println("\nEnd")
    close(value)
}
```

```
Start
100 101 102 103 104 105 106 107 108 109 
End
```

## Program #3 deadlock jika channel tidak di close

```go
package main

import (
    "fmt"
)

func main() {
    ch := make(chan int)

    go func() {
        for i := 0; i < 5; i++ {
			// channel in
            ch <- i
        }
		// channel must be close
		// if not will be deadlock
        close(ch)
    }()

// channel out
    for v := range ch {
        fmt.Println(v)
    }
}

```

```
0
1
2
3
4
5
```



<figure><img src="https://divan.dev/demos/gifs/hello.gif" alt=""><figcaption><p>Source: <a href="https://divan.dev/posts/go_concurrency_visualize/">https://divan.dev/posts/go_concurrency_visualize/</a></p></figcaption></figure>

Reference:

{% embed url="https://golangbot.com/channels/" %}
