# Channel

**Fungsi** -> tempat komunikasi data secara synchronous oleh go routine -> saat melakukan pengiriman data, go routine akan terblok sampai ada yang menerima data tersebut (blocking).

**Karakteristik** -> hanya bisa menerima 1 tipe data, secara default hanya bisa menampung 1 data, jika tidak digunakan harus di close atau bisa menyebabkan memory leak.

**Channel In -> Mengirim data**

**Channel Out -> Menerima data**

**Sifatnya -> Blocking**

**Channel harus di close -> jika tidak bisa menyebabkan memory leak**

## Contoh #1

```go
package main
  
import "fmt"
  
func test(value chan int) {
    // channel out
    result := 100 + <- value
    fmt.Printf("%d ", result)
}

func main() {
    fmt.Println("Start")
    value := make(chan int)

    for i := 0; i < 10; i++ {
        go test(value)
        // channel in
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

## Contoh 2

```go
package main
  
import "fmt"
  
func test(value chan int) {
    result := 100 + <- value
    value <- result
}

func main() {
    fmt.Println("Start")
    value := make(chan int)

    for i := 0; i < 10; i++ {
        go test(value)
        // channel in
        value <- i
        // channel out
        result := <- value
        fmt.Printf("%d ", result)
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

## Contoh 3

<pre class="language-go"><code class="lang-go"><strong>package main
</strong>  
import "fmt"

func main() {
    fmt.Println("Start")
    value := make(chan int)

    for i := 0; i &#x3C; 10; i++ {
        go func(i int) {
            result := 100 + i
            // channel in
            value &#x3C;- result
        }(i)
        // channel out
        print := &#x3C;- value
        fmt.Printf("%d ", print)
    }
    fmt.Println("\nEnd")
    close(value)
}
</code></pre>

```
Start
100 101 102 103 104 105 106 107 108 109 
End
```

## Channel perlu di close

Channel perlu di close untuk mengindikasikan tidak ada data yang dikirim lagi ke channel

Reference:

{% embed url="https://www.scaler.com/topics/golang/closing-the-channel-in-golang/" %}
