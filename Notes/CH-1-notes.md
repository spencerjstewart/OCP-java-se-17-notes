# <u>Chapter 1 - BUILDING BLOCKS</u>

### Learning about the environment

- JDK
	- Key commands:
		- `javac` converts .java files to .class files
		- `java` executes programs
		- `jar` packages files into a JAR file
		- `javadoc` generates documentation
		- `javap` dissassembles .class files to view bytecode
		- `jshell` REPL

### Understanding the class structure

- 2 primary elements
	1. methods
	2. fields
- comments
- If you have more than 1 type in a file, the top-most type is public.
	- Inner classes are not considered top-level types, so they can also have public access.
- public types must match the filename

### Writing a main() method

- Creating a main() method
	- `static` binds a method to its class so it called with just the class name
	- 3 acceptable formats for the parameter:
		- `String options[]`
		- `String...options`
		- `String[] options`
	- `final` is an acceptable optional keyword for both the method and the parameter
- Passing parameter to a Java program
	- You can pass a string with spaces in it using double quotes
	- Single-File Source Code: `java Zoo.java Bronx Zoo`
		- compile and run by including the .java extension

### Understanding package declarations and imports

- `java.lang` is automatically imported
- Wildcards
	- wildcards only match class files, not folders
	- can only have 1 wildcard in 1 import statement
	- cannot import non-static methods
- default package
	- special unnamed package
	- you can tell if a class is in default package if there's no package statement
- compiling with wildcards

```
javac packagea/*.java
```

- `-d` specifies the target directory when compiling
- classpath designation when compiling, designate folders and JARs
- Example java command:

```
java-cp/home/zoodirectory Zoo
```

- creating JARs
	- `-c` create new JAR
	- `-v` prints details when working with JAR files
	- `-f` JAR filename
	- `-C` directory containing the files to be used to create the JAR

### Creating objects

- calling constructors
	- if braces follow, it's not a constructor
	- don't have to code a constructor, default do-nothing constructor
	- executing instance initializer blocks
		- instance initializers
			- code blocks that can appear outside a method
			- cannot create them in a method
	- following the order of initialization
		1. fields and instance initializer blocks are run in the order in which they appear in the file
		2. constructor runs after all fields and instance initializer blocks have run

### Understanding data types

- using primitive types
	- What is the bit size of a boolean?
		- Not specified, dependent on JVM
	- `short` and `char`, signed vs. unsigned
		- `short` is signed, `char` is unsigned
		- both are 16 bits
	- writing numeric literals
		- `int` is the default type for a numeric literal
		- `long` requires an `L` suffix
		- `float` requires an `F` suffix
		- `double` requires no suffix
	- base
		- `0b` prefix for binary
		- `0` prefix for octal
		- `0x` prefix for hexadecimal
	- underscores
		- you can use underscores to improve readability
		- you can use multiple underscores in a row
		- you can place them anywhere except at the beginning or end of a literal
- using reference types
	- holds reference to an object
- distinguishing between primitives and reference types
	- primitives will cause a compile error if you attempt to assign null
		- you can use a wrapper to assign null to a primitive
- text blocks
- line break required after first `"""` and before last `"""`
```java
String textBlock = """
Hello
World
""";
```

### Declaring variables

- 4 rules for naming variables
	1. must begin with a letter, currency symbol, or _
	2. subsequent characters may also be numbers
	3. cannot use reserved words
	4. case sensitive

- you can declare multiple variables on 1 line
```java
int a, b, c = 0;
int a = 0, b = 0, c = 0;
  ```

### Initializing variables

- local variables
	- constructor, method, or initializer block
	- can be final
	- must be initialized before use, no default value
	- does not have to be initialized when declared
	- cannot be accessed until they are initialized
		- if initializing within an if statement, must be initialized in all branches
- defining instance and class variables
	- instance variables
	- value defined within a specific instance of an object
	- class variables
		- shared among all instances of a class
		- `static` keyword
	- not required to initialize instance and class variables
		- as soon as you initialize them, they are given a default value
			- `null` for objects
			- `0` or `0.0` for numbers
			- `false` for boolean
			- `char` is given a null character `\u0000`
- inferring the type with `var`
	- "local variable type inference"
	- used with local variables
	- cannot be used for instance or class variables
	- cannot be used for method parameters
	- cannot be used for return types
		- must be defined within the same statement
	- cannot be initialized to null
	- not a reserved word, so you can use it as a variable name
		- however it is a reserved type name, so you cannot use it to define a class, interface, or enum

### Destroying objects

- Object is eligible for GC when it is no longer reachable
	- no references to it
	- no references to any other objects that reference it
- On the exam, use arrows to draw what's going on

### Practice questions

- option C is incorrect because main() method must be static

- D and E are also correct because both the package and import statements are optional

- Public is a valid identifier
- _Q2_ is a valid identifier

- Remember that if an object is being used by another object, it is not eligible for GC
  even if you assign it null

- cross out blocks that are unreachable to easily find the answer to scope questions

- don't be tricked by text blocks
- remember local variables must be initialized before use, but they can be declared without
  being initialized and the code will compile

