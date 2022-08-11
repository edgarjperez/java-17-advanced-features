---
title: "Records"
permalink: /records 
layout: default
---

# Records

### *Immutable Data Objects*

Immutable object
: An object of which the **state cannot be changed** after the object is constructed.

Examples of immutable classes in Java API

- [String Class](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)
- [Class Integer](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Integer.html)
- [Class BigInteger](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/math/BigInteger.html)

### Advantages and disadvantages of Immutability

| Advantages                                                          | Disadvantages        |
|---------------------------------------------------------------------|----------------------|
| Immutability makes programs **less complicated**                    | String Concatenation |
| Immutable objects are **thread-safe**                               | Circular References  |
| Collections such as **HashMap** and **HashSet** expect Immutability |                      |
| Immutable objects can be safely **shared** and **reused**           |                      |

#### String concatenation

```java
// Inefficient code
String str = "";
for (int i = 0; i < 100; i++) {
    str = str + "hello ";
}
```

### Immutable class code example

```java

import java.util.Objects;

/**

 * Example of an immutable class.
 */
public final class ProductCls { // The class itself is final

    // Private final fields
    private final long id;
    private final String name;
    private final String description;

    // A constructor with a parameter for each field
    public ProductCls(long id, String name, String description) {
        this.id = id;
        this.name = name;
        this.description = description;
    }

    // Getter methods for the fields
    public long getId() {
        return id;
    }

    public String getName() {
        return name;
    }

    public String getDescription() {
        return description;
    }

    // equals(Object o), hashCode() and toString() methods
    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (o == null || getClass() != o.getClass()) return false;
        ProductCls that = (ProductCls) o;
        return id == that.id && Objects.equals(name, that.name) && Objects.equals(description, that.description);
    }

    @Override
    public int hashCode() {
        return Objects.hash(id, name, description);
    }

    @Override
    public String toString() {
        return "ProductCls{" +
                "id=" + id +
                ", name='" + name + '\'' +
                ", description='" + description + '\'' +
                '}';
    }
}

```
### Record code example

```java
/**
 * Example of a record with the same functionality as the immutable class {@link ProductCls}
 */
public record ProductRec(long id, String name, String description) {
}
```

### The Class Hierarchy of Records

- Records are implicitly **final**.
- Record cannot **extend classes**, but can **implement interfaces**.
- The common superclass for records is **java.lang.Record**.

### Use cases

- Domain Objects
- Value Objects
- Data Transfer Objects

### When not to use

- JPA Entities
- Singletons
- No direct replacement for JavaBeans
