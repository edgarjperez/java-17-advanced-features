---
title: "Optionals"
permalink: /optionals
layout: default
---

# Optional


## NullPointerException

Occurs when you dereference a null value,
for example when you call an instance method
or access a field via a variable that has the value null.

## What is an Optional?

An Optional is a container that can either
contain a value or be empty.

### Considerations

- Optional is an immutable value class. Should not be used for synchronization.
- Optional was primarily designed to be used as a return type for methods.

## Bad

````java
public class A implements Serializable {

    private Optional<String> name;
}
````

````java
public Customer getCustomer(Optional<Long> id) {..}
````


## Good 

````java
public Optional<Customer> getCustomer(long id) {..}
````

[Back](./../index.md)