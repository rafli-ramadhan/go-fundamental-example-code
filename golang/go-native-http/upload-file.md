# Upload File

Untuk meng-upload file melalui request dapat menggunakan code di bawah ini.

```go
package main

import (
	"fmt"
	"io"
	"net/http"
	"os"
)

func main() {
	mux := http.NewServeMux()
	mux.HandleFunc("/upload", func(w http.ResponseWriter, r *http.Request) {
		upload(w, r)
	})
	
	server := http.Server{
		Addr: 	"localhost:5000",
		Handler: mux,
	}

	fmt.Println("Server running on", server.Addr)
	err := server.ListenAndServe()
	if err != nil {
		panic(err)
	}
}

func upload(w http.ResponseWriter, r *http.Request) {
	file, fileHeader, err := r.FormFile("picture")
	if err != nil {
		w.WriteHeader(http.StatusInternalServerError)
		w.Write([]byte(err.Error()))
	}

	// untuk create file
	destinationFile, err := os.Create("./files/" + fileHeader.Filename)
	if err != nil {
		w.WriteHeader(http.StatusInternalServerError)
		w.Write([]byte(err.Error()))
	}

	// untuk meng-copy file ke ke direktori yang menerapkan io.Writer
	_, err = io.Copy(destinationFile, file)
	if err != nil {
		w.WriteHeader(http.StatusInternalServerError)
		w.Write([]byte(err.Error()))
	}

	w.Write([]byte(fileHeader.Filename + " has been uploaded"))
}
```

<figure><img src="../../.gitbook/assets/1 (5).png" alt=""><figcaption></figcaption></figure>

File bisa di cek di folder destinasi yaitu ./files.

<figure><img src="../../.gitbook/assets/1 (7) (1).png" alt=""><figcaption></figcaption></figure>
