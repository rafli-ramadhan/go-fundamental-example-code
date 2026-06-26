# Pointer pada Method

Pointer dapat digunakan di method jika ingin mengubah nilai dari variabel yang memiliki method tersebut secara permanen.

## Contoh code pointer pada method sebuah string

```go
package main
import "fmt"

type str string

func (s *str) Update1() {
	*s = "member_02"
}

func (s str) Update2() {
	s = "member_03"
}

func main() {
	var name str = "member_01"
	name.Update1()
	name.Update2()
	fmt.Println(name)
}


```

```
member_02
```

## Contoh code pointer pada method sebuah struct

```go
package main

import (
    "fmt"
)

type Man struct{
    Name string
}

func (m *Man) Test1() {
    m.Name = "member_02"
    fmt.Println(*m)
}

func (m Man) Test2() {
    m.Name = "member_03"
    fmt.Println(m)
}

func (m Man) Test3() {
    fmt.Println(m)
}

func main() {
    member_01 := Man{"member_01"}
    fmt.Println(member_01)
    member_01.Test1()
    member_01.Test2()
    member_01.Test3()
    
    fmt.Println(member_01)
}
```

```
{member_01}
{member_02}
{member_03}
{member_02}
{member_02}
```
