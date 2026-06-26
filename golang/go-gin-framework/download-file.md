# Download File

Untuk download file otomatis saat hit suatu endpoint, bisa menggunakan ctx.Header("content-disposition", ...) dan ctx.File() untuk menampilkan file saat endpoint di hit di browser. Tanpa header tersebut, file hanya akan ditampilkan saja dan tidak terdownload. Content-disposition adalah tipe header untuk menunjukkan bagaimana response diproses. Content-disposition di set attachment yang akan membuat browser men-dowload file otomatis. Contoh _code_ seperti di bawah ini.

```go
package main

import (
	"fmt"
	"net/http"

	"github.com/gin-gonic/gin"
)

func main() {
	r := gin.Default()
	r.GET("/download", Download)
	r.Run(":5000")
}

func Download(ctx *gin.Context) {
	filename, _ := ctx.GetQuery("file")
	if filename == "" {
		ctx.String(http.StatusBadRequest, "invalid requested file")
	}

	ctx.Header("content-disposition", "attachment;filename=\""+filename+"\"")
	ctx.File(fmt.Sprintf("./files/%s", filename))

	ctx.String(http.StatusOK, "Downloaded")
}
```

<figure><img src="../../.gitbook/assets/download (1).png" alt=""><figcaption></figcaption></figure>

Reference :

{% embed url="https://www.geeksforgeeks.org/http-headers-content-disposition/" %}
