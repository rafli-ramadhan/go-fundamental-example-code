# Function Init dan Main

Di golang function main dieksekusi saat perintah `go run` di jalankan. Sementara function Init tidak menerima parameter atau me-return suatu value. Baik ada atau tidak ada function main, function init akan selalu dijalankan saat `go run` . Jika ada beberapa package yang saling import dan setiap package terdapat function init, maka function init dari package terdalam yang akan dijalankan terlebih dahulu baru dilanjut function main dari package main.

<figure><img src="../../../.gitbook/assets/init.png" alt=""><figcaption><p>Sumber gambar : <a href="https://stackoverflow.com/questions/24790175/when-is-the-init-function-run">https://stackoverflow.com/questions/24790175/when-is-the-init-function-run</a></p></figcaption></figure>

## Contoh code

```go
package main

import "fmt"

var WhatIsThe = 5

func init() {
	WhatIsThe = 0
	fmt.Println("init")
}

func main() {
	if WhatIsThe == 0 {
		fmt.Println(0)
	}
	fmt.Println("main")
}
```

```
init
0
main
```

Reference:

{% embed url="https://stackoverflow.com/questions/24790175/when-is-the-init-function-run" %}
