# C Lang Notes

## Contents

- [Basics](#basics)
  - [Base Structure](#base-structure)
  - [Data Types](#data-types)
    - [Integer Types](#integer-types)
    - [Floating-point Types](#floating-point-types)
  - [Variables](#variables)
  - [Constants and Literals](#constants-and-literals)
  - [Operators](#operators)

## Basics

### Base structure

```C
#include <stdio.h> // Import packages needed

int main(void) {
    printf("Hello World\n");
    return 0;
}
```

`int` refers to what will be returned by the function

`main` - all C programs require a `main` function as an entry point to the program

`void` is needed when a function does not take any arguments.

`printf` is a function of `stdio.h` that prints to the console.

`return 0` - the function must have a return value.

### Data Types

**Basic Types -** arithmetic types

- integer
- floating-point

**Enumerated Types -** arithmetic types used to t define variables that can only assign certain discrete integer values throughout the program

**Void Types -** indicates no value is available

**Derived Types -** include

- pointer
- array
- structure
- union
- function

#### Integer Types

| Type           | Storage Size | Value Range                                          |
| -------------- | ------------ | ---------------------------------------------------- |
| char           | 1 byte       | -128 to 127 or 0 255                                 |
| unsigned char  | 1 byte       | 0 to 255                                             |
| signed char    | 1 byte       | -128 to 127                                          |
| int            | 2 or 4 bytes | -32,768 to 32,767 or -2,147,483,648 to 2,147,483,647 |
| unsigned int   | 2 or 4 bytes | 0 to 65,535 or 0 to 4,294,967,295                    |
| short          | 2 bytes      | -32,768 to 32,767                                    |
| unsigned short | 2 bytes      | 0 to 65,535                                          |
| long           | 8 bytes      | -9223372036854775808 to 9223372036854775807          |
| unsigned long  | 8 bytes      | 0 to 18446744073709551615                            |

#### Floating-Point Types

| Type        | Storage Size | Value Range            | Precision         |
| ----------- | ------------ | ---------------------- | ----------------- |
| float       | 4 byts       | 1.2E-38 to 3.4E+38     | 6 decimal places  |
| double      | 8 bytes      | 2.3E-308 to 1.7E+308   | 15 decimal places |
| long double | 10 bytes     | 3.4E-4932 to 1.1E+4932 | 19 decimal places |

### Variables

- Can be composed of letters, digits, and the underscore
- Must begin with a letter or underscore
- Case sensitive

#### Declaration

```C
// Declaration without initializing
int i, j, k;
char c, ch;
float f, salary;
double d;

// Declaration with initializing
extern int d = 3, f = 5;
int d = 3, f = 5;
byte z = 22;
char x = 'x';
```

`extern` is used to declare a variable that can be used across files. Variables can be declared multiple times in a program, but only once in a file, function, or code block.

```C
#include <stdio.h>

// Variable declaration:
extern int a, b;
extern int c;
extern float f;

int main () {

    /* variable definition */
    int a, b;
    int c;
    float f;

    /* actual initialization */
    a = 10;
    b = 20;

    c = a + b;
    printf("value of c : %d \n", c);

    f = 70.0/3.0;
    printf("value of f : %f \n", f);

    return 0;
}
```

**Result:**

```
value of c : 30
value of f : 23.333334
```

or with function

```C
// function declaration
int func();

int main() {

    //function call
    int i = func();
}

// function definition
int func() {
    return 0;
}
```

#### lvalue vs rvalue

**lvalue** - refer to a memory location. Can be on the left or right side of an assignment.

**rvalue** - refer to data value stored at some address in memory. Can only appear on the right side of an assignment.

### Constants and Literals

Fixed values. The values themselves are called literals.

Literals can be a decimal, octal, or hexadecimal. A prefix indicates which. 0x or 0X for hexadecimal, 0 for octal, and nothing for decimal. A suffix can be used in combination to indicate unsigned (U) and long (L).

```
// Example literals

212 // Legal - decimal
215u // Legal - unsigned decimal
0xFeeL // Legal - hexadecimal long
078 // Illegal - 0 indicates octal, but 8 is not an octal digit
032UU // Illegal - cannot repeat a suffix

// More legal examples

85 // decimal
0213 // octal
0x4b // hexadecimal
30 // int
30u // unsigned int
30l // long
30ul // unsigned long

```

Floating-point literals are made up of an integer part, a decimal point, a fractional part, and an exponent part. They may be represented in decimal or exponential form.

```
// Example floating-points

3.14159 // legal
314159E-5L // legal
510E // illegal - incomplete exponent
210f // illegal - no decimal or exponent
.e55 // illegal - missing integer or fraction

```

Character literals are enclosed in single quotes. Can be a plain character (e.g., 'x'), and escape sequence (e.g., '\t'), or a universal character (e.g.,'\u02C0').

**Escape Sequence Characters:**
| Escape Sequence | Meaning |
|--------------- | --------------- |
| \\\ | \ character |
| \\' | ' character |
| \\" | " character |
| \\? | ? character |
| \a | Alert or bell |
| \b | Backspace |
| \f | Form feed |
| \n | Newline |
| \r | Carriage return |
| \t | Horizontal tab |
| \v | Vertical tab |
| \ooo | Octal number of on to three digits |
| \xhh | Hecadecimal number of one or more digits |

#### Interpreting Decarations

Operators with identical precedence

- unary \* "dereference" operator which denots a pointer
- binary [] "array subscription" operator denotes an array
- (1+n)-ary () "function call" operator denotes a function
- () grouping parentheses override the precedence and associativity of the rest of the listed operators

| Operator                | Relative Precedence | Associativity |
| ----------------------- | ------------------- | ------------- |
| [] (array subscription) | 1                   | Left-to-right |
| () (function call)      | 1                   | Left-to-right |
| \* (dereference)        | 2                   | Right-to-left |

| Expression        | Interpretation                             |
| ----------------- | ------------------------------------------ |
| thing[x]          | an array of size X of...                   |
| thing(t1, t2, t3) | a function taking t1, t2, t3 and returning |
| \*thing           | a pointer to...                            |

```C
char *names[20];
// [] takes precedence over *, so the
// interpretation is: name is an array
// of size 20 of a point to char

char (*place)[10];
// Parentheses override precedence, the
// * is applied first:
// place is a pointer to an array of size 10 char

int fn(long, short);
// no precedence to consider

int *fn(void);
// the () is applied first: fn is a function
// taking void and returning a pointer to int

int (*fp)(void);
// overriding the precedence of ():
// fp is a pointer to a function taking void and
// returning int

int arr[5][8];
/* Multidimensional arrays are not an exception to the
rule; the [] operators are applied in left-to-right order
according to the associativity in the table: arr is an array of
size 5 of an array of size 8 of int. */

int **ptr;
/* The two dereference operators have equal precedence, so
the associativity takes effect. The operators are applied
ina right-to-left order: ptr is a pointer to a pointer to an int.*/

```

#### Multiple Declarations

The comma can be used as a separator (**not** acting like the comma operator) in order to delimit multiple declarations within a single statement. The following statement contains five declarations:

```C
int fn(void), *ptr, (*fp)(int), arr[10][20], num;
```

objects declared above:

- fn: a function taking void and returning int;
- ptr: a pointer to an int;
- fp: a pointer to a function taking int and returning int;
- arr: an array of size 10 of an of array of size 20 of int;
- num: int.

#### Fixed Width Integer Types

The header `<stdin.h>` provides several fixed-width integer type definitions.

```C
/* commonly used types include */
uint32_t u32 = 32; // exactly 32-bits wide

uint8_t u8 = 255; // exactly 8-bits wide

int64_t i64 = -65 // exactly 64 bits in two's complement representation

```

#### Integer Types and Constants

Signed integers can be of these types (the int after short, or long is optional):

```C
signed char c = 127; // required to be 1 byte, see remarks for further info
signed short int si = 32767; // required to be at least 16 bits
signed in i = 32767; // required to be at least 16 bits
signed long int li = 2147483647; // required to be at least 64 bits

/* unsigned versions */
unsigned int i = 65635;
unsigned short = 2767;
unsigned char = 255;

```

For all the types but `char` the `signed` version is assumed if the `signed` or `unsigned` part is omitted. The type `char` constitutes a third character type, different from `signed char` and `unsigned char` and the signedness (or not) depends on the platform.

Different types of integer constants (called _literals_ in C jargon) can be written in defferent bases, and different wdith, based on their prefix or suffix.

```C
/* the following variables are initialized to the same value */
int d = 42; // decimal constant (base 10)
int o - 052; // octal constant (base 8)
int x = 0xaf; // hexadecimal constants (base16)
int X = 0XAf; // (letters 'a' through 'f' (case insensitive) represent 10 through 15)

```

Decimal constants are always signed. Hexadecimal constants start with 0x or 0X and octal constants start just with a 0. The latter two are `signed` or `unsigned` depending on whether the value fits into the signed type or not.

```C
/* suffixes to describe width and signedness : */
long int i = 0x32; // no suffix represent in, or long int
unsigned in ui = 65535u; // u or U represent unsigned int, or long int
long int li = 65536l; // l or L represent long int

```

Without a suffix the constant has the first type that fits its value, that is a decimal constant that is larger than INT_MAX is of type `long` if possible, or `long long` otherwise.

The header file `<limits.h>` describes the limits of integers as folows. Their implementation-defined values shall be equal or greater in magnitude (absolute value) to those shown below, with the same sign.

| Macro      | Type                                             | Value                             |
| ---------- | ------------------------------------------------ | --------------------------------- |
| CHAR_BIT   | smallest object that is not a bit-field (byte) 8 |
| SCHAR_MIN  | `signed char`                                    | -127 / -(27-1)                    |
| SCHAR_MAX  | `signed char`                                    | +127 / 27-1                       |
| UCHAR_MAX  | `unsigned char`                                  | 255 / 28-1                        |
| CHAR_MIN   | `char`                                           | see below                         |
| CHAR_MAX   | `char`                                           | see below                         |
| SHRT_MIN   | `short int`                                      | -32767 / -(215 -1)                |
| SHRT_MAX   | `short int`                                      | +32767 / 215 -1                   |
| USHRT_MAX  | `unsigned short int`                             | 65535 / 216 -1                    |
| INT_MIN    | `int`                                            | -32767 / -(215 -1)                |
| INT_MAX    | `int`                                            | +32767 / 215 -1                   |
| UINT_MAX   | `unsigned int`                                   | 65535 / 216 -1                    |
| LONG_MIN   | `long int`                                       | -2147483647 / -(231 - 1)          |
| LONG_MAX   | `long int`                                       | +2147483647 / 231 - 1             |
| ULONG_MAX  | `unsigned long int`                              | +2147483647 / 231 - 1             |
| LLONG_MIN  | `long long int`                                  | -9223372036854775807 / -(263 - 1) |
| LLONG_MAX  | `long long int`                                  | 9223372036854775807 / 263 - 1     |
| ULLONG_MAX | `unsigned long long int`                         | 18446744073709551615 / 264 - 1    |

If the value of an object of type `char` sign-extends when used in an expression, the value of CHAR_MIN shall be the same as that of SCHAR_MIN and the value of CHAR_MAX shall be the same as that of SCHAR_MAX. If the value of an object of type `char` does not sign-extend in an expression, the value of CHAR_MIN shall be 0 and the value of CHAR_MAX shall be the same as that of UCHAR_MAX.

C99 standard added a new header, `<stdint.h>`, which contains definitions for fixed width integers, the fixed width integer example for a more in-depth explanation.

#### Floating Point Constants

C lang has three mandatory real floating point types, `float`, `double`, `long double`.

```C
float f = 0.314f;        // suffix f or F denotes type float
double d = 0.314;        // no suffix denotes double
long double ld = 0.3141; // suffix l or L denotes long double

/* the different parts of a floating point definition are optional */
double x = 1.; // valid. fractional part is optional
double x = .1; // valid. whole-number part is optional

/* they can also be defined in scientific notation */
double sd = 1.2e3; // decimal fraction 1.2 is scaled by 10*3. that is 1200.0

```

Header `<float.h>` defines various limits for floating point operations.

#### String Literals

```C
char* str = "hello, world"; // string literal

/* string literals can be used to initialize arrays */
char a1[] = "abc"; // a1 is char[4] holding {'a','b','c','\0'}
char a2[4] = "abc"; // same as a1
char a3[3] = "abc"; // a1 iss char[3] holding {'a','b', 'c'}, missing the '\0'
```

String literals are **not modifiable** (and in fact may be placed in read-only memory such as .rodata). Attempting to alter their values results in undefined behavior.

```C
char* s = "foobar";
s[0] = 'F'; // undefined behavior

/* it's good practice to denote string literals such, by using 'const' */
char const* s1 = "foobar";
s1[0] = 'F'; // compiler error!

/* Multiple string literals are concatenated at compile time, which
means you can write construct like these */
/* pre C99 only two narrow or two wide string literals may be concatenated */
char* s1 = "Hello, " "World";

/* post C99 more than two can be concatenated
concatenation is implementation defined*/
char* s1 = "Hello" ", " "World";

/* common usage */
char* ftm = "%" PRId16; // PRId16 macro since C99

/* String literals, same as character constants, support different character sets */

/* normal string literal, of type char[] */
char* s1 = "abs";

/* wide character string literal, of type wchar_t[] */
wchar_t* s2 = L"abc";

// >= C11
/* UTF-8 string literal, of type char[] */
char* s3 = u8"abc";

/* 16-bit wide string literal, of type char16_t[] */
char16_t* s4 = u"abc";

/* 32-bit wide string literal, of type char32_t[] */
char32_t* s5 = U"abc";

```

### Operators

Symbol for mathematical, relational or logical operation.

Many C operators are binary operators, meaning they have two operands. So in `a / b`, `/` is a binary operator that takes two operands (a,b). Unary operators take one operand (e.g., ~ or ++). `? :` is the only ternary operator.

#### Relational Operator

Binary operator that checks for truth between two operands. Evaluated to 1 (true) or 0 (false).

##### Equal

```C
1 == 0;             // evaluates to 0
1 == 1;             // evaluates to 1

int x = f;
int y = 5;
int *xptr = &x, *yptr = &y;
xptr == yptr;    // evaluates to 0, operands hold different location addresses.
*xptr == *yptr;  // evaluates to 1, operands point at locations that hold the same value
```

##### Not Equal

```C
1 != 0;             // evaluates to 1
1 != 1;             // evaluates to 0

int x = f;
int y = 5;
int *xptr = &x, *yptr = &y;
xptr != yptr;    // evaluates to 1, operands hold different location addresses.
*xptr != *yptr;  // evaluates to 0, operands point at locations that hold the same value
```

`!` can also be applied directly to a variable. `!someVariable` is equivalent to `someVariable == 0`

##### Other

- `>`
- `<`
- `>=`
- `<=`

#### Conditional Operator/Ternary Operator

```C
a = b ? c : d;

// is equivalent to:

if (b)
    a = c;
else
    a = d;
```

Ternaries can be nested. The following program writes even and odd numbers to two separate files.

```C
#include<stdio.h>

int main() {
    FILE *even, *odds;
    int n = 10;
    size_t k = 0;

    even = fopen("even.md", "w");
    odds = fopen("odds.md", "w");

    for(k = 1; k < n + 1; k++) {
        k%2==0 ? fprintf(even, "\t%5d\n", k)
               : fprintf(odds, "\t%5d\n", k);
    }
    fclose(even);
    fclose(odds);

    return 0;
}
```

#### Bitwise Operators

Bitwise operators can be used to perform a bit level operation on variables. The six bitwise operators in C are:

| Symbol | Operator                      |
| ------ | ----------------------------- |
| &      | bitwise AND                   |
| \|     | bitwise inclusive or          |
| ^      | bitwise exclusive OR(XOR)     |
| ~      | bitwise not(one's complement) |
| <<     | logical left shift            |
| >>     | logical right shift           |

```C
#include <stdio.h>

int main(void) {
    unsigned int a = 29;    // 29 = 0001 1101
    unsigned int b = 48;    // 48 = 0011 0000
    int c = 0;

    c = a & b;              // 32 = 0001 0000
    printf("%d & %d = %d\n", a, b, c);

    c = a | b;              // 61 = 0011 1101
    printf("%d | %d = %d\n", a, b, c);

    c = a ^ b;              // 45 = 0010 1101
    printf("%d ^ %d = %d\n");

    c = ~a;                 // -30 = 1110 0010
    printf("~%d = %d\n". a. c);

    c = a << 2;             // 116 = 0111 0100
    printf("%d << 2 = %d\n", a, c);

    c = a >> 2;             // 7 = 0000 0111
    printf("%d >> 2 = %d", a, c);

    return 0
}
```

Bitwise operations with signed types should be avoided because the sign bit of such a bit representation has a particular meaning. Particular restrictions apply to the shift operators:

- Left shifting a 1 bit into the signed bit is erroneous and leads to undefined behavior.
- Right shifting a negative value (with sign bit 1) is implementation defined and therefore not portable.
- If the value of the right operand of a shift operator is negative or greater than or equal to the width of the promoted left operand, the behavior is undefined.

##### Masking

Masking refers to the process of extracting the desired bits from (or transforming the desired bits in) a variable by using logical bitwise operations. The operand (a constant or variable) that is used to perform masking is called a mask.

Masking is used in many different ways:

- To decide the bit pattern of an integer variable.
- To copy a portion of a given bit pattern to a new variable, while the remainder of the new variable is filled with 0s (using bitwise AND)
- To copy a portion of a given bit pattern to a new variable, while the remainder of the new variable is filled with 1s (using bitwise OR)
- To copy a portion of a given bit pattern to a new variable, while the remainder of the ordinal bit pattern is inverted with the new variable (using bitwise exclusive OR)

The following function uses a mask to display the bit pattern of a variable:

```C
#include <limits.h>
void bit_pattern(int u) {
    int i, x, word;
    unsigned mask = 1;
    word = CHAR_BIT * sizeof(int);
    mask = mask << (word - 1);    // shift 1 to the leftmost position
    for(i = 1; i<= word; i++) {
        x = (u & mask) ? 1 : 0;   // identify the bit
        printf("%d", x);          // print bit value
        mask >>= 1;               // shift mask to the right by 1 bit
    }
}
```
