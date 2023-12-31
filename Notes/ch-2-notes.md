# <u>Chapter 2 - OPERATORS</u>

### Applying unary operators

- `~` is the bitwise complement operator
  - applies to byte, short, char, int, and long
  - trick
    - `~x` is the same as `-(x+1)`

### Working with binary operators

- numeric promotion rules:
  - if 2 different types, promote to the larger type
  - if one integral, the other floating point, promote to floating point
  - `byte`, `short`, and `char` are promoted to `int` anytime they're used with a binary arithmetic operator
  - resulting value is the same type as the promoted operands

### Assigning values

- casting values vs. variables
  - casting is not required when working with literals that fit in the data type
  - casting is required when working with variables and you're narrowing the data type
- compound operators
  - they also perform casting
- return value of assignment operators
  - result of an assignment is the value of the assignment

### Comparing values

- equality operators
  - can be applied to numeric primitives, boolean, and object references
  - `null == null` is true
  - `null != null` is false
- relational operators
  - `instanceof`
    - `null instanceof Object` is always false
      - even if you call instanceof on an explicitly `null` object, it will always return false
    - explicitly calling `null instanceof null` is a compile error
		- a compilation error happens if you use `instanceof` on incompatible types
- logical operators
  - `&`, `|`, and `^` are bitwise operators when applied to numeric primitives
		and logical operators when applied to boolean data
  - `&&` and `||` are called conditional operators
    - these have the short-circuit feature
      - beware of unperformed side-effects on the right side of conditional operators

### Ternary operator

- `? :` is the only operator that takes three operands
- In single-line multiple ternary operator statements, the innermost ternary operator is only evaluated if 
  the outermost ternary operator actually returns that ternary operator
