## Different Ways to Create an Object

1. **new keyword**

2. **class.forName()**
```java
public class Test {
    public static void main(String[] args) {
        class Animal {
            //Local inner class
        }
        try {
            //load the class dynamically
            Class<?> class1 = Class.forName("Animal");
            //create the object dynamically
            Object object = class1.newInstance();
        } catch (ClassNotFoundException | InstantiationException | IllegalAccessException e) {
            e.printStackTrace();
        }
    }
}
```
3. **Class Loader and newInstance() Method**
```java
public class Test {
    public static void main(String[] args) {
        class Animal {
        }
        try {
            ClassLoader cl = Test.class.getClassLoader();
            Class class1 = cl.loadClass("Test");
            Object object = class1.newInstance();
        } catch (ClassNotFoundException | InstantiationException | IllegalAccessException e) {
            e.printStackTrace();
        }
    }
}
```
4. **Object Deserialization**
5. **clone() method**
The *clone()* method is used to create a copy of an existing object, in order to use clone() method the corresponding class should have implemented _Cloneable_ interface a [Marker Interface](#marker_interface).


### Marker Interface
Interfce with no fields and methods, usually helps the JVM compiler
e. g. Clonable, Serializable

