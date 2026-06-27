# Kapan harus pakai Buffered Channel dibandingkan Channel

Kalau sender lebih cepat dari reciver dan ingin mengurangi blocking dengan menampung sementara data di buffer, tanpa harus menunggu penerima siap langsung.

Kalau receiver lebih cepat dari sender, lebih baik unbuffered channel.

**Apakah pengirim lebih cepat dari penerima?**

Contoh kasus, buffered channel terlalu kecil

```go
ch := make(chan int, 1)  // ❌ Terlalu kecil!
for i := 0; i < 1000; i++ {
    ch <- i  // Cepat penuh, malah blocking!
}
```

```go
ch := make(chan int, 1000)
for i := 0; i < 1000; i++ {
    ch <- i  // Cepat penuh, malah blocking!
}
```

Contoh implementasi Buffered Channel

```go
package main

import (
    "encoding/json"
    "fmt"
    "math/rand"
    "sync"
    "time"
)

type APIResponse struct {
    ID     int    `json:"id"`
    Data   string `json:"data"`
    Status string `json:"status"`
}

func main() {
    ch := make(chan APIResponse, 4)
    
    var wg sync.WaitGroup
    wg.Add(4)
    
    // Call 4 API concurrently
    for i := 1; i <= 4; i++ {
        go func(id int) {
            defer wg.Done()
            response := callAPI(id)
            ch <- response
        }(i)
    }
    
    wg.Wait()
    close(ch)
    
    responses := make([]APIResponse, 0, 4)
    for resp := range ch {
        responses = append(responses, resp)
    }
    
    finalJSON := mergeResponses(responses)
    publishToKafka(finalJSON)
    fmt.Println("Selesai!")
}

func callAPI(id int) APIResponse {
    // Simulasi response time random 1-5 detik
    delay := time.Duration(1+rand.Intn(5)) * time.Second
    time.Sleep(delay)
    
    return APIResponse{
        ID:     id,
        Data:   fmt.Sprintf("Data dari API %d", id),
        Status: "success",
    }
}

func mergeResponses(responses []APIResponse) []byte {
    result := map[string]interface{}{
        "timestamp": time.Now().Unix(),
        "data":      responses,
    }
    
    jsonData, _ := json.Marshal(result)
    return jsonData
}

func publishToKafka(data []byte) {
    fmt.Printf("Publish ke KAFKA: %s\n", string(data))
}
```

Apa yang terjadi jika channel penuh ? channel akan blocking sampai beberapa data di consume oleh buffer. Semisal 2 sender mengirimkan 2 data ke channel dalam 1 detik, hanya ada 1 worker consumer yang dapat memproses 1 data per detik, buffer channel 4, pada detik keberapa buffer channel penuh ? Detik ke 4

<figure><img src="../../.gitbook/assets/Screenshot 2026-06-27 at 22.59.05.png" alt=""><figcaption></figcaption></figure>

Setelah detik ke-empat, kondisi channel hanya akan menerima 1 data dari 1 sender, block data dari sender lainnya sampai ada 1 slot data lagi.

**Apa yang terjadi jika buffered channel diubah jadi unbuffered channel ?**

Pada unbuffered channel, sender BLOKIR pada saat itu juga (t=0), BUKAN menunggu sampai detik 1. Blocking, tapi tidak deadlock.

Unbuffered channel **tidak punya tempat penyimpanan**. Data harus **langsung dipindahkan** dari sender ke receiver. Jika receiver belum siap, sender akan **blocking** sampai receiver siap.

**Contoh Implementasi Code Call API**

```go
package main

import (
    "encoding/json"
    "fmt"
    "math/rand"
    "sync"
    "time"
)

type APIResponse struct {
    ID     int    `json:"id"`
    Data   string `json:"data"`
    Status string `json:"status"`
}

func main() {
    ch := make(chan APIResponse, 4)
    
    var wg sync.WaitGroup
    wg.Add(4)
    
    // Call 4 API concurrently
    for i := 1; i <= 4; i++ {
        go func(id int) {
            defer wg.Done()
            response := callAPI(id)
            ch <- response
        }(i)
    }
    
    wg.Wait()
    close(ch)
    
    responses := make([]APIResponse, 0, 4)
    for resp := range ch {
        responses = append(responses, resp)
    }
    
    finalJSON := mergeResponses(responses)
    publishToKafka(finalJSON)
    fmt.Println("Selesai!")
}

func callAPI(id int) APIResponse {
    // Simulasi response time random 1-5 detik
    delay := time.Duration(1+rand.Intn(5)) * time.Second
    time.Sleep(delay)
    
    return APIResponse{
        ID:     id,
        Data:   fmt.Sprintf("Data dari API %d", id),
        Status: "success",
    }
}

func mergeResponses(responses []APIResponse) []byte {
    result := map[string]interface{}{
        "timestamp": time.Now().Unix(),
        "data":      responses,
    }
    
    jsonData, _ := json.Marshal(result)
    return jsonData
}

func publishToKafka(data []byte) {
    fmt.Printf("Publish ke KAFKA: %s\n", string(data))
}
```

Scenario pakai unbuffered channel

```
API 1: selesai dalam 1 detik → ch <- response → ⚠️ BLOKIR! (nunggu diambil)
API 2: selesai dalam 2 detik → ch <- response → ⚠️ BLOKIR!
API 3: selesai dalam 3 detik → ch <- response → ⚠️ BLOKIR!
API 4: selesai dalam 5 detik → ch <- response → ⚠️ BLOKIR!

→ Resource terbuang percuma
```

Scenario pakai buffered channel

```
API 1: selesai dalam 1 detik → ch <- response ✅ LANGSUNG (buffer 1/4)
API 2: selesai dalam 2 detik → ch <- response ✅ LANGSUNG (buffer 2/4)
API 3: selesai dalam 3 detik → ch <- response ✅ LANGSUNG (buffer 3/4)
API 4: selesai dalam 5 detik → ch <- response ✅ LANGSUNG (buffer 4/4)

→ Resource efisien, CPU bisa dipakai goroutine lain
```

#### Skenario 1: Sender Cepat, Receiver Lambat

**Buffered (cap=5):**

text

```
Sender: 💨💨💨💨💨 → [1][2][3][4][5] → Receiver: 🐢
        (kirim 5 data tanpa blocking)     (proses 1 data/detik)
```

**Unbuffered:**

text

```
Sender: 💨 → [ ] → Receiver: 🐢
        ⚠️ BLOKIR! (setiap mau kirim)
```

**Hasil:** **Buffered LEBIH CEPAT** (sender gak blocking)

#### Skenario 2: Sender Lambat, Receiver Cepat

**Buffered (cap=5):**

text

```
Sender: 🐢 → [1][_][_][_][_] → Receiver: 💨
        (buffer nganggur)       (langsung ambil)
```

**Unbuffered:**

text

```
Sender: 🐢 → [ ] → Receiver: 💨
        (langsung transfer, receiver selalu siap)
```

**Hasil:** **SAMA CEPAT** (buffer gak berguna)

Skenario 3: Sender ≈ Receiver (Seimbang)

**Buffered (cap=5):**

text

```
Sender: ⚡ → [1][_][_][_][_] → Receiver: ⚡
        (buffer gak pernah penuh)
```

**Unbuffered:**

text

```
Sender: ⚡ → [ ] → Receiver: ⚡
        (transfer langsung, pas banget waktunya)
```

**Hasil:** **SAMA CEPAT** (atau unbuffered lebih cepat karena gak ada overhead buffer)
