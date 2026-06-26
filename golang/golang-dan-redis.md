---
description: https://redis.io/
coverY: 0
---

# Golang dan Redis

Redis bisa digunakan untuk caching dan message broker. Cache digunakan untuk menyimpan informasi yang sifatnya sementara.

## Installasi Redis melalui Docker

Untuk meng-install Redis di local komputer, pastikan sudah meng-install docker terlebih dahulu. Pertama jalankan docker, lalu install redis melalui CMD dengan command berikut.

```
docker pull redis
```

Untuk pengguna docker dekstop dapat install Redis dengan cara search Redis Image di bagian search docker, lalu klik pull. Begitu installasi selesai, image akan langsung muncul di Tab Image.

<figure><img src="../.gitbook/assets/redis (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/Redis 2.png" alt=""><figcaption></figcaption></figure>

## Contoh penggunaan redis pada CMD

<figure><img src="../.gitbook/assets/redis.png" alt=""><figcaption><p>Sumber gambar : dokcumentasi bootcamp PT Phincon</p></figcaption></figure>

## Package Redis di Golang

Untuk penggunaan redis di golang dapat menggunakan package berikut [https://github.com/redis/go-redis](https://github.com/redis/go-redis).

## Contoh code golang dengan Redis

Redis dapat digunakan untuk menyimpan value dari tipe data apapun di Golang. Cara yang mudah yaitu dengan mengkonversi value dengan suatu tipe data menjadi byte. Data byte tersebut dapat disimpan ke dalam Redis dengan tipe data Redis String. Cara konversi dari tipe data tertentu menjadi byte dapat menggunakan fungsi Marshal dari package "encoding/json".

{% code title="main.go" %}
```go
package main

import (
	"context"
	"encoding/json"
	"fmt"
	"strconv"
	"time"

	"github.com/redis/go-redis/v9"
)

var ctx = context.Background()

type rdb struct {
	redisClient *redis.Client
}

// inisialisasi redis
func (r *rdb) InitiateRedis() {
	r.redisClient = redis.NewClient(&redis.Options{
		// localhost:6379
        	Addr:     "localhost:6379",
		ClientName: "",
		Username: "",
	        Password: "",
	        DB:       0,
		// Dial timeout for establishing new connections.
		DialTimeout: 5*time.Second,
    	})
	if r.redisClient != nil {
		fmt.Println("Redis initialization")
	}
}

func main() {
	var redisTest = rdb{}
	redisTest.InitiateRedis()

	// set string data to redis
    	redisTest.RedisSetKey("username", "member_01")
    	redisTest.RedisSetKey("username", "member_02")
	redisTest.RedisSetKey("password", "Test123")

	// set integer data to redis
	num := 12313214
	str := strconv.Itoa(num)
	redisTest.RedisSetKey("token", str)

	// set array data to redis
	someArray := [3]string{"member_01", "member_02", "member_03"}
	byteArray, _ := json.Marshal(someArray)
	redisTest.RedisSetKey("user_array", byteArray)

	// set slice data to redis
	someSlice := []string{"member_01", "member_02", "member_03"}
	byteSlice, _ := json.Marshal(someSlice)
	redisTest.RedisSetKey("user_slice", byteSlice)

	// set map data to redis
	user := map[string]interface{}{
		"username": "member_01", "password": "Tes123", "token": 1214113141,
	}
	byteMap, _ := json.Marshal(user)
	redisTest.RedisSetKey("user_map", byteMap)

	// set struct data to redis
	type userdata struct {
		Username string
		Password string
		Token    int
	}
	user2 := userdata{"member_01", "Test123", 43234312432413}
	byteStruct, _ := json.Marshal(user2)
	redisTest.RedisSetKey("user_struct", byteStruct)

	// get value by key
	keys := []string{"username", "password", "token", "user_array", "user_slice", "user_map", "user_struct"}
	for _, key := range keys {
		value, err := redisTest.RedisGetKey(key)
		if err != nil {
			fmt.Printf("Error get value of key %s \n", value)
			continue
		}
		fmt.Printf("Value of username key %s is %s\n", key, value)
	}

	// delete value by key
	redisTest.RedisDeleteKey("username")
	redisTest.RedisDeleteKey("password")
}

// redis set key and value
func (r rdb) RedisSetKey(key string, value interface{}) {
	err := r.redisClient.Set(ctx, key, value, 5*time.Minute).Err()
    if err != nil {
        panic(err)
    }
	fmt.Printf("Key %s with value %v is set\n", key, value)
}

// redis get value by key
func (r rdb) RedisGetKey(key string) (value string, err error) {
	value, err = r.redisClient.Get(ctx, key).Result()
	if err == redis.Nil {
		err = fmt.Errorf("key doesn't exist : %s, data type : %T", redis.Nil, redis.Nil)
		return
	} else if err != nil {
		return
    } else {
		return
	}
}

// redis delete value by key
func (r rdb) RedisDeleteKey(key string) {
	if err := r.redisClient.Get(ctx, key).Err(); err != nil {
		if err = r.redisClient.Del(ctx, key).Err(); err != nil {
			fmt.Printf("Error delete : %s\n", err.Error())
		}
		fmt.Printf("Success delete key %s\n", key)
	}
}
```
{% endcode %}

```
Redis initialization
Key username with value member_01 is set
Key username with value member_02 is set
Key password with value Test123 is set
Key token with value 12313214 is set
Key user_array with value [91 34 109 101 109 98 101 114 95 48 49 34 44 34 109 101 109 98 101 114 95 48 50 34 44 34 109 101 109 98 101 114 95 48 51 34 93] is set
Key user_slice with value [91 34 109 101 109 98 101 114 95 48 49 34 44 34 109 101 109 98 101 114 95 48 50 34 44 34 109 101 109 98 101 114 95 48 51 34 93] is set
Key user_map with value [123 34 112 97 115 115 119 111 114 100 34 58 34 84 101 115 49 50 51 34 44 34 116 111 107 101 110 34 58 49 50 49 52 49 49 51 49 52 49 44 34 117 115 101 114 110 97 109 101 34 58 34 109 101 109 98 101 114 95 48 49 34 125] is set
Key user_struct with value [123 34 85 115 101 114 110 97 109 101 34 58 34 109 101 109 98 101 114 95 48 49 34 44 34 80 97 115 115 119 111 114 100 34 58 34 84 101 115 116 49 
50 51 34 44 34 84 111 107 101 110 34 58 52 51 50 51 52 51 49 50 52 51 50 52 49 51 125] is set
Value of username key username is member_02
Value of username key password is Test123
Value of username key token is 12313214
Value of username key user_array is ["member_01","member_02","member_03"]
Value of username key user_slice is ["member_01","member_02","member_03"]
Value of username key user_map is {"password":"Tes123","token":1214113141,"username":"member_01"}
Value of username key user_struct is {"Username":"member_01","Password":"Test123","Token":43234312432413}
```

Reference:

{% embed url="https://www.hostinger.co.id/tutorial/apa-itu-cache" %}
