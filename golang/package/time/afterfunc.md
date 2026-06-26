# AfterFunc

AfterFunc -> untuk menjalankan sebuah function dengan delay waktu tertentu.

```go
func time.AfterFunc(d time.Duration, f func()) *time.Timer
```

```go
package main
 
import (
    "fmt"
    "sync"
    "time"
)

func main() {
    wg := sync.WaitGroup{}
    wg.Add(1)
    time.AfterFunc(1*time.Second, func() {
        fmt.Println("execute after func")
        wg.Done()
    })

    fmt.Println("start")
    wg.Wait()
    fmt.Println("finish")
}
```

```
start
execute after func
finish
```
