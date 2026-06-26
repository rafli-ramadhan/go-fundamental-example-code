# Go Routine vs Synchronous

Kodingan di bawah ini untuk menunjukkan siapa yang lebih cepat antara synchronous dan go routine. Synchronous diwakili dengan fmt.Println() tanpa go func().

Intinya yaitu go routine tidak selalu lebih cepat dari pada kode program synchronous. Go routine digunakan untuk membuat aplikasi lebih cepat, bukan membuat kodingan lebih cepat (Julizar Wira, 2023).

## Implementasi Time Sleep

```go
package main

import (
	"fmt"
	"time"
)

func main() {
    fmt.Println("start")
    duration := time.Now()

    go func() {
        fmt.Println("test 1", time.Since(duration))
        go func() {
            fmt.Println("test 1.a", time.Since(duration))
        }()
            
        go func() {
            fmt.Println("test 1.b", time.Since(duration))
        }()
    
        go func() {
            fmt.Println("test 1.c", time.Since(duration))
        }()
        
        fmt.Println("test 2", time.Since(duration))
	}()
    
    fmt.Println("end", time.Since(duration))
    time.Sleep(2*time.Second)
    fmt.Println("end", time.Since(duration))
}
```

```
start
end 14.316µs
test 1 80.584µs
test 2 118.592µs
test 1.c 128.012µs
test 1.a 143.493µs
test 1.b 156.41µs
end 2.000573491s
```

## Implementasi Sync Wait Group

```go
package main

import (
	"fmt"
	"time"
	"sync"
)

var wg sync.WaitGroup

func main() {
    fmt.Println("start")
    duration := time.Now()

    go func() {
        fmt.Println("test 1", time.Since(duration))
        
        wg.Add(3)
        go func() {
            fmt.Println("test 1.a", time.Since(duration))
        }()
            
        go func() {
            fmt.Println("test 1.b", time.Since(duration))
        }()
    
        go func() {
            fmt.Println("test 1.c", time.Since(duration))
        }()
        
        fmt.Println("test 2", time.Since(duration))
        wg.Wait()
        fmt.Println("test 3", time.Since(duration))
	}()
    
    fmt.Println("end", time.Since(duration))
    time.Sleep(2*time.Second)
    fmt.Println("end", time.Since(duration))
}
```

```
start
end 17.017µs
test 1 883.865µs
test 2 1.588318ms
test 1.c 1.636508ms
test 1.a 1.658898ms
test 1.b 1.671221ms
end 2.002663523s
```
