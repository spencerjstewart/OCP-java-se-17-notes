# Chapter 7 - Beyond Classes

## Implementing Interfaces

### Declaring and Using an Interface

You can have the keyword `abstract` in the interface definition, but it's not necessary, they are all implicitly declared `abstract`. 

Functions are implicitly `public abstract`.

Constants are implicitly `public static final`.

You can have static methods in an interface. They belong to the interface itself and you cannot override them, therefore they are accessed using the interface name itself, not by implementors or subclasses. They have a body.

`public` keyword is required when implementing an interface method.

### Extending an Interface

An interface an extend another interface using the `extends` keyword.

Unlike a class, an interface can extend multiple interfaces.

An interface cannot implement another interface.

### Inheriting Duplicate Abstract Methods

Java supports inheriting two abstract methods that have compatible method declarations (has covariant return types and the same method signature).

### Inserting Implicit Modifiers

An implicit modifier is one that the compiler will automatically insert.

Rules:
- Interfaces are implicitly `abstract`.
- Interface variables are implicitly `public`, `static`, and `final`.
- Interface methods without a body are implicitly `abstract`.
- Interface methods without the `private` modifier are implicitly `public`.
  - This applies to `abstract`, `default`, and `static` interface methods.

`private` methods in an interface are used as helper methods that are intended to be used within the interface itself. Another common usecase is to provide a common implementation used by multiple default methods.

### Interfaces vs. Abstract Classes

Even though abstract classes and interfaces are both abstract types, only interfaces make use of implicit modifiers.

```
abstract class Husky { // abstract required in class declaration
    void play(); // WILL NOT COMPILE, abstract required in method declaration
}

public class Webby extends Husky {
    void play() {} // OK - play() is declared with package access in Husky
}
```

```
interface Poodle { // abstract optional in interface declaration
    void play(); // abstract optional in method declaration
}

public class Georgette implements Poodle {
    void play() {} // WILL NOT COMPILE - play is implicitly public in Poodle
}
```

### Declaring Concrete Interface Methods

Types:
- constant variable
  - `public static final` is implicit
- `default` method
  - `public` is implicit
- `static` methodj
  - `public` is implicit
- `private` method
- `private` static method

`protected` and package-private interface members don't exist.

### `default` interface method

One usecase is backwards compatibility, if you want to add an interface method to an existing interface that has been implemented, it will break the program unless you provide a default body.

Rules:
- Can only be declared within an interface.
- Must be marked with the `default` keyword and have a body.
- Implicitly `public`.
- Cannot be marked `abstract`, `final`, or `static`.
- If a class inherits two or more `default` methods with the same method signature, then the class must override the method.
  - This is to prevent ambiguity. 
  - You can access a specific interface using the `MyInterface.super.myMethod()` syntax.

### Declaring `static` Interface Methods

Rules:
- Must be marked with the `static` keyword and include a method body.
- If no access modifier, implicitly `public`.
- Cannot be marked `abstract` or `final`.
- Not inherited.

### Reusing Code with `private` Interface Methods

Rules:
- Must be marked with the `private` modifier and include a method body.
- May be called by any method within the interface definition.
- May only be called by `default` and other `private` non-`static` methods within the interface definition.

### Calling Abstract Methods

`default` and `private` non-`static` methods can access `abstract` methods declared within the interface.

## Working with Enums

An enum is a fixed set of constants.

Provides type-safe checking at compile-time instead of runtime.

### Creating Simple Enums

Has `public` or package-private access. Semicolon is optional for simple enums (only contains a list of values).

You can compare enum values with `==` because each enum value is initialized once in the JVM.

You cannot extend an enum.

### Calling the `values()`, `name()`, and `ordinal()` Methods

Each enum value has a corresponding `int` value, in the order in which they are declared.

### Using Enums in `switch` Statements

In the case statements, it will not compile if you introduce the enum type.
```
Season summer = Season.SUMMER;
switch(summer) {
    case WINTER:
        System.out.print("Get out the sled!");
        break;
    case Season.SUMMER: // WILL NOT COMPILE
        System.out.print("Time for the pool!");
        break;
    default:
        System.out.print("Is it summer yet?");
}
```

### Adding Constructors, Fields, and Methods

The first we ask for any of the enum values, Java constructs all of the enum values. So the constructor is only called once.

You can define a different method implementation for each enum.
```
public enum Season {
    WINTER {
        public String getHours() { return "return 10am-3pm"; }
    },
    SPRING {
        public String getHours() { return "9am-5pm"; }
    },
    SUMMER {
        public String getHours() { return "9am-7pm"; }
    },
    FALL {
        public String getHours() { return "9am-5pm"; }
    };

    public abstract String getHours();
}
```

