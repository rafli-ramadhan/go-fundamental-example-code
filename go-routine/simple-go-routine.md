# Simple Go Routine

```go
package main

import (
	"fmt"
	"time"
)

func main() {
    fmt.Println("start")

    go func() {
        fmt.Println("test 1")
	}()
    
    go func() {
        fmt.Println("test 2")
    }()
        
    go func() {
        fmt.Println("test 3")
    }()
        
    go func() {
        fmt.Println("test 4")
    }()
    
    time.Sleep(3*time.Millisecond)
    fmt.Println("end")
}
```

```
PS D:\go-server> go run main.go
start
test 4
test 2
test 3
test 1
PS D:\go-server> go run main.go
start
test 1
test 4
test 2
test 3
PS D:\go-server> go run main.go
start
test 4
test 1
test 3
test 2
end
PS D:\go-server> go run main.go
start
test 4
test 3
test 2
test 1
end
PS D:\go-server> 
```

```go
package main

import (
	"fmt"
	"sync"
)

var wg sync.WaitGroup

func main() {
    fmt.Println("start")

    wg.Add(4)
    go func() {
        fmt.Println("test 1")
		wg.Done()
    }()
    
    go func() {
        fmt.Println("test 2")
		wg.Done()
    }()
        
    go func() {
        fmt.Println("test 3")
		wg.Done()
    }()
        
    go func() {
        fmt.Println("test 4")
		wg.Done()
    }()

    wg.Wait()
	
    fmt.Println("end")
}
```

```
PS D:\go-server> go run .
start
test 4
test 2
test 1
test 3
PS D:\go-server> go run .
start
test 4
test 2
test 1
test 3
PS D:\go-server> go run .
start
test 1
test 4
test 2
test 3
PS D:\go-server> go run .
start
test 1
test 4
test 2
test 3
end
PS D:\go-server> go run .
start
test 4
test 1
test 2
test 3
end
```

## Go routine with Looping

```go
package main

import (
	"fmt"
	"sync"
)

var wg sync.WaitGroup

func main() {
    for i := 0; i<100; i++ {
	var i int = i
	wg.Add(1)
        go func() {
            fmt.Printf("test %d ",i+1)
	    wg.Done()
        }()
        wg.Wait()
    }
}
```

```
test 1 test 2 test 3 test 4 test 5 test 6 test 7 test 8 test 9 test 10 test 11 test 12 test 13 test 14 test 15 test 16 test 17 test 18 test 19 test 20 test 21 test 22 test 23 test 24 test 25 test 26 test 27 test 28 test 29 test 30 test 31 test 32 test 33 test 34 test 35 test 36 test 37 test 38 test 39 test 40 test 41 test 42 test 43 test 44 test 45 test 46 test 47 test 48 test 49 test 50 test 51 test 52 test 53 test 54 test 55 test 56 test 57 test 58 test 59 test 60 test 61 test 62 test 63 test 64 test 65 test 66 test 67 test 68 test 69 test 
70 test 71 test 72 test 73 test 74 test 75 test 76 test 77 test 78 test 79 test 80 test 81 test 82 test 83 test 84 test 85 test 86 test 87 test 88 test 89 test 90 test 91 test 92 test 93 test 94 test 95 test 96 test 97 test 98 test 99 test 100
```