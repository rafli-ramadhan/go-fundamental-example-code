# Exercise (Function)

Buat lah program gunakan multiple return value dari data nama berikut:&#x20;

• Aditya Ananta Putra \
• ADNAN NUR JAILANI\
• Afrila Zahra Prasetyo \
• Aida Nirmala \
• Amalia Rahma \
• ANDINI DWI RIZKY PUTRI \
• Angga Putra \
• CAHAYA WIJAYA IJAM \
• Dea Christina \
• DEVITA NANDA OKTAVIA \
• DEWI AYU LESTARI \
• Dhevina Ananda Fitri \
• DHEVY YANI RIZKI \
• Dwi Mahani \
• Eri Santosos \
• Faiza Amalia Mahfudz \
• FAUZIYATUNNISA \
• Febriyanti Syabina \
• Hafifah Nur Azmi Pratiwi \
• Juliansyah Husien \
• Kharisa Nur Aziza \
• Lun Wina \
• MAHREVA ROESTHA RAMADANIATY \
• MUHAMMAD FADHILAH \
• Muhammad Fatah Firdaus \
• Muhammad Rafly Ahya \
• Muhammad Rahmin Noor \
• Muhammad Rivaldi \
• Muhammad Rizky Rachmadhani \
• Nadiah Nahdhah Islamiyah \
• NOLA FEBRIANA SAPUTRI \
• RAFADYAN REYHAN MARITZA WERAT \
• Robby Satria \
• Salshabilla Wahyu Anafi \
• STEVI VIONI PAKULLA \
• Winny Rahmah Nia&#x20;

Ketentuan: \
a. Menghitung jumlah data\
b. Mencari data yang terdapat kata “Muhammad” dengan return slice\
c. Menghitung huruf a dari masing-masing nama dengan return map key:nama dan value:jumlah huruf a

## Answer

```go
package main

import (
	"fmt"
	"strings"
)

var usernames []string = []string{
    "Aditya Ananta Putra",
    "ADNAN NUR JAILANI",
    "Afrila Zahra Prasetyo",
    "Aida Nirmala",
    "Amalia Rahma",
    "ANDINI DWI RIZKY PUTRI",
    "Angga Putra",
    "CAHAYA WIJAYA IJAM",
	"Dea Christina",
    "DEVITA NANDA OKTAVIA",
    "DEWI AYU LESTARI",
    "Dhevina Ananda Fitri",
    "DHEVY YANI RIZKI",
    "Dwi Mahani",
 	"Eri Santosos",
    "Faiza Amalia Mahfudz",
    "FAUZIYATUNNISA",
    "Febriyanti Syabina",
    "Hafifah Nur Azmi Pratiwi",
    "Juliansyah Husien",
    "Kharisa Nur Aziza",
    "Lun Wina",
    "MAHREVA ROESTHA RAMADANIATY",
    "MUHAMMAD FADHILAH",
    "Muhammad Fatah Firdaus",
    "Muhammad Rafly Ahya",
    "Muhammad Rahmin Noor",
    "Muhammad Rivaldi",
    "Muhammad Rizky Rachmadhani",
    "Nadiah Nahdhah Islamiyah",
    "NOLA FEBRIANA SAPUTRI",
    "RAFADYAN REYHAN MARITZA WERAT",
    "Robby Satria",
    "Salshabilla Wahyu Anafi",
    "STEVI VIONI PAKULLA",
    "Winny Rahmah Nia",
}

	
func check(usernames ...string) (totalData int, checkMuhammad []string, totalAperData map[string]int) {
	totalAperData = map[string]int{}
	for i := range usernames {
		// check if username contain alphabet "A"
		if strings.Contains(strings.ToLower(usernames[i]), "muhammad") {
			checkMuhammad = append(checkMuhammad, usernames[i])
		}
		
		// calculate total data
		totalData++
		
		// calculate "A" for every data
		totalAperData[usernames[i]] = strings.Count(strings.ToLower(usernames[i]), "a")
	}

	return totalData, checkMuhammad, totalAperData
}

func main() {
	totalData, checkMuhammad, totalAperData := check(usernames...)

	fmt.Println(totalData)
	fmt.Println(checkMuhammad)
	fmt.Println(totalAperData)
}

```

```
36
[MUHAMMAD FADHILAH Muhammad Fatah Firdaus Muhammad Rafly Ahya Muhammad Rahmin Noor Muhammad Rivaldi Muhammad Rizky Rachmadhani]
map[ADNAN NUR JAILANI:4 ANDINI DWI RIZKY PUTRI:1 Aditya Ananta Putra:6 Afrila Zahra Prasetyo:5 Aida Nirmala:4 Amalia Rahma:5 Angga Putra:3 CAHAYA WIJAYA 
IJAM:6 DEVITA NANDA OKTAVIA:5 DEWI AYU LESTARI:2 DHEVY YANI RIZKI:1 Dea Christina:2 Dhevina Ananda Fitri:4 Dwi Mahani:2 Eri Santosos:1 FAUZIYATUNNISA:3 Faiza Amalia Mahfudz:6 Febriyanti Syabina:3 Hafifah Nur Azmi Pratiwi:4 Juliansyah Husien:2 Kharisa Nur Aziza:4 Lun Wina:1 MAHREVA ROESTHA RAMADANIATY:7 MUHAMMAD FADHILAH:4 Muhammad Fatah Firdaus:5 Muhammad Rafly Ahya:5 Muhammad Rahmin Noor:3 Muhammad Rivaldi:3 Muhammad Rizky Rachmadhani:5 NOLA FEBRIANA SAPUTRI:4 Nadiah Nahdhah Islamiyah:6 RAFADYAN REYHAN MARITZA WERAT:7 Robby Satria:2 STEVI VIONI PAKULLA:2 Salshabilla Wahyu Anafi:6 Winny Rahmah Nia:3]
```
