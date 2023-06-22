### Chapter 1 progress

1. end of chapter questions
	- 20
2. online wiley exam chapter 1
	- 45

### Needs to be studied

- `main` method
  - `void` must be included in signature
  - `final` is optional
- text blocks
  - any "code" inside a text block is ignored by the compiler
  - `\` then a return is escaped, so there is no new line
- `var`
  - cannot be initialized to `null`, but can be assigned it later
- packages and imports
	- if 2 classes are in the same package, and one class is using the other, no import is required
  - when importing the same class from 2 packages, in order for the code to compile, one must be a wildcard,
    and the other must be a specific import
    - specific import will take precedence over the wildcard
- `String`
	- does not have a length property, but a length method
- garbage collection
  - an object may be eligible for garbage collection but never removed from the heap
- `Long`
  - `Long.parseLong()` returns a `long`
  - `Long.valueOf()` returns a `Long`
- constructor vs method
  - constructors never have a return type
- remember local variables must be initialized before use, but they can be declared without
    being initialized and the code will compile
- _Q2_ is a valid identifier