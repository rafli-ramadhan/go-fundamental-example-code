# Get dan Set Cookie

Untuk get cookie dari request di Gin dapat menggunakan method Cookie(), sementara untuk set cookie di response dapat menggunakan method SetCookie().

```go
package main

import (
	"fmt"
	"net/http"

	"github.com/gin-gonic/gin"
)

func main() {
	r := gin.Default()
	r.GET("/", TestCookie)
	r.Run(":5000")
}

func TestCookie(ctx *gin.Context) {
	// get cookie from request
	getCookie, err := ctx.Cookie("gin_cookie")
	if err != nil {
        	fmt.Println(err)
        }
	fmt.Println(getCookie)

	// set cookie in response (name string, value string, maxAge int, path string, domain string, secure bool, httpOnly bool)
	ctx.SetCookie("gin_cookie", "test", 3600, "/", "localhost", false, true)
	ctx.SetCookie("gin_cookie", "test2", 3600, "/", "localhost", false, true)
	
	// get cookie from response
	resCookie := ctx.Writer.Header().Get("set-cookie")
	fmt.Println(resCookie)

	ctx.JSON(200, gin.H{
		"status": http.StatusOK,
	})
}
```

<figure><img src="../../.gitbook/assets/response 2 (1).png" alt=""><figcaption></figcaption></figure>
