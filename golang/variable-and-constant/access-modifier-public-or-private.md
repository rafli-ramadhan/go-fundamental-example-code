# Access Modifier (Public or Private)

Access modifier digunakan untuk memperbolehkan suatu variabel atau function diakses di package lain. Untuk bisa diakses di package lain, nama variabel atau function perlu diawali huruf kapital.

```go
package main

import (
    "fmt"
)

// public variable -> bisa diakses di package lain
var ErrInvalid   string = "invalid"
const StatusTrue bool   = true

// private variable -> tidak bisa diakses di package lain
var errInvalid   string = "invalid"
const statusTrue bool   = true

// public function -> bisa diakses di package lain
func Calculate() {}

// private function -> tidak bisa diakses di package lain
func calculate() {}
```
