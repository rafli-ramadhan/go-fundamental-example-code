# Redirect

Redirect merupakan pemindahan resource dari suatu alamat URL ke alamat baru. Untuk http status yang digunakan pada redirect bisa berupa:

* http.StatusMovedPermanently(301) -> resource yang di request telah dipindahkan ke url yang baru.
* http.StatusTemporaryRedirect(307) -> resource untuk sementara dipindahkan ke url lain.
* http.StatusPermanentRedirect(308) -> resource telah dipindahkan permanen ke url lain.

```go
package main

import (
	"fmt"
	"net/http"
)

func main() {
	mux := http.NewServeMux()
	mux.HandleFunc("/welcome", func(w http.ResponseWriter, r *http.Request) {
		http.Redirect(w, r, "https://www.google.com", http.StatusMovedPermanently)
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

```

<figure><img src="../../.gitbook/assets/redirect.png" alt=""><figcaption></figcaption></figure>
