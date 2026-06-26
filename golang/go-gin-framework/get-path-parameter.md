# Get Path Parameter

Untuk get path parameter di Gin bisa menggunakan method Param() seperti _code_ dibawah ini.

```go
package main

import (
	"net/http"
	"github.com/gin-gonic/gin"
)

func main() {
	r := gin.Default()
	r.GET("/:id/:name", Get)
	r.Run(":5000")
}

func Get(ctx *gin.Context) {
	id := ctx.Param("id")
	name := ctx.Param("name")
	ctx.JSON(200, gin.H{
		"status": http.StatusOK,
		"data":   map[string]interface{}{
			"id": 	id,
			"name":	name,
		},
	})
}
```

<figure><img src="../../.gitbook/assets/1 (6) (1) (1).png" alt=""><figcaption></figcaption></figure>
