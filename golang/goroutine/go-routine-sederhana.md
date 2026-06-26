# Go Routine Sederhana

## Go Routine dengan Time Sleep

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
	}()
    
    go func() {
        fmt.Println("test 2", time.Since(duration))
    }()
        
    go func() {
        fmt.Println("test 3", time.Since(duration))
    }()
        
    go func() {
        fmt.Println("test 4", time.Since(duration))
    }()

    go func() {
        fmt.Println("test 5", time.Since(duration))
    }()
    
    fmt.Println("sleep 2 second", time.Since(duration))
    time.Sleep(2*time.Second)
    fmt.Println("end", time.Since(duration))
}
```

```
start
sleep 2 second 32.806µs
test 5 68.975µs
test 1 97.493µs
test 2 108.316µs
test 3 117.996µs
test 4 125.836µs
end 2.000692238s
```

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

## Go Routine with Sync Wait Group

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
            fmt.Printf("start %d ",i+1)
            fmt.Printf("end %d ",i+1)
	    wg.Done()
        }()
        wg.Wait()
    }
}
```

```
start 1 end 1 start 2 end 2 start 3 end 3 start 4 end 4 start 5 end 5 start 6 end 6 start 7 end 7 start 8 end 8 start 9 end 9 start 10 end 10 start 11 end 11 start 12 end 12 start 13 end 13 start 14 end 14 start 15 end 15 start 16 end 16 start 17 end 17 start 18 end 18 start 19 end 19 start 20 end 20 start 21 end 21 start 22 end 22 start 23 end 23 start 24 end 24 start 25 end 25 start 26 end 26 start 27 end 
27 start 28 end 28 start 29 end 29 start 30 end 30 start 31 end 31 start 32 end 32 start 33 end 33 start 34 end 34 start 35 end 35 start 
36 end 36 start 37 end 37 start 38 end 38 start 39 end 39 start 40 end 40 start 41 end 41 start 42 end 42 start 43 end 43 start 44 end 44 start 45 end 45 start 46 end 46 start 47 end 47 start 48 end 48 start 49 end 49 start 50 end 50 start 51 end 51 start 52 end 52 start 53 end 53 start 54 end 54 start 55 end 55 start 56 end 56 start 57 end 57 start 58 end 58 start 59 end 59 start 60 end 60 start 61 end 61 start 62 end 62 start 63 end 63 start 64 end 64 start 65 end 65 start 66 end 66 start 67 end 67 start 68 end 68 start 69 end 69 start 70 end 70 start 71 end 71 start 72 end 72 start 73 end 73 start 74 end 74 start 75 end 75 start 76 end 76 start 77 end 77 start 78 end 78 start 79 end 79 start 80 end 80 start 81 end 81 start 82 end 82 start 83 end 83 start 84 end 84 start 85 end 85 start 86 end 86 start 87 end 87 start 88 end 88 start 89 end 89 start 
90 end 90 start 91 end 91 start 92 end 92 start 93 end 93 start 94 end 94 start 95 end 95 start 96 end 96 start 97 end 97 start 98 end 98 start 99 end 
99 start 100 end 100
```
