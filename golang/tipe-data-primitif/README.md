---
coverY: 0
---

# Tipe Data Primitif

Tipe data basic : number (int, float), string dan boolean

```go
package main

import "fmt"

var d int

func main() {
	var a int
	a = 1
	fmt.Println(a)
	
	// tipe data yang tidak bisa diubah
	const b = 2
	fmt.Println(b)

	// dynamic bisa diubah-ubah.
	c := 3 // tidak bisa handle int 64 untuk processor 32 bit dan hanya bisa digunakan pada level function
	fmt.Println(c)

	d = 4
	fmt.Println(d)

	// garbage collection -> untuk menghindari sampah-sampah variable
	nilai1, nilai2 := 2, 3
	fmt.Println(nilai1)
	fmt.Println(nilai2)

	var (
		number1, number2 int
		kata1, kata2 string
	)
	number1, number2 = 4, 5
	kata1, kata2 = "test1", "test2"

	fmt.Println(number1)
	fmt.Println(number2)
	fmt.Println(kata1)
	fmt.Println(kata2)

	// string untuk menyimpan tipe data karakter dengan tanda petik
	string1 := "test string" // default ""
	fmt.Println(string1)

	// back tick
	fmt.Println(`
	Test
	`)

	// get string value
	fmt.Println(len(string1))
	fmt.Println(string1[0]) // -> hasilnya int8 (byte) -> 116
	fmt.Println(string1[1]) // -> hasilnya int8 (byte) -> 101
	fmt.Println(string(string1[0]))
	fmt.Println(string(string1[1]))

	// int untuk menyimpan tipe data numerik
	int1 := 32 // tidak bisa memprediksi, default 0
	fmt.Println((int1))

	float1 := 3.5
	fmt.Println(int(float1))

	var isFloat bool // default false
	isFloat = true
	fmt.Println(isFloat)

	const status = "status" // tidak bisa diubah

	var nilai32 int32 = 32769
	var nilai64 int64 = int64(nilai32)
	var nilai16 int16 = int16(nilai32)
	
	fmt.Println(nilai64)
	fmt.Println(nilai16)

	fmt.Println(string("9"))
}
```

