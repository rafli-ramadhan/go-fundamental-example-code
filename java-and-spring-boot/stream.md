# Stream

Stream adalah saluran (pipeline) data yang memungkinkan kita untuk memproses sekumpulan data lebih simple.

### 3 Bagian Utama Stream

1. Source Data: atau tempat data berasal semisal dari List, Set, Array atau I/O channel.
2. Intermediate Operations: Operasi untuk memproses data dengan output berupa Stream.
3. Terminal Operation: Operasi yang mengakhiri pipeline dan menghasilkan hasil akhir seperti angka, List baru, atau hanya logging.

### Contoh code tanpa Stream

```java
import java.util.*;

public class Main {
    public static void main(String[] args) {
      List<String> nama = Arrays.asList("Budi", "Siti", "Andi", "Ramadhan", "Joko");
      List<String> hasil = new ArrayList<>();

      for (String n : nama) {
          if (n.length() > 4) {
              hasil.add(n.toUpperCase());
          }
      }
      System.out.println(hasil);
    }
}
```

```
[RAMADHAN]
```

### Contoh code dengan Stream untuk filter & convert result to uppercase

```java
import java.util.stream.Collectors;
import java.util.Arrays;
import java.util.ArrayList;
import java.util.List;

public class Main {
    public static void main(String[] args) {
      List<String> name = Arrays.asList("Budi", "Siti", "Andi", "Ramadhan", "Joko");

      List<String> output = name.stream()                     // 1. Source Data
                              .filter(n -> n.length() > 4)    // 2. Intermediate Operation (Filter)
                              .map(String::toUpperCase)       // 2. Intermediate Operation (Transformasi)
                              .collect(Collectors.toList());  // 3. Terminal Operation

      System.out.println(output);
    }
}
```

```
[RAMADHAN]
```

### Contoh code dengan Stream untuk filter dan map ke calculate total

```java
import java.util.*;


public class Main {
    public static void main(String[] args) {
      List<Integer> score = Arrays.asList(80, 90, 75, 60, 100);

      int totalPassedScore = score.stream()
                            .filter(n -> n > 75)
                            .mapToInt(Integer::intValue)
                            .sum();

      System.out.println("Total Passed Score: " + totalPassedScore);
    }
}
```

```
Total Passed Score: 270
```

### Contoh code dengan Stream untuk distinct dan mengurutkan angka

```java
import java.util.stream.Collectors;
import java.util.Arrays;
import java.util.ArrayList;
import java.util.List;

public class Main {
    public static void main(String[] args) {
      List<Integer> randomNumbers = Arrays.asList(5, 3, 8, 3, 1, 5, 9, 2);

      List<Integer> shortingResult = randomNumbers.stream()
                                        .distinct() // bisa distinc dulu atau sorted dulu
                                        .sorted()
                                        .collect(Collectors.toList());

      System.out.println(shortingResult);
    }
}
```

```
[1, 2, 3, 5, 8, 9]
```
