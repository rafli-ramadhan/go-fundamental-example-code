# Penerapan Looping pada Sorting

## 1. Bubble Sort

```go
package main

import "fmt"

func BubbleSort(slice[] int)[]int {
    for i:=0; i< len(slice)-1; i++ {
        for j:=0; j < len(slice)-i-1; j++ {
            if (slice[j] > slice[j+1]) {
                // swap
                slice[j], slice[j+1] = slice[j+1], slice[j]
            }
        }
    }
    return array
}

func main() {
   slice := []int{11, 14, 3, 8, 18, 17, 43};
   fmt.Println(BubbleSort(array))
}
```

## 2. Quick Sort

```go
package main

import (
	"fmt"
	"math/rand"
)

func main() {
    slice := []int{11, 14, 3, 8, 18, 17, 43}
	fmt.Println(quicksort(slice))
}

func quicksort(s []int) []int {
    if len(s) < 2 {
        return s
    }
     
    left, right := 0, len(s)-1
    pivot := rand.Int() % len(s)
     
    // swap
    s[pivot], s[right] = s[right], s[pivot]
     
    for i, _ := range s {
        if s[i] < s[right] {
            s[left], s[i] = s[i], s[left]
            left++
        }
    }
     
    s[left], s[right] = s[right], s[left]
     
    quicksort(s[:left])
    quicksort(s[left+1:])
     
    return s
}
```
