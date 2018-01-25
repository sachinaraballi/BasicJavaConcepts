# Polymorphism in Java

**"One Interface, multiple methods"**

There are two types of polymorphism in java -

- Compile time polymorphism (or Static polymorphism)
- Runtime polymorphism (or Dynamic Polymorphism)

We can perform polymorphism in java by

- Method overloading (Compile time polymorphism)
- Method overriding (Runtime polymorphism)

## Overriding 

An ability of a subclass to re-implement an instance method inherited from a superclass.

### Rules for method overriding 

1. **Only inherited methods can be overridden.**
**public**, **protected** and **default** (in the same package) can be overridden and **private** methods cannot be overridden.
2. **Final and static methods cannot be overridden.**
- A final method means that it cannot be re-implemented by a subclass, thus it cannot be overridden. -
- A static method is available to all instances of the superclass and its subclasses, so it’s not permissible to re-implement the static method in a particular subclass.
3. **The overriding method must have same argument list.**
4. **The overriding method must have same return type (or subtype).**
5. **The overriding method must not have more restrictive access modifier.**
6. **The overriding method must not throw new or broader checked exceptions.**
7. **Use the super keyword to invoke the overridden method from a subclass.**
8. **Constructors cannot be overridden.**
Because constructors are not methods and a subclass’ constructor cannot have same name as a superclass’ one, so there’s nothing relates between constructors and overriding.
9. **Abstract methods must be overridden by the first concrete (non-abstract) subclass.**
10. **A static method in a subclass may hide another static one in a superclass, and that’s called hiding.**
```java
public class Animal {
    public static void testClassMethod() {
        System.out.println("The static method in Animal");
    }
}

class Dog extends Animal {
    public static void testClassMethod() {
        System.out.println("The static method in Dog");
    }
    
    public class DoSomething {
      testClassMethod(); // prints The static method in Dog
      Animal.testClassMethod(); // calls hidden method
    }
    }
}
```
11. **The synchronized modifier has no effect on the rules of overriding.**
12. **The strictfp modifier(float point related) has no effect on the rules of overriding.**
