# Unmarshal vs Marshal

Di golang untuk mengubah suatu tipe data golang ke JSON dapat menggunakan fungsi Marshal, sementara untuk mengubah JSON ke suatu tipe data golang dapat menggunakan fungsi Unmarshal. Keduanya bisa digunakan untuk mengubah nilai dengan tipe data int, float?, string, bool, slice, struct, map dan interface ? menjadi JSON dan sebaliknya.

```
func Unmarshal(data []byte, v interface{}) error
```

```
func Marshal(v interface{}) ([]byte, error)
```

## Contoh _code_ marshal (int-> JSON) & unmarshal (JSON -> int)

```go
package main

import (
    "encoding/json"
    "fmt"
)

func main() {
    jsonData, _ := json.Marshal(123)
    fmt.Println(string(jsonData))
}
```

```
123 // -> JSON
```

```go
package main

import (
    "encoding/json"
    "fmt"
)

func main() {
    var jsonString = `2`
    var jsonData = []byte(jsonString)

    var data int

    var err = json.Unmarshal(jsonData, &data)
    if err != nil {
        fmt.Println(err.Error())
        return
    }

    fmt.Println(data)
}
```

```
123
```

## Contoh _code_ marshal (string-> JSON) & unmarshal (JSON -> string)

```go
package main

import (
    "encoding/json"
    "fmt"
)

func main() {
    jsonData, _ := json.Marshal("test")
    fmt.Println(string(jsonData))
}
```

```
"test" // -> JSON
```

```go
package main

import (
    "encoding/json"
    "fmt"
)

func main() {
    var jsonString = `"test"`
    var jsonData = []byte(jsonString)

    var data string

    var err = json.Unmarshal(jsonData, &data)
    if err != nil {
        fmt.Println(err.Error())
        return
    }

    fmt.Println(data)
}
```

```
test
```

## Contoh _code_ marshal (boolean-> JSON) & unmarshal (JSON -> boolean)

```go
package main

import (
    "encoding/json"
    "fmt"
)

func main() {
    jsonData, _ := json.Marshal(true)
    fmt.Println(string(jsonData))
}
```

```
true
```

```go
package main

import (
    "encoding/json"
    "fmt"
)

func main() {
    var jsonString = `true`
    var jsonData = []byte(jsonString)

    var data bool
    // json -> struct
    var err = json.Unmarshal(jsonData, &data)
    if err != nil {
        fmt.Println(err.Error())
        return
    }

    fmt.Println(data)
}
```

```
true
```

## Contoh _code_ marshal (slice -> JSON) & unmarshal (JSON -> slice)

```go
package main

import (
    "encoding/json"
    "fmt"
)

func main() {
    jsonData, _ := json.Marshal([]string{"test 1", "test 2", "test 3"})
    fmt.Println(string(jsonData))
}
```

```
["test 1","test 2","test 3"] // -> JSON
```

```go
package main

import (
    "encoding/json"
    "fmt"
)

func main() {
    var jsonString = `["test 1", "test 2", "test 3"]`
    var jsonData = []byte(jsonString)

    var data []string
    // json -> struct
    var err = json.Unmarshal(jsonData, &data)
    if err != nil {
        fmt.Println(err.Error())
        return
    }

    fmt.Println(data)
}
```

```
[test 1 test 2 test 3]
```
