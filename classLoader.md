# Class Loading

A class represents the **code** to be executed, whereas data represents the state associated with that code i.e. **Object** or **Instance**.

 In Java, a class will usually have its code contained in a .class file,  in the Java runtime, each and every class will have its code also available in the form of a first-class Java object, which is an instance of [java.lang.Class](https://docs.oracle.com/javase/1.5.0/docs/api/java/lang/Class.html). Whenever we compile any Java file, the compiler will embed a public, static, final field named class, of the type java.lang.Class, in the emitted byte code.

In Java, a class is identified by its fully qualified class name. The fully qualified class name consists of the **package** name and the **class** name. But a class is uniquely identified in a JVM using its fully qualified class name along with the instance of the **ClassLoader** that loaded the class. Thus, if a class named Cl in the package Pg is loaded by an instance kl1 of the class loader KlassLoader, the class instance of C1, i.e. C1.class is keyed in the JVM as `(Cl, Pg, kl1)`. This means that the two class loader instances `(Cl, Pg, kl1)` and `(Cl, Pg, kl2)` are not one and the same, and classes loaded by them are also completely different and not type-compatible to each other. 

![](http://2.bp.blogspot.com/-HCTsr-j_ojw/USTOh1f8JwI/AAAAAAAAAjg/YegPspR5K48/s1600/java_classloader_hierarchy.PNG)

##Types : 
1. **BootstrapLoader**

Whenever a new JVM is started by typing `java MyMainClass`, the "bootstrap class loader" is responsible for loading key Java classes like [java.lang.Object](https://docs.oracle.com/javase/1.5.0/docs/api/java/lang/Object.html) and other runtime code into memory first. The runtime classes are packaged inside of the **`JRE\lib\rt.jar`** file. As it call native methods to load classes, it will differ across other JVMs.

2. **Extension Class Loader (ExtClassLoader)**

Next comes the Java extension class loader. We can store extension libraries, those that provide features that go beyond the core Java runtime code, in the path given by the **`java.ext.dirs`** property. The ExtClassLoader is responsible for loading all .jar files kept in the **`java.ext.dirs`** path. A developer can add his or her own application .jar files or whatever libraries he or she might need to add to the classpath to this extension directory so that they will be loaded by the extension class loader.

![](https://docs.oracle.com/javase/tutorial/figures/ext/extb1.gif)

3. **Application Class Loader (AppClassLoader)**

he application class loader is responsible for loading all of the classes kept in the path corresponding to the **`java.class.path`** system property.


## The Java Class Loading Mechanism

The Java platform uses a **delegation model** for loading classes. The basic idea is that every class loader has a **"parent"** class loader. When loading a class, a class loader first **"delegates"** the search for the class to its parent class loader before attempting to find the class itself.
Here are some highlights of the class-loading API:

- Constructors in **`java.lang.ClassLoader`** and its subclasses allow you to specify a parent when you instantiate a new class loader. If you don't explicitly specify a parent, the virtual machine's system class loader will be assigned as the default parent.
- The **`loadClass`** method in **`ClassLoader`** performs these tasks, in order, when called to load a class:
1. If a class has already been loaded, it returns it.
2. Otherwise, it delegates the search for the new class to the parent class loader.
3. If the parent class loader does not find the class, **`loadClass`** calls the method **`findClass`** to find and load the class.
```java
protected synchronized Class<?> loadClass
    (String name, boolean resolve)
    throws ClassNotFoundException{

    // First check if the class is already loaded
    Class c = findLoadedClass(name);
    if (c == null) {
        try {
            if (parent != null) {
                c = parent.loadClass(name, false);
            } else {
                c = findBootstrapClass0(name);
            }
        } catch (ClassNotFoundException e) {
            // If still not found, then invoke
            // findClass to find the class.
            c = findClass(name);
        }
    }
    if (resolve) {
	    resolveClass(c);
    }
    return c;
}
```

- The **`findClass`** method of **`ClassLoader`** searches for the class in the current class loader if the class wasn't found by the parent class loader. You will probably want to override this method when you instantiate a class loader subclass in your application.

```java
public class MyClassLoader extends ClassLoader{

    public MyClassLoader(){
        super(MyClassLoader.class.getClassLoader());
    }
}
```

- The class **`java.net.URLClassLoader`** serves as the basic class loader for extensions and other JAR files, overriding the findClass method of **`java.lang.ClassLoader`** to search one or more specified URLs for classes and resources.

