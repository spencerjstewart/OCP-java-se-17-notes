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