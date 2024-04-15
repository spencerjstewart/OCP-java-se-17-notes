# Chapter 8 - Lambdas and Functional Interfaces

## Writing Simple Lambdas

A *lambda expression* is a block of code that gets passed around.

Java relies on context when figuring out what lambda expressions mean. *Context* is where and and how the lambda is interpreted.

The parentheses around the lambda parameters can be omitted only if there is a single parameter and its type is not explicitly stated.

Not enough information to infer type so does not compile:
`var invalid = (Animal a) -> a.canHope(); // Does not compile`

## Coding Functional Interfaces

A *functional interface* is an interface that contains a single public abstract method, it can have any number of default, static, and private methods.

The `@FunctionalInterface` is optional. It tells the compiler you intend to code a functional interface and will warn you if you do not follow the rules.

```
@FunctionalInterface
public interface Spring {
    public void sprint(int speed);
}

// These are valid functional interfaces:

public interface Dash extends Sprint {}

public interface Climb {
    void reach();
    default void fall() {}
    static int getBackUp() { return 100; }
    private static boolean checkHeight() { return true; }
}
```

### Object Methods Exception

These methods are inherited from `Object` and therefore do not count toward the single abstract method rule:
```
public String toString()
public boolean equals(Object)
public int hashCode()
```

## Using Method References

Four method reference formats:
- `static` methods
- Instance methods on a particular object.
- Instance methods on a parameter to be determined at runtime.
- Constructors

### Calling `static` Methods

```
interface Converter {
    long round(double num);
}

Converter methodRef = Math::round;
System.out.println(methodRef.round(100.1));
```

### Calling Instance Methods on a Particular Object

```
interface StringStart {
    boolean beginningCheck(String prefix);
}

var str = "Zoo";
StringStart methodRef = str::startsWith;
System.out.println(methodRef.beginningCheck("A"));
```

### Calling Constructors

```
interface StringCopier {
    String copy(String value);
}

StringCopier methodRef = String::new;
StringCopier lambda = x -> new String(x);
var myString = methodRef.copy("Zebra");
System.out.println(myString.equals("Zebra")); // true
```

## Working with Built-in Functional Interfaces

An important note is that functional interfaces support covariant return types, but not covariant parameter types.

### Implementing `Supplier`

Used when you want to generate values without inputting.

```
@FunctionalInterface
public interface Supplier<T> {
    T get();
}

Supplier<LocalDateTime> getTime = LocalDateTime::now;
System.out.println(getTime.get());
```

### Implementing `Consumer`

When you want to take one or two parameters, but not return anything.

```
@FunctionalInterface
public interface Consumer<T> {
    void accept(T t);
}
```

### Implementing `Predicate` and `BiPredicate`

`Predicate` is often used when filtering and matching.

```
@FunctionalInterface
public interface Predicate<T> {
    boolean test(T t);
}

public class Main {
	public static void main(String[] args) {

		Predicate<Integer> isGreaterThan10 = Main::test;
		System.out.println(
				isGreaterThan10.test(10));
	}

	private static boolean test(Integer num) {
		return num > 10;
	}
}
```

### Implementing `Function` and `BiFunction`

Return type is the 2nd or 3rd input.

```
@FunctionalInterface
public interface Function<T, R> {
    R apply(T t);
}
```

### Implementing `UnaryOperator` and `BinaryOperator`

Special cases of `Function`: all input parameters and return type must be the same time.

```
T apply (T t);
T apply (T t1, T t2);
```

### Convenience Methods on Functional Interfaces

`Consumer`
- `andThen()`

`Function`
- `andThen()`
- `compose()`

`Predicate`
- `and()`
- `negate()`
- `or()`

### Learning the Functional Interfaces for Primitives

Generics are removed from each functional interface except the `Function` variants.

The abstract method name and function interface name are often changed for the primitive variant.

## Working with Variables in Lambdas

Tricky exam content: You can add modifiers to lambda parameters like `final` or even an annotation like `@Deprecated`.

### Using Local Variables Inside a Lambda Body

You cannot use the same name as a parameter when declaring a local variable.

### Referencing Variables from the Lambda Body

The only thing lambdas cannot access are variables that are not final or effectively final. For example you cannot assign to parameter names inside the lambda method body. If you create a local variable, it must be assigned once.



