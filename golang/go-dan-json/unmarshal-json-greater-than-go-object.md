# Unmarshal (JSON -> Go Object)

Unmarsal merupakan cara untuk mengubah JSON string menjadi golang object berupa map\[string]interface atau struct.

## Contoh _code_ decode dari JSON string menjadi struct

```go
package main

import (
    "encoding/json"
    "fmt"
)

type User struct {
    Name string `json:"Name"`
    Age  int
}

func main() {
    var jsonString = `{"Name": "john wick", "Age": 27, "Address": "Test"}`
    var jsonData = []byte(jsonString) // slice byte

    var user User
    // json -> struct
    var err = json.Unmarshal(jsonData, &user)
    if err != nil {
        fmt.Println(err.Error())
        return
    }

    fmt.Println(user)
    fmt.Println(user.Name)
    fmt.Println(user.Age)
}
```

```
{andri 21}
andri
21
```

## Contoh _code_ decode dari JSON string menjadi map

```go
package main

import (
    "encoding/json"
    "fmt"
)

func main() {
    var jsonString = `{"Name": "john wick", "Age": 27}`
    var jsonData = []byte(jsonString)

    var user map[string]interface{}
    // json -> struct
    var err = json.Unmarshal(jsonData, &user)
    if err != nil {
        fmt.Println(err.Error())
        return
    }

    fmt.Println(user)
}
```

```
map[Age:27 Name:john wick]
```
