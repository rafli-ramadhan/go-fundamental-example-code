# Map

Map di Golang memiliki pola seperti array atau slice yang menyimpan beberapa data dengan tipe data yang sama dengan pasangan key dan value. Sebelum digunakan, map perlu di inisiasi sebagai berikut.

```go
var example map[string]int = map[string]int{}
```

atau bisa menggunakan fungsi make() sebagai berikut.

```go
var example map[string]int = make(map[string]int)
```

## Contoh code map string interface

Map string interface bisa digunakan untuk menampung key dengan tipe data string dan value dengan tipe data apapun. Map jenis ini sangat berguna untuk encoding dan decoding JSON pada saat membuat REST API.

```go
package main
import "fmt"

func main() {
    var someMap map[string]interface{}
    
    someMap = map[string]interface{}{
        "username"  : "test",
        "age"       : 20,
    }
    
    fmt.Println(someMap)
}
```

```
map[age:20 username:test]
```

## Contoh code map string dengan value map string interface

Map juga bisa diisi dengan value yang juga merupakan map seperti _code_ di bawah ini.

```go
package main
import "fmt"

func main() {
    var someMap map[string]map[string]interface{}
    var someSubMap map[string]interface{} = map[string]interface{}{
        "username"  : "dana",
        "age"       : 24,
    }

    someMap = map[string]map[string]interface{}{
        "map1"  : someSubMap,
        "map2"  : someSubMap,
    }
    
    fmt.Println(someMap["map1"])
    fmt.Println(someMap["map2"])
    fmt.Println(someMap["map1"]["username"])
}
```

```
map[age:24 username:dana]
map[age:24 username:dana]
dana
```

## Contoh code map dengan key dan value beragam tipe data

Dari code dibawah ini, key dari map bisa berupa tipe data primitif (numeric, string, boolean), tipe data aggregate (array dan struct), dan tipe data reference khusus function dan channel. Key tidak bisa bertipe data map atau slice. Sementara value dari key bisa tipe data apapun termasuk map dan slice.

```go
package main

import "fmt"

func test() int {
	return 1
}

func main() {
	var someChan = make(chan int)
	type user struct {
		name string
		age  int
	}
	// someSubMap := map[string]int{
	// 	"a": 1,
	// 	"b": 2,
	// }
	someMap := map[interface{}]interface{}{
		1:               true,
		"username":      "member_01",
		false:           2,
		0.9:             []int{1, 2, 3, 4, 5},
		0.9+5i:			"test complex",
		user{"umar", 2}: user{"utsman", 1},
		[3]int{1, 2, 3}: "array",
		// panic: runtime error: hash of unhashable type []int
		// []int{1,2,3}		: "slice",
		// panic: runtime error: hash of unhashable type map[string]int
		// someSubMap		: "submap",

		test():   "function",
		someChan: "channel",
	}

	fmt.Println(someMap[user{"umar", 2}])
	fmt.Println(someMap[[3]int{1, 2, 3}])
	fmt.Println(someMap[0.9+5i])
	fmt.Println(someMap[test()])
	fmt.Println(someMap[someChan])
}

```

```
{utsman 1}
array
test complex
function
channel
```

## Add, Update dan Delete Value di Map Int Interface

```go
package main

import "fmt"

func main() {
    m := map[int]interface{}{
		1: "member_01",
		2: "member_02",
	}
	// add value by key
	m[3] = "member_003"
    
	// update value by key
	_, exist := m[3]
	if exist {
		m[3] = "member_03"
	}

	fmt.Println(m)
	
	delete(m, 3)
	fmt.Println(m)
}
```

```
map[1:member_01 2:member_02 3:member_03]
map[1:member_01 2:member_02]
```

## Add, Update dan Delete Value di Map Struct Interface

```go
package main

import "fmt"

func main() {
	type user struct {
		name string
		age  int
	}
	user1 := user{name: "member_01", age: 1}
	user2 := user{name: "member_02", age: 2}
	m := map[user]interface{}{
		user1: "member_01",
		user2: "member_02",
	}
	// add value by key
	m[user{name: "member_03", age: 3}] = "member_003"

	// update value by key
	_, exist := m[user{name: "member_03", age: 3}]
	if exist {
		m[user{"member_03", 3}] = "member_03"
	}

	fmt.Println(m)

	delete(m, user{"member_03", 3})
	fmt.Println(m)
}

```

```
map[{member_01 1}:member_01 {member_02 2}:member_02 {member_03 3}:member_03]
map[{member_01 1}:member_01 {member_02 2}:member_02]
```

## Challenge

1. Buatlah map dengan key nama orang dan valuenya macam-macam hobi maksimal 3, dengan ketentuan berikut:&#x20;

a. Buat map dengan function make&#x20;

b. Isi map dengan 10 data&#x20;

c. Cetak dengan fungsi printf. Contoh: “nama saya umar mempunya hobi gaming, hiking, dan fishing”

### Jawaban

```go
package main

import (
	"fmt"
)

func main() {
    type hobbies []string
    
    var users map[string]hobbies = make(map[string]hobbies)
    users["Adni"]   = []string{"Golf"}
    users["Faras"]  = []string{"Basketball", "Diving", "Gold"}
    users["Dawam"]  = []string{"Diving", "Scating"}
    users["Rizky"]  = []string{"Golf"}
    users["Alfi"]   = []string{"Basketball", "Diving", "Gold"}
    users["Jason"]  = []string{"Diving"}
    users["Mega"]   = []string{"Golf", "Scating"}
    users["Albert"] = []string{"Basketball", "Diving", "Gold"}
    users["Fajar"]  = []string{"Diving"}
    users["Dito"]   = []string{"Golf"}
    
    for i := range users {
        var hobi string
        if len(users[i]) == 1 {
            hobi = fmt.Sprintf("%s", users[i][0])
        } else if len(users[i]) == 2 {
            hobi = fmt.Sprintf("%s dan %s", users[i][0], users[i][1])
        } else if len(users[i]) == 3 {
            hobi = fmt.Sprintf("%s, %s, dan %s", users[i][0], users[i][1], users[i][2])
        }
    
        fmt.Printf("\nNama saya %s mempunyai hobi %s", i, hobi)
    }
}
```

```
Nama saya Jason mempunyai hobi Diving
Nama saya Albert mempunyai hobi Basketball, Diving, dan Gold
Nama saya Dito mempunyai hobi Golf
Nama saya Adni mempunyai hobi Golf
Nama saya Faras mempunyai hobi Basketball, Diving, dan Gold
Nama saya Alfi mempunyai hobi Basketball, Diving, dan Gold
Nama saya Fajar mempunyai hobi Diving
Nama saya Dawam mempunyai hobi Diving dan Scating
Nama saya Rizky mempunyai hobi Golf
Nama saya Mega mempunyai hobi Golf dan Scating
```
