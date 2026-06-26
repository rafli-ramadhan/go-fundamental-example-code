---
coverY: 0
---

# Logging

Logging digunakan untuk mencatat aktivitas yang terjadi di server. Contohnya saat suatu endpoint di hit, dapat ditampilkan logging request dari client.

Jenis-jenis logging di Golang berdasarkan kepopulerannya di Github:

1. **Logrus**

{% embed url="https://github.com/sirupsen/logrus" %}

2. **Zap**

{% embed url="https://github.com/uber-go/zap" %}

3. **ZeroLog**

{% embed url="https://github.com/rs/zerolog" %}

Golang juga memiliki bawaan package log sendiri bernama "log". Perbedaan log dan fmt yaitu log dapat menampilkan waktu suatu kode dieksekusi. Perlu diperhatikan juga bahwa log digunakan untuk logging, sementara fmt untuk formatting. Selain itu, jika dilihat dari code log(...) memang di program untuk dapat menghindari race condition.

## Contoh code

Berikut adalah contoh code logging menggunakan zerolog.

```go
package main

import (
	"fmt"

	"github.com/rs/zerolog"
	"github.com/rs/zerolog/log"
)

func main() {
    zerolog.TimeFieldFormat = zerolog.TimeFormatUnix

    log.Debug().
        Str("Scale", "833 cents").
        Float64("Interval", 833.09).
		Bool("IsSuccess", true).
		Any("Some Interface", "example").
		AnErr("Error", fmt.Errorf("some error")).
        Msg("Fibonacci is everywhere")
    
    log.Debug().
        Str("Name", "Tom").
        Send()
}
```

```bash
{"level":"debug","Scale":"833 cents","Interval":833.09,"time":1562212768,"message":"Fibonacci is everywhere"}
{"level":"debug","Name":"Tom","time":1562212768}
```

Reference :

{% embed url="https://stackoverflow.com/questions/19646889/why-should-i-use-log-println-instead-of-fmt-println" %}
