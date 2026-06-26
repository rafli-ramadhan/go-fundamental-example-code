---
description: Package "sync/atomic"
---

# Atomic

## Contoh code untuk store atomic value

```go
package main

import (
	"fmt"
	"sync/atomic"
)

type Person struct {
	name string
	age  int
}

func main() {
	var person atomic.Value
	person.Store(Person{name: "John", age: 30})
	fmt.Println("Initial Person:", person.Load())

	person.Store(Person{name: "Jane", age: 25})
	fmt.Println("New Person:", person.Load())
}
```

```
Initial Person: {John 30}
New Person: {Jane 25}
```

## Contoh code add, store dan load data dengan atomic

Pada code di bawah ini digunakan fungsi AddInt64, StoreInt64 dan LoadInt64 untuk add, store dan load data dengan tipe int64.

```go
package main

import (
    "fmt"
    "sync/atomic"
)

func main() {
    var num int64
    fmt.Println("Before:", num)

    atomic.AddInt64(&num, 5)
    fmt.Println("After:", num)
    
    atomic.StoreInt64(&num, 10)
    fmt.Println("After:", num)
    
    fmt.Println("Final Value:", atomic.LoadInt64(&num))
}

```

```
Before: 0
After: 5
After: 10
Final Value: 10
```

Fungsi-fungsi yang lebih lengkap pada package atomic dapat dilihat pada link berikut.&#x20;

{% embed url="https://pkg.go.dev/sync/atomic#LoadInt64" %}

Reference:

{% embed url="https://www.geeksforgeeks.org/atomic-addint64-function-in-golang-with-examples/" %}

