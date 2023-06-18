# CHAPTER 3 - MAKING DECISIONS

### Creating decision-making statements

- pattern matching
  - don't confuse this with the `Pattern` class or regex
  - pattern variable must be a subtype of the type on the left
    - cannot be the same
  - pattern variable must be a new variable
    - cannot be an existing variable
    - there are some exceptions e.g.:
      <pre><code>// This compiles
      Number value = 123;
      if (value instanceof List data) {}
      </code></pre>
  - flow scoping
    - the variable is only in scope when the compiler can definitely determine its type
    - the pattern matching variable can be used outside of the if-block if the compiler can determine its type

### Applying _switch_ statements

- case values can be combined in Java 14
  - you can write
  <pre><code>switch(animal) {
  case 1, 2: System.out.println("1 or 2");
	}</code></pre>
  
  instead of

	<pre><code>switch(animal) {
  	case 1: case 2: System.out.println("1 or 2");
	}</code></pre>
- switch statements are not required to have any cases or a default case
- if no break statements, all statements after the matching case are executed
- the data type of the parameter is not evaluated until runtime
- the parameter must be a _char_, _byte_, _short_, _int_, _Character_, _Byte_, _Short_, _Integer_, _String_, or _enum_
- the data type of the case value must match the data type of the parameter, or can be automatically promoted to it
- the case value must be a literal value or an initialized final variable
	- cannot be a method that always returns the same value
- switch expressions
  - yield is required when returning from a code block
  - yield is optional when returning from a single expression

### Constructing _for_ loops

- infinite loop

<pre><code>for(;;) {
  System.out.println("Hello World");
}</code></pre>

- you can add multiple statements to the initialization and update sections of the for loop
  - variables in initialization block must be the same data type
- for-each loop
  - right side must be an array or an object that implements `Iterable`

### Controlling flow with branching

- you can add a label to the head of a while or for loop to break to it
- you can add a label to the head of a while or for loop to continue to it
  - this transfers control to the boolean expression of the loop vs the break statement which transfers control 
    to the statement after the loop
- be careful about unreachable code
  - statements after break, continue, and return statements

### Review questions

~~1~~ 
- a, b, c, e, f
- you can also use `var` in a switch expression

~~2~~
- e, f

<pre><code>3: int temperature = 4;
4: long humidity = -temperature
+ temperature * 3;
5: if (temperature>=4)
6: if (humidity < 6) System.out.println("Too Low");
7: else System.out.println("Just Right");
8: else System.out.println("Too High");
</code></pre>

3
- a, d, f, h

~~4~~
- e
- the switch expression must cover all possible values
  - this can be done with a default case

~~5~~
- c
- any code after continue, break, or return will not compile

~~6~~
- c, e
- switch expressions that take a String require a `default` branch

~~7~~
- a, b, d
- myArray[myArray.length] will never compile

8
- g

~~9~~
- d, f
- with for-loops, the update of the control variable happens after the first loop

~~10~~
- d
- remember the rules about compile-time constants in switch statements

11
- a

12
- c

13
- G
- `while` requires the parentheses around the boolean expression

14
- b, d, f

15
- f

~~16~~
- a, b
- review tricky loops

~~17~~
- h
- review tricky loops

18
- c, e

~~19~~
- C
- you cannot access a variable in the while boolean expression if the variable was declared in the do {} block

~~20~~
- b, d
- For option B,
  the first continue on line 8 causes the execution to skip the innermost loop on the first iteration
  of the second loop but not the second iteration of the second loop. The innermost loop
  is executed, and with continue on line 12, it produces an infinite loop at runtime, making
  option B incorrect.

~~21~~
- E
- `Long` is not compatible for a switch statement
- cannot have same case values
- block returns in a switch expression must have a `yield` statement and 1 semicolon

~~22~~
- G 
- In switch statements, it's fine to use `var`.
  - In switch expressions, you cannot use `var`.
- the `final` keyword is irrelevant when figuring out what is valid as a parameter or case in both switch statements 
  and switch expressions

~~23~~
- a
- remember that an "else if" must come after an "if", and before an "else"

~~24~~
- a, d
- `for (var obj in myList) {}` is not valid syntax
  - there is no `in` keyword in Java

~~25~~
- b
- Remember fall through behavior happens when there is no break statement, and the case value matches the parameter
	- All cases after the matching case are executed unless there is a break statement

26
- F 

~~27~~
- B
- You can throw an exception in a switch expression.
- Every case block in a switch expression must have a `yield` statement or a `throw` statement
  - If you have an if-else statement in a case block, you must have a `yield` statement in both the if and else blocks

28
- F

29
- c 