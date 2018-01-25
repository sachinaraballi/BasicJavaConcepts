# Basics

### Object: 
*An object is a software bundle of related **state**(fields) and **behavior**(methods).*

Benefits of bundling :
- **Modularity:** The source code for an object can be written and maintained independently of the source code for other objects. Once created, an object can be easily passed around inside the system.
- **Information-hiding:** The internal implementation of an Object remains hidden from the outside world.
- **Code re-use:** This allows specialists to implement/test/debug complex, task-specific objects, which you can then trust to run in your own code.
- **Pluggability and debugging ease:** If a particular object turns out to be problematic, you can simply remove it from your application and plug in a different object as its replacement. 

#### Creating an Object (Instantiate a Class)
This can be done in two ways 
1.  new operator: The new operator instantiates a class by dynamically allocating(run time) memory for a new object and returning a reference to that memory. This reference is then stored in the variable.
```java 
Object variable = new Object();
```
![](https://docs.oracle.com/javase/tutorial/figures/java/objects-oneRef.gif)


In Java, Array is treated as Object, so we use new keyword to create an Array e.g 
```java 
int arr[] = new int[10];
```
2. Reflection



### Class: 
*A class is a blueprint or prototype from which objects are created.*

### Interface:
*An interface is a contract between a class and the outside world. When a class implements an interface, it promises to provide the behavior published by that interface.*

---

## Variables:

- **Instance variablev(Non-Static Fields)** : 
- **Class variable(Static Fields)** :
- **Local variable** :
- **Parameters** : 


## OOPS Concepts
- [Encapsulation]()
- [Inheritance]()
- [Polymorphism]()
- [Abstraction](#some-heading)

