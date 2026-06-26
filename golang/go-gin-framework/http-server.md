# HTTP Server

Untuk membuat server di gin bisa menggunakan method Run() seperti code berikut.

```go
package main

import (
	"github.com/gin-gonic/gin"
)

func main() {
	r := gin.Default()

	r.Run(":5000")
}

```
