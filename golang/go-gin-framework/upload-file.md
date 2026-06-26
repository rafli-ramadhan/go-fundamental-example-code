# Upload File

Upload file di gin dapat menggunakan method FormFile() untuk mendapatkan multipart file dari request dan SaveUploadFile() untuk menyimpan file di direktori yang diinginkan. Contohnya seperti _code_ di bawah ini yang digunakan untuk menyimpan gambar.

```go
package main

import (
	"fmt"
	"net/http"

	"github.com/gin-gonic/gin"
)

func main() {
	r := gin.Default()
	r.GET("/", Upload)
	r.Run(":5000")
}

func Upload(ctx *gin.Context) {
	file, _ := ctx.FormFile("picture")
	err := ctx.SaveUploadedFile(file, fmt.Sprintf("./files/%s", file.Filename))
	if err != nil {
		ctx.JSON(http.StatusBadRequest, gin.H{
			"status":  http.StatusOK,
			"message": err,
		})
		return
	}

	ctx.JSON(http.StatusOK, gin.H{
		"status":  http.StatusOK,
		"message": fmt.Sprintf("'%s' has been uploaded: ", file.Filename),
	})
}

```

<figure><img src="../../.gitbook/assets/1 (5) (1) (1).png" alt=""><figcaption></figcaption></figure>

## Upload lebih dari 1 file (.png dan .txt)

```go
package main

import (
	"fmt"
	"net/http"

	"github.com/gin-gonic/gin"
)

func main() {
	r := gin.Default()
	r.GET("/", Upload)
	r.Run(":5000")
}

func Upload(ctx *gin.Context) {
	file, _ := ctx.FormFile("picture")
	err := ctx.SaveUploadedFile(file, fmt.Sprintf("./files/%s", file.Filename))
	if err != nil {
		ctx.JSON(http.StatusBadRequest, gin.H{
			"status":  http.StatusOK,
			"message": err,
		})
		return
	}

	file2, _ := ctx.FormFile("txt")
	err = ctx.SaveUploadedFile(file2, fmt.Sprintf("./files/%s", file2.Filename))
	if err != nil {
		ctx.JSON(http.StatusBadRequest, gin.H{
			"status":  http.StatusOK,
			"message": err,
		})
		return
	}

	ctx.JSON(http.StatusOK, gin.H{
		"status":  http.StatusOK,
		"message": fmt.Sprintf("'%s' and '%s' has been uploaded: ", file.Filename, file2.Filename),
	})
}

```

<figure><img src="../../.gitbook/assets/1 (7) (1) (1).png" alt=""><figcaption></figcaption></figure>
