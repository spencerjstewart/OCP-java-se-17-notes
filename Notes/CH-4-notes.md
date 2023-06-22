# CHAPTER 4 - Core API

### Creating and manipulating Strings

- `null` + a String = `null` + String
- Strings are immutable
- formatting
  - `String.format()`
    - uses rounding instead of truncating
  - `"some string".formatted(args...)`
- `StringBuilder.delete()` will not throw index out of bounds exception
- `StringBuilder.replace()` is different from `String.replace()`

### Understanding equality

- `String.equals()` compares the values of the Strings
- `==` compares the references of the Strings
  - the references are created when you create the primitive
    - manipulating a String so that the values equal another String at runtime will not make `==` return true
			- The one exception is compile-time constants
      - you can use `String.intern()` to make the references equal

### Understanding arrays

- valid syntax:

```java
int[] numAnimals;
int [] numAnimals2;
int []numAnimals3;
int numAnimals4[];
int numAnimals5 [];
```

- different behavior when declaring if on a single line

```java
int[] ids, types; // both are arrays
int ids2[], types2; // ids2 is an array, types2 is an int
```

- An array of `String`s does not allocate space for the `String` objects, only the references to them
- If you initialize an array with a size, the array will be filled with the default value for that type
- `Arrays.binarySearch()` required a sorted array
- arrays do not have a `length()` method, they have a `length` field
- `Arrays.binarySearch()` knows where the element should be inserted, and if it doesn't exist, 
  it will return the negative of that index minus one
- `Arrays.compare()` 
  - return values for arrays with the same length
    - negative number means the first array is smaller than the second.
    - a zero means arrays are equal
    - a positive number means the first array is larger than the second.
  - return values for arrays with different lengths
		- If all the elements are the same but the first array is longer than the second array,
      return a positive number.
    - If all the elements are the same buy the second array is longer than the first array,
			return a negative number.
    - If the arrays have different elements, it returns the result of the first nonmatching element.
  - Other rules
    - `null` is smaller than any non-`null` value
    - `Strings`
      - one is smaller if it is a prefix of another
      - numbers are smaller than letters
      - uppercase is smaller than lowercase
	- If the types are different, will not compile
- `Arrays.mismatch()`
  - returns -1 if the arrays are equal
  - returns the index of the first mismatched element if the arrays are not equal

### Math APIs

- for `min()` and `max()`
  - return type is the same as the parameters
- `round()`
  - floats return int
  - doubles return long
- `floor()` and `ceil()`
	- return type is the same as the parameter
- `pow(double num, double exp)`
	- returns a double

### Working with dates and times

- Creating dates and times
  - `LocalDate`
    - contains just a date--no time and no time zone
  - `LocalTime`
    - contains just a time--no date and no time zone
  - `LocalDateTime`
    - contains both a date and time but no time zone
  - `ZonedDateTime`
    - contains a date, time, and time zone
  - all four use the static method `.now()`
  - All of these objects have private constructors + static methods that return instances
    - there are no public constructors, will not compile if you try to use `new`
- Periods
  - Cannot chain methods
		- The code will compile but it won't be what you intended
      `var period = Period.ofYears(1).ofWeeks(1);` == `var period = Period.ofWeeks(1);`
  - Internally, it only uses years, months, days
    - `ofWeeks()` is for convenience
  - `Period.of(years, months, days)`
    - `toString()` prints out `P1Y2M3D`
      - anything that's zero is not printed
    - You can use `LocalDate` and `LocalDateTime` with a `Period`
- Duration
  - Intended for smaller units of time
  - days, hours, minutes, seconds, milliseconds, nanoseconds
  - milliseconds
    - `Duration.ofMillis(1).toString()` == `PT0.001S` // 3 decimal places
    - `Duration.ofNanos(1).toString()` == `PT0.000000001S` // 9 decimal places
  - no factory method like `Period`
  - `Duration.of(num, ChronoUnit)`
- Using `ChronoUnit` for differences
  - `ChronoUnit.UNIT.between(start, end)`