- E is also correct, you are allowed to compile something like `var num = 1/0`, but it throws an exception
  at runtime, and the question is about what compiles/is valid

- remember that local variables have no default value, but class and instance variables do

- Remember you cannot place underscores at the beginning or end of a numeric literal
- Remember you cannot place underscores before or after a decimal point

- Remember that you don't need to import classes in the same package
- Remember importing java.lang is optional

- When thinking about whether or not import statements will compile, you need to keep in mind ambiguity.
- Remember a wildcard can only be used to import classes from a specific, not subpackages of that specific package


- An object may be eligible for garbage collection but never removed from the heap.
  - This is just another way of saying GC is not guaranteed to run

- Leading whitespace does nothing in text blocks.
- You can escape the end of a text block with a backslash
	- If you use the enter key after the backslash, you will only see 1 line
- `"""\"""` is a valid text block

- You can concatenate Strings with null.


- `var` cannot be used as a method parameter
- We know the type of var at compile time.

- Long.parseLong returns a `long`
- Love.valueOf returns a `Long`

- Remember what defines a valid constructor.

- Memorize the order in which code is executed.
- Static variables and blocks are executed in the order they appear in the file *when an object is created*

- Remember that binary and hexadecimal values can be assigned to byte, short, int, and long variables.
- Remember you prepend binary values with `0b` or `0B` and hexadecimal values with `0x` or `0X`


- Remember a double like 50.0 cannot be initialized to a float variable without a cast
	- must append `f` or `F` to the value

### Practice questions based on notes

Which of the following is a valid main() method declaration in Java? (Choose all that apply)
A. public void main(String[] args)
B. public static void main(String args)
C. public static void main(String[] args)
D. static public void main(String[] args)
E. public static main(String[] args)

Which of the following are valid identifiers in Java? (Choose all that apply)
A. Public
B. _Q2_
C. 2Q_
D. var
E. static

Consider the following code snippet:

java
Copy code
var num;
System.out.println(num);
What will be the result of compiling and running this code?
A. The code will not compile.
B. The code will compile and print null.
C. The code will compile and print 0.
D. The code will compile and print an empty string.
E. The code will compile but throw a NullPointerException at runtime.

Which of the following are valid ways to declare a numeric literal in Java? (Choose all that apply)
A. int num1 = 123_456;
B. int num2 = 123__456;
C. double num3 = 1.23_456;
D. double num4 = 1.23__456;
E. int num5 = _123456;

Which of the following statements about import in Java are correct? (Choose all that apply)
A. You don't need to import classes in the same package.
B. Importing java.lang is mandatory.
C. A wildcard can be used to import classes from a specific package and its subpackages.
D. Importing a class can cause a compile error due to ambiguity.
E. Importing java.lang is optional.

Consider the following code snippet:

java
Copy code
var text = """
Hello, World!\
""";
System.out.println(text);
What will be the output of this code?
A. Hello, World!
B. Hello, World!\
C. Hello, World!\n
D. Hello, World!\\
E. The code will not compile.

Which of the following statements about var in Java are correct? (Choose all that apply)
A. var can be used as a method parameter.
B. The type of var is known at compile time.
C. var can be used to declare instance variables.
D. var can be used to declare local variables.
E. var can be used to declare class variables.

Which of the following statements about constructors in Java are correct? (Choose all that apply)
A. A constructor can have a return type.
B. A constructor must have the same name as the class.
C. A constructor can take parameters.
D. A constructor can be private.
E. A constructor can be abstract.

Given the following code snippet, what will be the output?

java
Copy code
var num = 1/0;
System.out.println(num);
A. The code will not compile.
B. The code will compile but throw an ArithmeticException at runtime.
C. The code will compile and print Infinity.
D. The code will compile and print 0.
E. The code will compile and print NaN.

Which of the following statements about numeric literals in Java are correct? (Choose all that apply)
A. You can place underscores at the beginning or end of a numeric literal.
B. You can place underscores before or after a decimal point.
C. Binary and hexadecimal values can be assigned to byte, short, int, and long variables.
D. You prepend binary values with 0b or 0B and hexadecimal values with 0x or 0X.
E. A double like 50.0 can be initialized to a float variable without a cast.

Which of the following statements about text blocks in Java are correct? (Choose all that apply)
A. Leading whitespace does nothing in text blocks.
B. You can escape the end of a text block with a backslash.
C. """\""" is a valid text block.
D. You can concatenate Strings with null in a text block.
E. Text blocks can contain any character except for the triple-quote """.

Which of the following statements about the var keyword in Java are correct? (Choose all that apply)
A. var cannot be used as a method parameter.
B. The type of a var variable is known at compile time.
C. var can be used to declare local variables.
D. var can be used to declare instance variables.
E. var can be used to declare class variables.

Which of the following statements about constructors in Java are correct? (Choose all that apply)
A. A constructor must have the same name as the class.
B. A constructor can have a return type.
C. A constructor can be private.
D. A constructor can be static.
E. A constructor can be abstract.