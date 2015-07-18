# Java Programming Interviews Exposed
## Menu
* [Chapter 6: Design Patterns](#design-patterns)
* [Chapter 8: Java Basics](#java-basics)


## <a name="design-patterns"></a>Chapter 6: Design Patterns
### Builder Pattern
The intention of the builder pattern is **to find a solution to the telescoping constructor anti-pattern**. The telescoping constructor anti-pattern occurs when the increase of object constructor parameter combination leads to an exponential list of constructors. Instead of using numerous constructors, the builder pattern uses another object, a builder, that receives each initialization parameter step by step and then returns the resulting constructed object at once.
![builder](https://upload.wikimedia.org/wikipedia/commons/thumb/f/f3/Builder_UML_class_diagram.svg/1000px-Builder_UML_class_diagram.svg.png)

---
### Strategy Pattern
The Strategy Pattern **enables you to easily swap specific implementation details of an algorithm without requiring a complete rewrite**. 
Using the Strategy Pattern enables you to defer decisions about which implementation to use until run time. 
![strategy pattern](https://upload.wikimedia.org/wikipedia/commons/3/39/Strategy_Pattern_in_UML.png)

---
### Template Pattern
The Template Pattern is used to defer or delegate some or all steps of an algorithm to a subclass. 
![template](http://www.tutorialspoint.com/design_pattern/images/template_pattern_uml_diagram.jpg)

---
### Decorator Pattern
The Decorator Pattern enables you to change or configure the functionality of a specific object, such as adding buttons or functionality to a scrollbar, or defining exactly how to model sandwich orders from two different customers from the same set of ingredients. 
![decorator](http://www.tutorialspoint.com/design_pattern/images/decorator_pattern_uml_diagram.jpg)

---
### Flyweight Pattern
The Flyweight Pattern can be a useful pattern in situations where you have several objects, and many may represent the same value.In these instances, it can be possible to share the values as long as the objects are immutable.
![flyweight](http://www.tutorialspoint.com/design_pattern/images/flyweight_pattern_uml_diagram.jpg)

---
### Singleton Pattern
**A singleton is a class that allows only one instance to be created.**

```Java
private static Singleton INSTANCE;
public static Singleton getInstance() { 
	if (INSTANCE == null) {
		INSTANCE = new Singleton(); 
	}
	return INSTANCE; 
}

// Java中的enum写法
public enum Singleton {
    INSTANCE;
    
    // methods
    public void execute (String arg) {
        // Perform operation here 
    }
}
```

> lazy initialization: The Singleton instance is only created when it is first needed. At first glance, it looks like any other calls to getInstance() will return that same instance. If, however, INSTANCE is null, and a thread is switched after the if statement but before INSTANCE is initialized, then a second (or more) thread calling getInstance() will also have the if statement return true and create a new object. This can result in strange, erratic behavior or worse, memory leaks resulting in the JVM eventually crashing.
Java 5 introduced the Enum type. If you create the Singleton as a single-element Enum, the JVM guarantees that only one instance will ever be created

## <a name="java-basics"></a>Java Basics
> Be aware that **char** is unsigned. That is, the range of values a char can take is from ==0 to 65,535==, because chars represent Unicode values.




