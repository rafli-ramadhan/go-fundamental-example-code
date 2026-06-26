# Context Background & TODO

Context background digunakan untuk membuat context kosong yang tidak pernah dibatalkan, tidak pernah time out dan tidak ada value apapun.

```
context.Background()
```

Sementara context TODO digunakan untuk membuat context kosong mirip dengan context background, namun context TODO digunakan saat belum jelas context apa yang ingin digunakan.

```
context.TODO()
```

```go
package main

import(
    "context"
    "fmt"
)

func main() {
    background := context.Background()
    fmt.Println(background)
    todo := context.TODO()
    fmt.Println(todo)
}
```

```
context.Background
context.TODO
```
