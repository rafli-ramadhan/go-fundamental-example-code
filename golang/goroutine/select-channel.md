# Select Channel

Penerapan select pada channel.

```go
package main

import (
	"fmt"
)

func g(ch chan int, num int) {
	ch <- num
}

func main() {
	ch1 := make(chan int)
	ch2 := make(chan int)

	go g(ch1, 5)
	go g(ch2, 3)

	select {
	case <-ch1:
		fmt.Println("Test1")
	case <-ch2:
		fmt.Println("Test2")
	default:
		fmt.Println("The default case!")
	}
}

```

```go
package main

import (
    "errors"
    "fmt"
    "sync"
)

var wg sync.WaitGroup

func main() {
    	success := make(chan bool, 1)
	errCh := make(chan error, 1)

    	wg.Add(1)

	go func() {
		defer wg.Done()
		err := errors.New("there is an error")
		errCh <- err
	}()

	wg.Wait()
    	success <- true

	select {
	case err := <-errCh:
		fmt.Println(err)
	case <- success:
		fmt.Println("success")
	}
}
```

```
D:\go-server>go run .
error there is an error

D:\go-server>go run .
success

D:\go-server>go run .
success

D:\go-server>go run .
there is an error
```

```go
package main

import "fmt"

func channelNum(num chan int) {
	// channel in
	num <- 15
}

func channelStr(str chan string) {
	// channel in
	str <- "Test"
}

func main() {
	num := make(chan int)
	str := make(chan string)

	go channelNum(num)
	go channelStr(str)

	// channel out
	select {
	case number := <- num:
		fmt.Println(number)
	case text := <- str:
		fmt.Println(text)
	}
}
```

```
D:\go-server>go run .
Test

D:\go-server>go run .
Test

D:\go-server>go run .
15

D:\go-server>go run .
Test

D:\go-server>go run .
Test

D:\go-server>go run .
15
```
