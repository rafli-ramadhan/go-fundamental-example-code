# Timer & After

## Timer

Timer adalah representasi waktu satu kejadian

Ketika waktu timer sudah expire, maka event akan dikirim ke dalam channel Untuk membuat Timer kita bisa menggunakan fungsi time.NewTimer(duration).

Fungsi time.NewTimer() mengembalikan struct \*time.Timer yang memiliki property C yang bertipe channel.

```go
func time.NewTimer(d time.Duration) *time.Timer
```

```go
package main
 
import (
    "fmt"
    "time"
)

func main() {
    timer := time.NewTimer(5 * time.Second)
    fmt.Println(time.Now())
    
    timeTimer := <-timer.C
    fmt.Println(timeTimer)
}
```

```
2023-03-28 11:25:07.7328437 +0700 +07 m=+0.002623201
2023-03-28 11:25:12.7468608 +0700 +07 m=+5.016640301
```

## After

Kadang kita hanya butuh channel Timer saja, tidak membutuhkan data Timer -> bisa menggunakan function time.After(duration)

```go
func time.After(d time.Duration) <-chan time.Time
```

<pre class="language-go"><code class="lang-go">package main
 
import (
    "fmt"
    "time"
)

func main() {
    timer := time.After(1 * time.Second)
    fmt.Println(time.Now())
    
    timeTimer := &#x3C;-timer
<strong>    fmt.Println(timeTimer)
</strong>}
</code></pre>

```
2023-03-28 11:33:45.2167092 +0700 +07 m=+0.002684001
2023-03-28 11:33:46.2264751 +0700 +07 m=+1.012449901
```
