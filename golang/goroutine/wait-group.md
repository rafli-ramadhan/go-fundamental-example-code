# Wait Group

WaitGroup adalah mekanisme digolang yang berfungsi untuk melakukan sinkronisasi antara goroutine. WaitGroup memiliki cara kerja yang sama dengan sleep pada go routine. Jika menggunakan sleep, maka kita akan memaksa go routine untuk berhenti dalam waktu tertentu. Hal tersebut akan membuat program lebih lambat.

## Contoh _code_ wait group 1

```go
package main

import (
	"fmt"
	"sync"
)

func main() {
	var wg sync.WaitGroup
	num := []int{1, 2, 3, 4, 5}

	for _, v := range num {
		wg.Add(1)
        
        go func (v int) {
            defer wg.Done()
            fmt.Println(v)
        }(v)
	}
	wg.Wait()
}
```

```
PS D:\bootcamp-go\go-routine> go run main.go
1
5
4
2
3
PS D:\bootcamp-go\go-routine> go run main.go
5
2
1
3
4
PS D:\bootcamp-go\go-routine> go run main.go
5
2
1
3
4
```

## Contoh _code_ wait group 2

```go
var wg sync.WaitGroup()
```

```go
package main

import (  
    "fmt"
    "sync"
)

func numbers(wg *sync.WaitGroup) {
    defer wg.Done()
    for i := 1; i <= 5; i++ {
        fmt.Printf("%d ", i)
    }
}

func alphabets(wg *sync.WaitGroup) {
    defer wg.Done()
    for i := 'a'; i <= 'e'; i++ {
        fmt.Printf("%c ", i)
    }
}

func main() {
    wg := new(sync.WaitGroup)

    for i := 0; i <= 10; i++ {
        wg.Add(2)
        go numbers(wg)
        go alphabets(wg)
        wg.Wait()
    }

    fmt.Println("end")
}
```

```
a b c d e 1 2 3 4 5 a b c d e 1 2 3 4 5 a b c d e 1 2 3 4 5 a b c d e 1 2 3 4 5 a b c d e 1 2 3 4 5 a b c d e 1 2 3 4 5 a b c d e 1 2 3 4 5 a b c d e 1 2 3 4 5 a b c d e 1 2 3 4 5 a 
b c d e 1 2 3 4 5 a b c d e 1 2 3 4 5 end
```

Reference:

{% embed url="https://kodingin.com/golang-waitgroup/" %}
