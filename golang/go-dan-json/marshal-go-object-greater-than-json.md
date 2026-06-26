# Marshal (Go Object -> JSON)

Marshal merupakan cara untuk mengubah object dalam Golang menjadi JSON string. Object tersebut dapat berupa map\[string]interface atau struct.

## Contoh _code_ marshal dari struct menjadi JSON object

```go
package main

import (
    "encoding/json"
    "fmt"
)

type User struct {
    Name string
    Age  int
}

func main() {
    users := []User{
        {"andi", 21}, 
        {"andre", 20},
    }
    
    var bytes, err = json.Marshal(users)
    if err != nil {
        fmt.Println(err.Error())
        return
    }
    
    var jsonObject = string(bytes)
    fmt.Println(jsonObject)
}
```

```
[{"Name":"andi","Age":21},{"Name":"andre","Age":20}]
```

## Contoh _code_ marshal dari map menjadi JSON object

```go
package main

import (
    "encoding/json"
    "fmt"
)

func main() {
    users := map[string]interface{}{
        "name":     "andi", 
        "age":      21, 
        "":         "empty",
        "test_nil": nil,
    }

    var bytes, err = json.Marshal(users)
    if err != nil {
        fmt.Println(err.Error())
        return
    }
    
    var jsonObject = string(bytes)
    fmt.Println(jsonObject)
}
```

```
{"":"empty","age":21,"name":"andi","test_nil":null}
```
