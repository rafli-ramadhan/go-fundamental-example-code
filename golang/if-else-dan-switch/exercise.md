# Exercise

1. Buatlah program menggunakan keyword if else untuk mengevaluasi variable score dan menampilkan output dengan variabel result dengan ketentuan:&#x20;

* Jika nilai score lebih atau sama dengan 90. Isi variabel result dengan nilai: 'Selamat! Anda mendapatkan nilai A'.
* Jika nilai score ada di antara 80 hingga 89. Isi variabel result dengan nilai: 'Anda mendapatkan nilai B.'&#x20;
* Jika nilai score ada di antara 70 hingga 79. Isi variabel result dengan nilai: 'Anda mendapatkan nilai C.'
* Jika nilai score ada di antara 60 hingga 69. Isi variabel result dengan nilai: 'Anda mendapatkan nilai D.'
* Jika nilai score di bawah 60. Isi variabel result dengan nilai: 'Anda mendapatkan nilai E.'

2. Buatlah program terdapat price, qty dan total, total didapat dari perkalian price dan qty dimana jika terdapat discount maka total berkurang 10%
3. Buatlah program menghitung jumlah string huruf vocal pada kata “Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.”
4. Buatlah program yang menghitung factorial 30
5. Buatlah program dimana mencari bilangan itu ganjil atau genap berdasarkan angka terbilang 1 sampai 10, contoh: satu, dua, tiga

## Jawaban

```go
package main

import (
	"fmt"
	"strings"
)

// soal no 1
func SwitchExercise2(score int) {
	var result string
	switch {
	case score >= 90 :
        	result = "A"
 	case score >= 80 && score < 89 :
        	result = "B"
	case score >= 70 && score < 79 :
        	result = "C"
    	case score >= 60 && score < 69 :
        	result = "D"
	default :
		result = "E"
	}
	
	fmt.Printf("Anda mendapatkan nilai %v \n", result)
}

// soal no 2
func CalculateTotal(price float64, qty float64, discount bool) {
	var total float64 = price * qty
	if discount {
		total = total * 0.9
	}
	fmt.Printf("\nTotal : %v \n", total)
}

// soal no 3
func CalculateVocalAlphabet(input string) {
	vocals := []string{"a" ,"e" ,"i" , "o", "u"}
	var totalVocal int = 0

	for i := range input {
		for j := range vocals {
			if strings.ToLower(string(input[i])) == vocals[j] {
				totalVocal++
			}
		}
	}
	
	fmt.Printf("Total huruf vokal pada string '%v' ada %d huruf vokal.\n", input, totalVocal)
}

// soal no 4
func CalculateFactorial(input float64) {
	var result float64 = input
	for i := 1; i < int(input); i++ {
		result = result * (input - float64(i))
	}

	fmt.Printf("Hasil dari faktorial %f adalah %f \n", input, result)
}

// soal no 5
func CheckOddOrEven(input string) {
	var number int
	switch {
	case input == "satu":
		number = 1
	case input == "dua":
		number = 2
	case input == "tiga":
	    number = 3
	case input == "empat":
	    number = 4
	case input == "lima":
	    number = 5
	case input == "enam":
	    number = 6
	case input == "tujuh":
	    number = 7
	case input == "delapan":
	    number = 8
	case input == "sembilan":
	    number = 9
	case input == "sepuluh":
	    number = 10
	default:
	    fmt.Println("angka yang kamu input salah")
	}

	if number % 2 == 0 {
		fmt.Printf("\nBilangan %v adalah bilangan genap", input)
	} else {
		fmt.Printf("\nBilangan %v adalah bilangan ganjil", input)
	}
}
```
