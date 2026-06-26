# Serve File

Untuk menampilkan suatu file semisal html atau png, disarankan menggunakan method StaticFile. Bisa juga menggunakan StaticFS atau Static. Keduanya sama karena di dalam method Static terdapat method StaticFS.

```go
package main

import (
	"net/http"

	"github.com/gin-gonic/gin"
)

func main() {
	r := gin.Default()

	r.StaticFS("/html", http.Dir("./files"))
	r.StaticFS("/pic", http.Dir("./files"))

	r.Static("/html2", "./files")
	r.Static("/pic2", "./files")

	r.StaticFile("/html3", "./files/index.html")
    	r.StaticFile("/pic3", "./files/1.png")

	r.Run(":5000")
}
```
