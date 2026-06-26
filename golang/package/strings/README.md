# Strings

Berikut adalah contoh _code_ fungsi-fungsi yang terdapat di package string di golang

```go
package main

import (
	"fmt"
	"strings"
)

func main() {
	fmt.Println(
		strings.Contains("test", "es"),
		// true
		strings.Count("test", "t"),
		// 2
		strings.HasPrefix("test", "te"),
		// true
		strings.HasSuffix("test", "st"),
		// true
		strings.Index("test", "e"),
		// 1
		strings.Join([]string{"a","b","c"}, "-"),
		// "a-b-c"
		strings.Repeat("a", 5),
		// "aaaaa"
		strings.Replace("aaaa", "a", "b", 2),
		// "bbaa"
		strings.Replace("aaaa", "a", "b", 3),
		// "bbba"
		strings.Replace("bbaaaa", "a", "b", 3),
		// "bbbbba
		strings.Split("a-b-c-d-e", "-"),
		// []string{"a","b","c","d","e"}
		strings.ToLower("TEST"),
		// "test"
		strings.ToUpper("test"),
		// "TEST"
	)
}
```

```
true 2 true true 1 a aaaaa bbaa bbba bbbbba [a b c d e] test TEST
```

Reference:

{% embed url="https://www.santekno.com/mengenal-library-standard-string-pada-golang/" %}
