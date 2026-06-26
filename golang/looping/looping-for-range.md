# Looping for range

Looping for range digunakan untuk mengulangi urutan pada value dengan tipe data string, array, slice, map dan channel.

## Contoh code looping for range pada string

Looping di string di Golang menghasilkan value dengan tipe data rune bukan byte.

```go
package main

import "fmt"

func main() {
	str := "Hello, world!"
	for i, c := range str {
		fmt.Printf("str[%d] = %c type %T\n", i, c, c)
	}
}

```

```go
str[0] = H type int32
str[1] = e type int32
str[2] = l type int32
str[3] = l type int32
str[4] = o type int32
str[5] = , type int32
str[6] =   type int32
str[7] = w type int32
str[8] = o type int32
str[9] = r type int32
str[10] = l type int32
str[11] = d type int32
str[12] = ! type int32
```

## Contoh code looping for range pada array

```go
package main

import "fmt"
 
func main() {
    values := [7]int{1, 3, 5, 7, 9, 11, 13}
 
    for i, val := range values {
        fmt.Printf("value[%d] = %d \n", i, val)
    }
}
```

```
value[0] = 1 
value[1] = 3 
value[2] = 5 
value[3] = 7 
value[4] = 9 
value[5] = 11
value[6] = 13
```

## Contoh code looping for range pada slice

```go
package main

import "fmt"
 
func main() {
    values := []int{1, 3, 5, 7, 9, 11, 13}
 
    for i, val := range values {
        fmt.Printf("value[%d] = %d \n", i, val)
    }
}
```

```
value[0] = 1 
value[1] = 3 
value[2] = 5
value[3] = 7
value[4] = 9
value[5] = 11
value[6] = 13
```

## Contoh code looping for range pada map

```go
package main

import "fmt"
 
func main() {
    users := map[string]interface{}{
		"member_01" : "aliana",
		"member_02" : "dawam",
		"member_03" : "yusran",
	}
 
    for key, val := range users {
        fmt.Printf("value[%s] = %s \n", key, val)
    }
}
```

```
value[member_01] = aliana 
value[member_02] = dawam 
value[member_03] = yusran
```

## Contoh code looping for range pada channel

```go
package main

import (
    "fmt"
)

func main() {
    ch := make(chan int)

    go func() {
        for i := 0; i < 100; i++ {
			// channel in
            ch <- i
        }
		// channel must be close
		// if not will be deadlock
        close(ch)
    }()

	// channel out
    for v := range ch {
        fmt.Println(v)
    }
}

```

```
0
1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
18
19
20
21
22
23
24
25
26
27
28
29
30
31
32
33
34
35
36
37
38
39
40
41
42
43
44
45
46
47
48
49
50
51
52
53
54
55
56
57
58
59
60
61
62
63
64
65
66
67
68
69
70
71
72
73
74
75
76
77
78
79
80
81
82
83
84
85
86
87
88
89
90
91
92
93
94
95
96
97
98
99
```

Reference:

{% embed url="https://stackoverflow.com/questions/72019318/golang-running-for-range-loop-on-channel-how-to-continue-execution-of-block-ha" %}
