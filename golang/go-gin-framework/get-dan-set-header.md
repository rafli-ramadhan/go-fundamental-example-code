# Get dan Set Header

Untuk request header di Gin bisa menggunakan method GetHeader() dan untuk set header baru di response bisa menggunakan method Header(). Contohnya seperti _code_ dibawah ini.

```go
package main
import (
	"fmt"
	"net/http"
	"github.com/gin-gonic/gin"
)

func main() {
	r := gin.Default()
	r.GET("/", TestHeader)
	r.Run(":5000")
}

func TestHeader(ctx *gin.Context) {
	// Get header dari request
	testHeader := ctx.GetHeader("Content-Type")
	// Set new header in response
	ctx.Header("Content-Type", "application/xml")
	ctx.Header("Content-Type", "application/json")
	ctx.Header("Test", "test")
	// Get header from response
	getResHeader := ctx.Writer.Header().Get("Content-Type")
	fmt.Println(getResHeader)
	ctx.JSON(200, gin.H{
		"status": http.StatusOK,
		"header": testHeader,
	})
}
```

<figure><img src="../../.gitbook/assets/1 (3) (1) (1).png" alt=""><figcaption></figcaption></figure>
