# Challenge : OOP

Apa output dari code di bawah ini ?

```java
import java.util.*;

class Kendaraan {
    String jenis = "Kendaraan Umum";

    public Kendaraan() {
        System.out.print("Kendaraan Diinisialisasi - ");
        tampilkanJenis();
    }

    public void tampilkanJenis() {
        System.out.println(jenis);
    }
}

class Mobil extends Kendaraan {
    String jenis = "Mobil Sedan";

    public Mobil() {
        // Ada super() implisit di sini
        System.out.print("Mobil Diinisialisasi - ");
        tampilkanJenis();
    }

    @Override
    public void tampilkanJenis() {
        System.out.println(jenis);
    }
}

public class Main {
    public static void main(String[] args) {
        System.out.println("--- Mulai Eksperimen ---");
        Kendaraan unit = new Mobil();
        System.out.println("Jenis dari atribut: " + unit.jenis);
    }
}
```

```
--- Mulai Eksperimen ---
Kendaraan Diinisialisasi - null
Mobil Diinisialisasi - Mobil Sedan
Jenis dari atribut: Kendaraan Umum
```
