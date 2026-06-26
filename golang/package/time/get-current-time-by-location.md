# Get Current Time By Location

time.Time -> merupakan struct dan punya method&#x20;

| Method             | Return    |   |
| ------------------ | --------- | - |
| time.Now().Local() | time.Time |   |
| time.Now().Year()  | Int       |   |
| time.Now().Month() | Int       |   |
| time.Now().Day()   | Int       |   |

## Contoh _code_ untuk memperoleh waktu di lokasi saat ini

```go
package main

import (
    "fmt"
    "time"
)

func main() {
	// return current local time
    	now := time.Now()
    	fmt.Println(now)

	fmt.Println(now.Year())
	fmt.Println(now.Month())
	fmt.Println(now.Day())
	fmt.Println(now.Format("02/01/2006 03:04 PM"))
	fmt.Println(now.Format("03:04 PM"))
	fmt.Println(now.Format("15:04"))
}
```

```
PS D:\go-example> go run main.go
2023-05-28 16:28:45.0438233 +0700 +07 m=+0.003357401
2023
May
28
28/05/2023 04:28 PM
04:28 PM
16:28
```

## Contoh _code_ untuk memperoleh waktu di suatu lokasi

```go
package main

import (
    "fmt"
    "time"
)

func main() {
    	now := time.Now()
	loc, err := time.LoadLocation("Asia/Tokyo")
	if err != nil {
		panic(err)
	}
	fmt.Println(now.In(loc).Year())
	fmt.Println(now.In(loc).Month())
	fmt.Println(now.In(loc).Day())
	fmt.Println(now.In(loc).Format("02/01/2006 03:04 PM"))
	fmt.Println(now.In(loc).Format("03:04 PM"))
	fmt.Println(now.In(loc).Format("15:04"))
}
```

```
2023-05-28 16:35:44.6906019 +0700 +07 m=+0.003208701
2023
May
28
28/05/2023 06:35 PM
06:35 PM
18:35
```
