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

### Interface
*An interface is a contract between a class and the outside world. When a class implements an interface, it promises to provide the behavior published by that interface.*

---

## Variables:

- **Instance variablev(Non-Static Fields)** : 
- **Class variable(Static Fields)** :
- **Local variable** :
- **Parameters** : 

***

#### equals() and hashCode() methods: 

hashCode() method is used to get a unique integer for given object. This integer is used for determining the bucket location, when this object needs to be stored in some HashTable like data structure. By default, Object’s hashCode() method returns and integer representation of memory address where object is stored. In case of Integer wrapper class, it retunrs primitive int value and in case of String class, returns ```s[0]*31^(n-1) + s[1]*31^(n-2) + ... + s[n-1]```

equals() method, as name suggest, is used to simply verify the equality of two objects. Default implementation simply check the object references of two objects to verify their equality.

##### Overriding the default behavior

Consider Employee.class 

  ```java
  public class Employee
{
    private Integer id;
    private String firstname;
 
    public Integer getId() {
        return id;
    }
    public void setId(Integer id) {
        this.id = id;
    }
    public String getFirstname() {
        return firstname;
    }
    public void setFirstname(String firstname) {
        this.firstname = firstname;
    }
}
```
```java
public class EmployeeTest {
    public static void main(String[] args) {
        Employee e1 = new Employee();
        Employee e2 = new Employee();
 
        e1.setId(100);
        e2.setId(100);
 
        //Prints false in console
        System.out.println(e1.equals(e2));
    }
}
```
For correct behaviour, we need to overrride equals()
```java
public boolean equals(Object o) {
    if(o == null)
    {
        return false;
    }
    if (o == this)
    {
        return true;
    }
    if (getClass() != o.getClass())
    {
        return false;
    }
     
    Employee e = (Employee) o;
    return (this.getId() == e.getId());
     
}
```
Still we are not done yet, according to the contract: if you override equals() method then you must override hashCode() method.

```java
        Set<Employee> employees = new HashSet<Employee>();
        employees.add(e1);
        employees.add(e2);
         
        //Prints two objects
        System.out.println(employees);
 ```
 In order to correct this, we need to override hashCode() method also
 ```java
 @Override
public int hashCode()
{
    final int PRIME = 31;
    int result = 1;
    result = PRIME * result + getId();
    return result;
}
```


## OOPS Concepts
- [Encapsulation]()
- [Inheritance]()
- [Polymorphism]()
- [Abstraction](#interface)



