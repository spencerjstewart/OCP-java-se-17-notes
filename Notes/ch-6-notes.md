# Chapter 6 - Class Design

## Understanding Inheritance

### Declaring a Subclass

Inheritance is transitive. If X extends Y and Y extends Z, then X extends Z.

### Class Modifiers

- `final`: may not be extended
- `abstract`: requires concrete subclass to instantiate
- `sealed`: The class may only be extended by a specific list of classes.
- `non-sealed`: A subclass of a sealed class permits potentially unnamed subclasses. 
- `static`: Used for `static` nested classes defined within a class.

### Single vs. Multiple Inheritance

Java only supports single inheritance, but also supports implementing multiple interfaces in one class.

### Inheriting Object

All classes in Java inherit from `java.lang.Object`. `Object` is the only class that doesn't have a parent class.

## Creating Classes

### Extending a Class

Remember when working with subclasses that `private` members are never inherited.

Package members are only inherited if the 2 classes are in the same package.

### Applying Class Access Modifiers

A `.java` file can have at most 1 `public` top-level class.

A `.java` file can have multiple package-private classes.

A top-level class cannot be `protected` nor `private`.

### Calling the `super` reference

Java checks for a local variable, a local member variable, then a super member variable.

If a member variable is on the super class, but not defined as local member variable, you can still access it with `this.prop`.

## Declaring Constructors

### Creating a Constructor

Must match name of class. Cannot have return type.

Parameters cannot use `var`.

Multiple constructors allowed as long as parameters are distinct.

### The Default Constructor

Every class has a constructor whether you explicitly define one or not.

An important rule to know is that the compiler only inserts the default constructor when no constructors are defined.

The default constructor has the same access level as the class in which it is defined. 

### Calling Overloaded Constructors with this()

Does not compile:
```
public Hamster(int weight) {
    Hamster(weight, "brown"); // compile error
}
```

```
public Hamster(int weight) {
    new Hamster(weight, "brown"); // compiles, but creates an extra object
}
```

The proper way to call a constructor within a constructor:
```
public Hamster(int weight) {
    this(weight, "brown");
}
```

When using `this()`, it must be the first statement in the constructor, which also means there can only be one call to this():
```
public Hamster(int weight) {
    print("chew");
    this(weight, "brown"); // compile error
}
```
The compiler will report an error if there's a cycle.

### Calling Parent Constructors with super()

The first statement of *every* constructor call is an implicit or explicit call to `super()`, or another constructor using `this()`.

### Default Constructor Tips and Tricks

If we have a super class that has a constructor with parameters, and no no-parameter default constructor, the subclass must make an explicit call to the super constructor.

It's fine for the subclass to have a no-parameter constructor, but it must call the explicit parent constructor. Additionally, the subclass cannot refer to `super()` (no-parameter default constructor), because one has been neither inserted nor defined.

## Initializing Objects

### Initializing Classes

Order of initialization:
1. If X extends Y, initialize Y first.
2. Process `static` variable declarations in the order in which they appear in the class.
3. Process all `static` initializers in the order in which they appear in the class.

This program will print `ABC` once:
```
public class Animal {
    static {
        print("A");
    }
}

public class Hippo extends Animal {
    public static void main(String[] grass) {
        print("C");
        new Hippo();
        new Hippo();
    }
    static {
        print("B");
    }
}
```

### Initializing `final` Fields

`final` fields can be assigned a value in the line in which they are declared, or in a static initializer block (the `final` field does not have to be static).

Unlike `static` class member, `final` non-static class members can be set in a constructor.

Important rule: By the time the constructor completes, all `final` instance variables must be assigned a value exactly once.

This does not compile, because it's possible to not assign a value to `type` if you call the `MouseHouse()` constructor:
```
public class MouseHouse {
    private final int volume;
    private final String type;
    {
        this.volume = 10;
    }
    public MouseHouse(String type) {
        this.type = type;
    }
    public MouseHouse() {
        this.volume = 2;
    }
}
```

Can be fixed with:
```
public MouseHouse() {
    this(null);
}
```

### Initializing Instances

Order of initialization for instance of X:
1. Initialize X if it has not been initialized.
2. If X extends Y, initialize the instance of Y first.
3. Process all instance variable declarations in the order in which they appear in the class.
4. Process all instance initializers in the order in which they appear in the class.
5. Initialize the constructor, including any overloaded constructors referenced with `this()`.

## Inheriting Members

### Overriding a Method

Occurs when a subclass declares a new implementation for an inherited method with the same signature and a covariant return type. Access modifiers, optional specifiers, and declared exceptions can vary with some rules:
1. Access Modifiers:
   - You can use the same or less restrictive access modifier compared to the overridden method.
2. Optional Specifiers:
   - `final`: cannot override method declared as final
   - `static`: cannot override a static method, if you try to, you will hide the super class method instead of overriding it
   - `synchronized`, `native`, `strictfp` can be used in the overriding method without restriction
3. Declared Exceptions: 
   - You can declare fewer or narrower exceptions.
   - You cannot declare newer or broader checked exceptions in the overriding method.
   - If there are no checked exceptions in the overridden method, the overriding method cannot introduce them.
4. `static` method hiding
   - If a subclass method has the same signature as a super class `static` method, the code will not compile. If they are both `static`, method hiding occurs.

### Hiding Variables

Java does not allow variables to be overridden, only hidden.

## Creating Abstract Classes

### Introducing Abstract Classes

Rules:
- Only instance methods can be marked `abstract`, not variables, constructors, or `static` methods.
- The `abstract` keyword cannot be placed after the `class` keyword or after the return type in methods.

### Creating a Concrete Class

An abstract class can extend a non-abstract class and vice versa.

### Creating Constructors in Abstract Classes

If an abstract class does not provide a constructor, the compiler will automatically insert a default no-argument constructor.

The constructor of an abstract class can only be called when its concrete subclass is initialized.

Both method and class cannot be marked both `abstract` and `final`.

Method cannot be both `abstract` and `private`.

Method cannot be both `abstract` and `static`.

## Creating Immutable Objects

Immutable objects are useful for secure code and when dealing with concurrency.

### Declaring an Immutable Class

Strategy:
1. Mark the class as `final` or make all of the constructors private.
2. Mark all the instance variables `private` and `final`.
3. Don't define any setter methods.
4. Don't allow referenced mutable objects to be modified.
5. Use a constructor to set all properties, making a copy if needed.