An enum can implement an interface, just provide the method body in the enum type.

All enums can be directly printed. 

## Sealing Classes

A class or interface that restricts which other classes may directly implement/extend it.

### Declaring a Sealed Class

Example:
```
public sealed class Bear permits Kodiak, Panda {}

public final class Kodiak extends Bear {}

public non-sealed class Panda extends Bear {}
```

### Compiling Sealed Classes

A sealed class must be declared in the same package as its direct subclasses. One exception is using named modules so that they are in the same module but different packages.

### Specifying the Sublcass Modifier

Every class that directly extends a sealed class must specify exactly one of the following three modifiers: `final`, `sealed`, or `non-sealed`.

### Omitting the `permits` Clause

If all of the permitted subclasses or subinterfaces are defined in the same source file, the `permits` clause is not required.

### Sealing Interfaces

One distinct feature of a sealed interface is that the `permits` list can apply to a class that implements the interface, or another interface that extends the interface.

## Encapsulating Data with Records

Encapsulation is a way to protect class members by restricting access to them.

### Applying Records

Uses the `record` keyword instead of `class`

Members automatically added to records:
- Constructor
- Accessor methods for each field
- `equals()` that returns `true` if each field is equal using `equals()`
- `hashCode()` that uses all fields
- `toString()` that prints each field in a convenient, easy-to-read format

### Understanding Record Immutability

Records have no setters and every field is implicitly `final`.

Records are implicitly `final`, although you can optionally include the `final` keyword and that will compile fine.

Like enums, you cannot extend or inherit a record.

Like enums, a record can implement a regular or sealed interface.

### Declaring Constructors in Records

The long constructor is declaring the constructor the compiler normally inserts automatically. The compiler will not insert a constructor automatically.

Each field is final, so the constructor must set every field.

A compact constructor is a special type of shorthand for records:
```
public record Crange(int numberEggs, String name) {
    public Crane {
        if (numberEggs < 0) throw new IllegalArgumentException();

        name = name.toUpperCase();
    }
}
```

You can modify compact constructor parameters, but you cannot modify fields of the record.

Records do not support instance initializers. All initializers for the fields of a record must happen in a constructor.

## Creating Nested Classes

Four types:
- Inner class: non-`static` type defined at the member level.
- Static nested class: `static` type defined at the member level.
- Local class: defined within a method body
- Anonymous class: a local class that does not have a name

As of Java 16, all four types of nested classes can define `static` variables and methods.

### Inner Class

Properties:
- Can be declared `public`, `protected`, `private` or package-private
- Can extend a class and implement interfaces
- Can be marked `abstract` or `final`
- Can access members of the outer class, including `private` members
  
Since an inner class is not `static`, it needs to be called using an instance of the outer class, so you'll need to create two objects. 

This is valid syntax: `new Home().new Room()`. This creates an instance of the inner class of `Home`.

### Anonymous Class

Must extend an existing class or implement an interface. Writing an anonymous class is equivalent to writing a local class with an unspecified name and immediately using it.

You can define anonymous classes outside a method body. This is valid:
```
public class Gorilla {
    interface Climb {}
    Climb climbing = new Climb() {};
}
```

## Understanding Polymorphism

```
public class Car extends Machine implements HasWheels {

}
Car car1 = new Car();
Machine car2 = new Car();
HasWheels car3 = new Car();
```

A compile-time error will occur if you try to assign a supertype to a subclass type without an explicit cast.

You cannot cast unrelated types (types that are not related by any hierarchy).

### Casting Interfaces

If you have a standalone class, subclass it, and in that subclass you implement an interface, you are allowed to cast the superclass to that interface at compile-time, but at runtime there will be an exception.

### `instanceof`

Compile-time error if you try to use `instanceof` with unrelated types.

### Polymorphism and Method Overriding

```
public interface Talk {
    void talk();
}

public class Bob implements Talk {
    public void talk() {
        System.out.print("Hello there");
    }
}

public class Bill extends Bob {
    public void talk() {
        System.out.print("Ok let's go");
    }
}

Bob bob = new Bob();
bob.talk();
Bob bill = new Bill();
bill.talk();

// This prints Hello thereOk let's go
```

What matters here is the actual underlying type of the object at runtime, that's the method used.

This is different for static methods, where the method called is based on the reference type of variable, not the underlying object.