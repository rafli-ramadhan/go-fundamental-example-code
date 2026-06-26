# Function vs Method

Method ada kepemilikan. Contohnya :

```go
type test int

// function
func Calculate() {}

// method
func (t test) Calculate() {}
```

## Contoh _code_ method

```go
package main

import "fmt"

type rect struct {
	width, height int
}

func (r rect) area() int {
	return r.width * r.height
}

func (r rect) perimeter() int {
	return 2 * (r.width + r.height)
}

func main() {
	r := rect{width: 10, height: 5}
	fmt.Println("area     : ", r.area())
	fmt.Println("perimeter: ", r.perimeter())
}

```

```
area     :  50
perimeter:  30
```

Reference:

{% embed url="https://www.geeksforgeeks.org/methods-in-golang/" %}
