# Router

Untuk membuat router bisa menggunakan method sesuai HTTP Verb yang akan dipakai. Contoh untuk GET bisa menggunakan method GET seperti contoh code berikut.

## Contoh code router dengan HTTP method GET

```go
package main

import (
	"github.com/gin-gonic/gin"
)

func main() {
	r := gin.Default()

	r.GET("/welcome", welcome)
	r.Run(":5000")
}

func welcome(ctx *gin.Context) {
	ctx.Writer.Write([]byte("success"))
}
```

<figure><img src="../../.gitbook/assets/1 (2) (1) (1).png" alt=""><figcaption></figcaption></figure>

## Contoh code router dengan HTTP method GET, POST, PATCH dan DELETE

```go
package main

import (
	"net/http"
	"github.com/gin-gonic/gin"
)

func main() {
	r := gin.Default()
	r.GET("/", GetHandler)
	r.POST("/", GetHandler)
	r.PATCH("/", GetHandler)
	r.DELETE("/", GetHandler)
	r.Run(":5000")
}

func GetHandler(ctx *gin.Context) {
	if ctx.Request.Method == http.MethodGet {
		ctx.Writer.Write([]byte("test get"))
	} else if ctx.Request.Method == http.MethodPost {
		ctx.Writer.Write([]byte("test post"))
	} else if ctx.Request.Method == http.MethodPatch {
		ctx.Writer.Write([]byte("test patch"))
	} else if ctx.Request.Method == http.MethodDelete {
		ctx.Writer.Write([]byte("test delete"))
	}
}
```
