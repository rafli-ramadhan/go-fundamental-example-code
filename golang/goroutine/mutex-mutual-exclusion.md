# Mutex (Mutual Exclusion)

Mutex -> digunakan untuk mengatasi race condition -> locking dan unlocking

Dimana ketika kita melakukan locking terhadap mutex, maka tidak ada yang bisa melakukan locking lagi sampai kita melakukan unlock.&#x20;

Jika ada beberapa goroutine melakukan lock terhadap Mutex, maka hanya 1 goroutine yang dieksekusi, setelah goroutine tersebut melakukan unlock, baru goroutine selanjutnya melakukan lock lagi.

Kekurangan -> ada kemungkinan beberapa go routine saling menggu untuk melakukan lock -> bisa menimbulkan deadlock.

```go
package main
 
import (
    "fmt"
    "sync"
)

var wg sync.WaitGroup
var m sync.Mutex

func f(v *int, wg *sync.WaitGroup) {
    m.Lock()
    *v++
    m.Unlock()
    wg.Done()
}
 
func main() {
    var v int = 0
 
    for i := 0; i < 1000; i++ {
        wg.Add(1)
        go f(&v, &wg)
    }
 
    wg.Wait()
    fmt.Println("Finished", v)
}
```

```
Finished 1000
```

```go
package main
 
import (
    "fmt"
    "sync"
)

var wg sync.WaitGroup
var m sync.Mutex

func f(v *int, wg *sync.WaitGroup) {
    m.Lock()
    *v++
    m.Unlock()
    wg.Done()
}
 
func main() {
    var v int = 0
 
    for i := 0; i < 10000; i++ {
        wg.Add(1)
        go f(&v, &wg)
    }
 
    wg.Wait()
    fmt.Println("Finished", v)
}
```

```
Finished 10000
```

```go
package main
 
import (
    "fmt"
    "sync"
)

var wg sync.WaitGroup
var m sync.Mutex
 
func main() {
    var v int = 0
 
    for i := 0; i < 10000; i++ {
        wg.Add(1)
        go func() {
            m.Lock()
            v++
            m.Unlock()
            wg.Done()
        }()
    }
    
    wg.Wait()
    fmt.Println("Finished", v)
}
```

```
Finished 10000
```
