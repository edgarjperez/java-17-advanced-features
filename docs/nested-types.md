---
title: "Nested Types"
permalink: /nested-types
layout: default
---

# Nested types

Types (clasess, interfaces, records, enums) that are defined in other places than inside a package.

| Nested Types          |
|-----------------------|
| Static Nested Classes |
| Inner Classes         |
| Nested Interfaces     |
| Nested Records        |
| Nested Enums          |
| Local Types           |
| Anonymous Classes     |


## Static Nested Classes
**static** means that the members of the class belongs to the class itself, 
and not are associated with the instance of the class.

### Considerations
- Inside the static nested class, only the static members of the enclosing class are accessible.
- The nested class has full access to the static members and methods of the enclosing class, even if those are private.
- Shadowing is possible inside the nested class.
```java
public class Enclosing {

    private static int number = 23;

    private static void printNumber() {
        System.out.println(number);
    }
    
    static class Nested {
        private int number = 36;
        private void run() {
            System.out.println(number);
            System.out.println(Enclosing.number);
            printNumber();
        }
    }
}
```

### Use cases

- Builder Pattern

````java
public record Employee(String name) {}

public record Invoice(long id, Employee employee, BigDecimal amount) {
    
    public static Builder builder() {
        return new Builder();
    }
    
    public static class Builder {
        private long id;
        private Employee employee;
        private BigDecimal amount;
        
        public Builder withId(long id) {
            this.id = id;
            return this;
        }
        
        public Builder forEmployee(Employee employee) {
            this.employee = employee;
            return this;
        }
        
        public Builder payAmount(BigDecimal amount) {
            this.amount = amount;
            return this;
        }
        
        public Invoice build() {
            return new Invoice(id, employee, amount);
        }
    }
}
````

## Nested Interfaces, Records, enums

- Are implicit static