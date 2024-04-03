# CHAPTER 5 - METHODS

## Designing Methods

- The method signature is the method name + parameter list.
  
### Optional Specifiers 

  - modifiers:
    - static
    - abstract
    - final
    - default: used in interface to provide default implementation
    - synchronized
    - native
    - strictfp
  - these can be in any order, but must appear before return type
  
### Return Type

This does not compile, because `return` must always be reachable.
```
String hike8 (int a) {
    if (1 < 2) return orange;
}
```

### Method Signature

The method signature is the name of the signature plus the types of the parameters. The names of the parameters is irrelevant.

## Declaring Local and Instance Variables

All local variable references are destroyed after the block is executed, but the objects they point to may still be accessible.

### Local Variable Modifiers

`final` is the only modifier that can be applied to a local variable.

Using `final` with local variables is a good practice. 


### Instance Variable Modifiers

- `final`
  - must be given a value when declared or when the object is instantiated
  - `final` instance variables are not given a default value if not assigned one like non-`final` instance variables
- `volatile`
- `transient`

## Working with Varargs

### Creating a Varargs Method

Rules:
- A method can have at most 1 varargs parameter.
- varargs must be the last parameter in the list.

### Calling a Varargs Method

You must pass in an array, or list the element of the array and let Java create it for you.

If you call a method with no arguments that had a varargs parameter, Java creates an array of length zero.

### Accessing Elements of a Vararg

Just like accessing an array.
```
public static void run(int... steps) {
    System.out.print(steps[1]);
}
```

## Accessing `static` Data

The `static` keyword indicates that a variable, method, or class belongs to the class rather than a specific instance of the class.

### Designing `static` Methods and Variables

2 main purposes:
- For utility methods that don't require an instance.
- For state that is shared by all instances, such as a counter.

### Accessing a `static` Variable or Method

You can use a null instance to access a static variable or method:
```
Snake s = new Snake();
System.out.println(s.hiss); 
s = null;
System.out.println(s.hiss); // this still works
```

### Class vs. Instance Membership

A `static` member cannot call an instance member without referencing an instance of the class.
```
public class MantaRay {
    private String name = "Sammy";
    public void third() {
        System.out.print(name); 
    }
    public static void main(String args[]) {
        third(); // does not compile
    }
}
```

This can be fixed by creating an instance of MantaRay first, then calling `third`.
```
public static void main(String args[]) {
    var ray = new MantaRay();
    ray.third();
}
```

Similarly, `static` variables cannot use an instance variable without an instance of the class.

### `static` Initializers

The `static` keyword before braces specify this block should be run when class is loaded.

You don't have to assign a value to a `static final` variable, as long as it's initialized with a `static` initializer block.

### `static` Imports

`static` imports are for importing `static` methods and variables.

You cannot use a `static` import for importing classes.

This will not compile because `asList` is imported, but not `Arrays`:
```
import static java.util.Arrays.asList;
public class MyClass {
    public static void main(String[] args) {
        Arrays.asList("one");
    }
}
```

Compiler error if you try to `static` import 2 methods or variables with the same name.

## Passing Data among Methods

Java is "pass-by-value".
```
public static void main(String[] args) {
    int num = 4; // remains as 4 even after num is assigned 8
    newNumber(num)
}
public static void newNumber(int num) {
    num = 8; // this doesn't affect num in the main method
}
```

### Autoboxing and Unboxing Variables

Wrapper classes are useful for:
- Nullability
- Utility methods
- For use in collections and generics
    - Cannot have primitive types for generics nor collections
  
You cannot unbox a `null`:
```
Integer myInt = null;
int myNullInt = myInt; // NullPointerException
```

Java will not implicitly cast and autobox simultaneously:
```
Long myLong = 8; // does not compile
```

## Overloading Methods

Same name, but different parameter lists. Overriding is different from overloading.

Everything other than the method name can vary when overloading. The parameter list must vary in order to overload.

When calling an overloaded method, the most specific method is called.
```
public static String speak(String s) {
    return "something";
}
public static String speak(Object s) {
    return "obj";
}
public static void main(String[] args) {
    print(speak("thing"));
    print("-");
    print(5);
}
// something-obj
```

Primitives work in a similar way to reference variables.
```
public static void myMethod(int i) {
    print("ok");
}
public static void myMethod(long l) {
    print("no");
}
public static void main(String[] args) {
    myMethod(5);
    myMethod(10L);
}
// okno
```

Autoboxing also applies when you have overloaded methods with a wrapper class and the corresponding primitive.

This is a valid overload, but arrays do not autobox:
```
public static void walk(int[] ints) {}
public static void walk(Integer[] integers) {}
```

Overloading doesn't work with this usage of varargs:
```
public static void add(int[] nums) {}
public static void add(nums...) {} // does not compile
```