- Period vs Duration
  - Period
		- date-based
		- years, months, days
  - Duration
    - time-based
    - hours, minutes, seconds, milliseconds, nanoseconds
- `Instant`
	- represents a specific moment in time in the GMT time zone
  - You can use `toInstant()` with `ZonedDateTime`, but not with `LocalDateTime`
    - `LocalDateTime` does not have a time zone, and therefore is not universal
- Accounting for DST
  - `LocalDateTime` does not account for DST
  - `ZonedDateTime` does account for DST
	- If you try to create a time that doesn't exist, Java `ZonedDateTime` will adjust it for you

### Practicing questions

~~1~~
- a, c
- Code does not compile. Always check types.

~~2~~
- c, e
- When creating a multidimensional array, must specify the size of the first dimension.

~~3~~
- a, c, d, f
- When using Dates, the enum is called `Month`, not `MonthEnum`

~~4~~
- a, c, d, e 
- line 9 is a trick, "Hello" is already in the string pool, so calling intern() doesn't change anything

5
- b

6
- c
- When using `Math.round()`, the return type is an int when called with a float, and a long when called with a double
- `Math.random()` returns a double, so you can't assign it to a `float`

~~7~~
- a, d
- These are 6 hours apart: 2022–08–28T05:00 GMT-04:00 2022–08–28T09:00 GMT-06:00

~~8~~ 
- a, c, f
- StringBuilder.replace() replaces a range of characters 
- String.replace() does not replace a range of indices

9
- a, c, f
- An array does not override equals(), so it uses object equality.

~~10~~
- c
- All of these lines compile. The min() and floor() methods return the same type passed 
  in: int and double, respectively. The round() method returns a long when called with a
  double. 

11
- e

~~12~~
- a, d
- If you call `String.substring()` with the same start and end index, it returns an empty string.

~~13~~
- d 
- A String is immutable. Calling concat() returns a new String but does not change
  the original. A StringBuilder is mutable. Calling append() adds characters to the existing
  character sequence along with returning a reference to the same object.

14
- a, f
- Remember that `Instant` does not have a public constructor. Without a time zone, Java cannot calculate
  the instant in time. The code will not compile.

~~15~~
- b, f
- `Arrays.binarySearch()` Numbers sort before letters and uppercase sorts before lowercase.

~~16~~
- b, d
  - a, b, g

```java
var base = "ewe\nsheep\\t";
int length = base.length();
int indent = base.indent(2).length();
int translate = base.translateEscapes().length();
/**
 * There are 11 characters in base because there are two escape characters. The \n
 counts as one character representing a new line, and the \\ counts as one character representing
 a backslash. This makes option B one of the answers. The indent() method adds
 two characters to the beginning of each of the two lines of base. This gives us four additional
 characters. However, the method also normalizes by adding a new line to the end if
 it is missing. The extra character means we add five characters to the existing 11, which is
 option G. Finally, the translateEscapes() method turns any text escape characters into
 actual escape characters, making \\t into \t. This gets rid of one character, leaving us with
 10 characters matching option A.
 */
```

17
- a, g

~~18~~
- e, f
- You have to remember that trailing whitespaces are ignored by the compiler in text blocks.
- Remember that String literals are immutable.

~~19~~
- c, d
- When doing `Arrays.compare()`, positive integer if arrays are different and first is larger.
- The compare() method returns a positive integer when the arrays are different and
  the first is larger. This is the case for option A since the element at index 1 comes first alphabetically.
  It is not the case for option C because the s4 is longer or for option E because the
  arrays are the same.
  The mismatch() method returns a positive integer when the arrays are different in a position
  index 1 or greater. This is the case for options B and D since the difference is at index 1.
  It is not the case for option F because there is no difference.

~~20~~
- b, d, 
	- a, d
- `ChronoUnit.HOURS.between()` only returns the difference in actual duration that has passed, not the wall clock 
  hours. So even if daylight savings time occurs, it will not be reflected in the result.

~~21~~
- a, b, c
- b returns a `String` that isn't stored anywhere. Be careful about `String` operations not being assigned.

~~22~~
- e
- Dates are immutable, and the output for the methods were not stored anywhere.