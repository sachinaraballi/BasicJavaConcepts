# Class Loading

A class represents the **code** to be executed, whereas data represents the state associated with that code i.e. **Object** or **Instance**.

 In Java, a class will usually have its code contained in a .class file,  in the Java runtime, each and every class will have its code also available in the form of a first-class Java object, which is an instance of [java.lang.Class](https://docs.oracle.com/javase/1.5.0/docs/api/java/lang/Class.html). Whenever we compile any Java file, the compiler will embed a public, static, final field named class, of the type java.lang.Class, in the emitted byte code.

In Java, a class is identified by its fully qualified class name. The fully qualified class name consists of the **package** name and the **class** name. But a class is uniquely identified in a JVM using its fully qualified class name along with the instance of the **ClassLoader** that loaded the class. Thus, if a class named Cl in the package Pg is loaded by an instance kl1 of the class loader KlassLoader, the class instance of C1, i.e. C1.class is keyed in the JVM as `(Cl, Pg, kl1)`. This means that the two class loader instances `(Cl, Pg, kl1)` and `(Cl, Pg, kl2)` are not one and the same, and classes loaded by them are also completely different and not type-compatible to each other. 

##Types : 
1. BootstrapLoader

Whenever a new JVM is started by typing `java MyMainClass`, the "bootstrap class loader" is responsible for loading key Java classes like [java.lang.Object](https://docs.oracle.com/javase/1.5.0/docs/api/java/lang/Object.html) and other runtime code into memory first. The runtime classes are packaged inside of the **`JRE\lib\rt.jar`** file. As it call native methods to load classes, it will differ across other JVMs.

2. Extension Class Loader (ExtClassLoader)

Next comes the Java extension class loader. We can store extension libraries, those that provide features that go beyond the core Java runtime code, in the path given by the **`java.ext.dirs`** property. The ExtClassLoader is responsible for loading all .jar files kept in the **`java.ext.dirs`** path. A developer can add his or her own application .jar files or whatever libraries he or she might need to add to the classpath to this extension directory so that they will be loaded by the extension class loader.

![](https://docs.oracle.com/javase/tutorial/figures/ext/extb1.gif)

3. Application Class Loader (AppClassLoader)

he application class loader is responsible for loading all of the classes kept in the path corresponding to the **`java.class.path`** system property.

