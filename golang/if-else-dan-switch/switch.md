# Switch

Switch merupakan salah satu bentuk percabangan di golang. Switch memiliki sekitar 5 bentuk seperti yang tertera dibawah ini.

## 1. Switch dengan Single Case Value

Switch jenis ini hanya memiliki satu value untuk setiap case. Nama variabel setelah switch bisa diberi atau tidak diberi kurung (...).

```go
package main

import (
    "fmt"
)

func choose(value int) {
	switch value {
	case 1:
		fmt.Println(1)
	case 2:
		fmt.Println(2)
	case 3:
		fmt.Println(3)
	}
}

func main() {
	choose(1)
	choose(2)
}
```

```
1
2
```

## 2. Switch Case dengan fallthrough

Statement fallthrough digunakan untuk menampilkan case yang terpenuhi value-nya dan case setelahnya.

```go
package main
import "fmt"

func main() {
  dayOfWeek := 5

  switch dayOfWeek {
    case 1:
      fmt.Println("Sunday")
      fallthrough
    case 2:
      fmt.Println("Monday")
      fallthrough
    case 3:
      fmt.Println("Tuesday")
      fallthrough
    case 4:
      fmt.Println("Wednesday")
      fallthrough
    case 5:
      fmt.Println("Thursday")
      fallthrough
    case 6:
      fmt.Println("Friday")
      fallthrough
    case 7:
      fmt.Println("Saturday")
      fallthrough
    default:
      fmt.Println("Invalid day")
      // fallthrough // -> cannot fallthrough final case in switch
  }
}
```

```
Thursday
Friday
Saturday
Invalid day
```

## 3. Switch dengan Multiple Case

Switch jenis ini memiliki beberapa value untuk setiap case-nya.

```go
package main
import "fmt"

func main() {
    day := "Monday"
    
    switch day {
    case "Monday", "Tuesday", "Wednesday", "Thursday", "Friday":
        fmt.Println("Work Day")
    case "Saturday", "Sunday":
        fmt.Println("Weekend")
    }
}
```

```
Work Day
```

## 4. Switch tanpa Expression

Switch jenis ini bisa digunakan dengan relational operator (>, <, >=, <=, ==, &&, atau !=).

```go
package main
import "fmt"

func main() {
    day := "Monday"
    
    switch {
    case day == "Monday" || day == "Tuesday" || day == "Wednesday" || day == "Thursday" || day == "Friday":
        fmt.Println("Work Day")
    case day == "Saturday" || day == "Sunday":
        fmt.Println("Weekend")
    }
}
```

```
Work Day
```

```go
package main

import "fmt"

func main() {
  var isValid bool = true

  switch {
    case isValid:
      fmt.Println("true")
     default:
      fmt.Println("false")
  }
}
```

```
true
```

```go
package main

import "fmt"

func main() {
  numOfDays := 28

  switch {
    case numOfDays == 28:
      fmt.Println("It's February")
    default:
      fmt.Println("Not February")
  }
}
```

```
It's February
```

## 5. Switch dengan Optional Statement

Deklarasi variabel pada switch jenis ini terletak setelah statement switch.

```go
package main

import "fmt"

func main() {
    switch  day := "Monday"; day {
    case "Monday", "Tuesday", "Wednesday", "Thursday", "Friday":
        fmt.Println("Work Day")
    case "Saturday", "Sunday":
        fmt.Println("Weekend")
    }
}
```

```
Work Day
```

```go
package main

import "fmt"

func main() {
  switch isValid := false; isValid {
    case isValid:
      fmt.Println("true")
     default:
      fmt.Println("false")
  }
}
```

```
true
```

```go
package main

import "fmt"

func main() {
  switch numOfDays := 28; numOfDays {
    case 28:
      fmt.Println("It's February")
    default:
      fmt.Println("Not February")
  }
}
```

```
It's February
```

## 6. Type Switch

Type switch digunakan untuk memperoleh tipe data dari suatu nilai dalam interface kosong. Type switch memiliki format seperti di bawah ini. Banyaknya case dapat disesuaikan sesuai kebutuhan.

```go
switch v := i.(type) {
case int:
    // program
case string:
    // program
case float64:
    // program
case bool:
    // program
case []string:
    // program
default:
    // program
}
```

### Contoh code

```go
package main

import "fmt"

func main() {
    var user any = []string{"member_01", "member_02", "member_03"}
    arr := user.([]string)

    switch result := user.(type) {
    case string:
        fmt.Printf("String", result)
    case int:
        fmt.Printf("Integer", result)
    case []string:
        for _, v := range arr { // cannot range over user (variable of type any)
            fmt.Print(v)
        }
    }
}
```

```
member_01
member_02
member_03
```

Reference:

{% embed url="https://www.programiz.com/golang/switch" %}

{% embed url="https://www.digitalocean.com/community/tutorials/how-to-write-switch-statements-in-go" %}

{% embed url="https://go.dev/tour/methods/16" %}
