# Download File

Download file digunakan untuk mendownload file dari suatu endpoint. File tersebut ditaruh didalam folder yang sama dengan aplikasi.

```go
package main

import (
	"fmt"
	"net/http"
)

func main() {
	mux := http.NewServeMux()
	mux.HandleFunc("/", download)

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

func download(w http.ResponseWriter, r *http.Request) {
	filename := r.URL.Query().Get("file")
	if filename == "" {
		w.WriteHeader(http.StatusBadRequest)
		w.Write([]byte("invalid requested file"))
	}

	w.Header().Add("content-disposition", fmt.Sprintf("attachment;filename=\"%s\"", filename))
	//w.Header().Add("content-disposition", "attachment;filename=\""+filename+"\"")
	http.ServeFile(w, r, "./files/txt/"+filename)
	w.Write([]byte("downloaded"))
}
```

<figure><img src="../../.gitbook/assets/folder file serve.png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/download native.png" alt=""><figcaption></figcaption></figure>
