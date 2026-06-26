---
description: In Progress
---

# Anotasi dan Package di Java Spring Boot

## Autowired

Penjelasan @Autowired dapat disimak di link berikut.

{% embed url="https://stackoverflow.com/questions/3153546/how-does-autowiring-work-in-spring" %}

Contoh code dengan @Autowired

```java
@Controller // Defines that this class is a spring bean
@RequestMapping("/users")
public class SomeController {

    // Tells the application context to inject an instance of UserService here
    @Autowired
    private UserService userService;

    @RequestMapping("/login")
    public void login(@RequestParam("username") String username,
           @RequestParam("password") String password) {

        // The UserServiceImpl is already injected and you can use it
        userService.login(username, password);

    }
}
```

Contoh code tanpa @Autowired

```java
@Controller // Defines that this class is a spring bean
@RequestMapping("/users")
public class SomeController {
    private UserService userService;

    public SomeController(UserService userService) {
        this.userService = userService;
    }

    @RequestMapping("/login")
    public void login(@RequestParam("username") String username,
           @RequestParam("password") String password) {

        // The UserServiceImpl is already injected and you can use it
        userService.login(username, password);

    }
}
```

## Override

Penjelasan @Override dapat disimak pada link berikut.

{% embed url="https://stackoverflow.com/questions/94361/when-do-you-use-javas-override-annotation-and-why" %}

Contoh code penggunaan @Override pada subclass.

{% code title="Animal.java" %}
```java
public class Animal {
    public void makeSound() {
        System.out.println("The animal makes a sound");
    }
}
```
{% endcode %}

{% code title="Dog.java" %}
```java
public class Dog extends Animal {
    @Override
    public void makeSound() {
        System.out.println("The dog barks");
    }
}

```
{% endcode %}

Contoh code penggunaan @Override pada class yang mengimplementasikan method yang sama pada suatu interface.

{% code title="FooService.java" %}
```java
public interface FooService {
    void doSomething();
}
```
{% endcode %}

{% code title="FooServiceImpl.java" %}
```java
@Service
public class FooServiceImpl implements FooService {
    @Override
    public void doSomething() {
        // ...
    }
}
```
{% endcode %}

## Qualifier

Penjelasan @Qualifier dapat simak pada link berikut.

{% embed url="https://www.javaguides.net/2018/06/spring-qualifier-annotation-example.html" %}

Contoh code penggunaan @Qualifier.

{% code title="FooFormatter.java" %}
```java
@Component("fooFormatter")
public class FooFormatter implements Formatter {
    public String format() {
        return "foo";
    }
}
```
{% endcode %}

{% code title="BarFormatter.java" %}
```java
@Component("barFormatter")
public class BarFormatter implements Formatter {
    public String format() {
        return "bar";
    }
}
```
{% endcode %}

{% code title="FooService.java" %}
```java
@Component
public class FooService {
    @Autowired
    @Qualifier("fooFormatter")
    private Formatter formatter;
}

```
{% endcode %}

## Package java.util.List

{% code title="ListExample.java" %}
```java
import java.util.ArrayList;
import java.util.List;

public class ListExample {
    public static void main(String[] args) {
        List<String> list = new ArrayList<>();

        list.add("apple");
        list.add("banana");
        list.add("cherry");

        System.out.println(list);
    }
}
```
{% endcode %}
