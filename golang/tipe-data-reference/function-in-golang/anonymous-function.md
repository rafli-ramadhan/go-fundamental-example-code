# Anonymous Function

Anonymous function hampir mirip function biasa, bedanya anonymous function bisa secara langsung di inisiasi ke suatu variabel.

## Contoh _code_ : anonymous function sebagai variabel

```go
package main

import (
	"fmt"
)

type Filter func(name string) string

func sayHelloWithFilter(name string, filter Filter) {
	nameFiltered := filter(name)
	fmt.Println("Hello", nameFiltered)
}
	
func main() {
	// anonymous function as variable
	filter := func(name string) string {
		if name == "Kucing" {
			return ""
		} else {
			return name
		}
	}
	sayHelloWithFilter("Umar", filter)
	sayHelloWithFilter("Andi", filter)
}
	
```

```
Hello Umar
Hello Andi
```

```go
package main

import "fmt"

var (
	rectangle = func(p, l int) int {
		return p * l
	}
	triangle = func(a, t int) int {
		return a * t / 2
	}
)

func main() {
	fmt.Println(rectangle(20, 30))
	fmt.Println(triangle(20, 30))
}
```

```
600
300
```

## Contoh _code_ 2 : anonymous function sebagai parameter

```go
package main

import (
	"fmt"
)

type Filter func(name string) string

func sayHelloWithFilter(name string, filter Filter) {
	nameFiltered := filter(name)
	fmt.Println("Hello", nameFiltered)
}
	
func main() {
	// anonymous function as parameter
	sayHelloWithFilter("Umar", func(name string) string {
		if name == "Kucing" {
			return ""
		} else {
			return name
		}
	})
	sayHelloWithFilter("Andi", func(name string) string {
		if name == "Kucing" {
			return ""
		} else {
			return name
		}
	})
}
	
```

```
Hello Umar
Hello Andi
```
