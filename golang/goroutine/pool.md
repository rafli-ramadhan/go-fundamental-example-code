# Pool

Pool merupakan implementasi design pattern bernama _object pool pattern_. Design pattern pool dapat digunakan untuk menyimpan data. Data dapat diambil dari pool dengan menggunakan Get(). Setelah selesai menggunakan datanya, bisa disimpan kembali ke pool menggunakan Put(). Implementasi pool di Golang ini sudah aman dari problem _race condition_.

## Contoh _code_

```go
package main
 
import (
    "fmt"
    "sync"
    "time"
)

var pool sync.Pool

func main() {
    var v int
    pool.Put(v)
    pool.Put(2)
    pool.Put(3)
    pool.Put(4)
    pool.Put(5)
    pool.Put(6)
    pool.Put(7)
    pool.Put(8)
    pool.Put(9)
    pool.Put(10)

    for i := 0; i < 10; i++ {
        data := pool.Get()
        fmt.Printf("%d ", data)
    }

    time.Sleep(3 * time.Millisecond)    
}
```

```
0 10 9 8 7 6 5 4 3 2
```

```go
package main
import (
    "fmt"
    "sync"
)

var pool sync.Pool
func main() {
    pool.Put(1)
    pool.Put(2)
    pool.Put(3)
    fmt.Println(pool.Get())
    fmt.Println(pool.Get())
    fmt.Println(pool.Get())
}
```

```
1
3
2
```

```go
package main

import (
	"fmt"
	"sync"
)

type Person struct {
	Name string
	Age  int
}

var pool = sync.Pool{
	New: func() interface{} {
		return &Person{}
	},
}

func main() {
	person := pool.Get().(*Person)
	person.Name = "John"
	person.Age = 30
	fmt.Println(*person)

	pool.Put(person)

	person = pool.Get().(*Person)
	fmt.Println(*person)
}

```

```
{John 30}
{John 30}
```

```go
package main

import (
	"fmt"
	"sync"
)

type Person struct {
	Name string
	Age  int
}

var pool = sync.Pool{
	New: func() interface{} {
		return Person{}
	},
}

func main() {
	person := pool.Get().(Person)
	person.Name = "John"
	person.Age = 30
	fmt.Println(person)

	pool.Put(person)

	person = pool.Get().(Person)
	fmt.Println(person)
}

```

```
{John 30}
{John 30}
```
