# RW Mutex vs Mutex

RW Mutex -> Digunakan untuk supaya beberapa function dapat membaca data yang sama secara bersamaan.

## Mutex Only

```go
package main
 
import (
    "fmt"
    "sync"
)

var (
	wg sync.WaitGroup
	m sync.Mutex
	rw sync.RWMutex
	v int = 0
)
 
func main() {
    for i := 1; i <= 10; i++ {
		fmt.Printf("\nITERASI-%d\n", i)
		wg.Add(2)

		go func() {
			m.Lock()
			fmt.Println("Write lock")
			v++
			fmt.Println("Write unlock")
			m.Unlock()
			wg.Done()
		}()

		go func() {
			m.Lock()
			fmt.Println("Read lock")
			fmt.Println(v)
			fmt.Println("Read unlock")
			m.Unlock()
			wg.Done()
		}()
    }
    
    wg.Wait()
    fmt.Println("\nFinished", v)
}
```

```
ITERASI-1

ITERASI-2

ITERASI-3

ITERASI-4

ITERASI-5

ITERASI-6
Write lock
Write unlock
Read lock
1
Read unlock
Write lock
Write unlock
Read lock
2
Read unlock
Write lock
Write unlock
Read lock
3
Read unlock
Write lock
Write unlock
Read lock
4
Read unlock
Write lock
Write unlock
Read lock
5
Read unlock
Read lock
5
Read unlock
Write lock
Write unlock

ITERASI-7

ITERASI-8

ITERASI-9

ITERASI-10
Write lock
Write unlock
Read lock
7
Read unlock
Read lock
7
Read unlock
Write lock
Write unlock
Write lock
Write unlock
Read lock
9
Read unlock
Read lock
9
Read unlock
Write lock
Write unlock

Finished 10
```

## RW Mutex

```go
package main
 
import (
    "fmt"
    "sync"
)

var (
	wg sync.WaitGroup
	m sync.Mutex
	rw sync.RWMutex
	v int = 0
)
 
func main() {
    for i := 1; i <= 10; i++ {
		fmt.Printf("\nITERASI-%d\n", i)
		wg.Add(2)

		go func() {
			m.Lock()
			fmt.Println("Write lock")
			v++
			fmt.Println("Write unlock")
			m.Unlock()
			wg.Done()
		}()

		go func() {
			rw.RLock()
			fmt.Println("Read lock")
			fmt.Println(v)
			fmt.Println("Read unlock")
			rw.RUnlock()
			wg.Done()
		}()
    }
    
    wg.Wait()
    fmt.Println("\nFinished", v)
}
```

```
ITERASI-1

ITERASI-2
Write lock
Write unlock
Write lock
Write unlock
Read lock

ITERASI-3
Read lock
2
Read unlock
Read lock
Write lock
Write unlock

ITERASI-4

ITERASI-5
2
Read unlock
Write lock
Write unlock
Write lock
Write unlock
2
Read unlock

ITERASI-6

ITERASI-7

ITERASI-8
Read lock
5
Read unlock
Read lock
Read lock
5
Read unlock
Write lock
Write unlock
Write lock
Write unlock
Write lock
Write unlock
5
Read unlock
Read lock
8
Read unlock
Read lock
8
Read unlock

ITERASI-9

ITERASI-10
Write lock
Read lock
9
Read unlock
Read lock
9
Read unlock
Write unlock
Write lock
Write unlock

Finished 10
```
