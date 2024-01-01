# C Lang Notes

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

| Type    | Storage Size    | Value Range    |
|---------------- | --------------- | --------------- |
| char    | 1 byte    | -128 to 127 or 0 255    |
| unsigned char    | 1 byte    | 0 to 255    |
| signed char   | 1 byte   | -128 to 127   |
| int   | 2 or 4 bytes   | -32,768 to 32,767 or -2,147,483,648 to 2,147,483,647   |
| unsigned int   | 2 or 4 bytes   | 0 to 65,535 or 0 to 4,294,967,295   |
| short   | 2 bytes   | -32,768 to 32,767   |
| unsigned short   | 2 bytes   | 0 to 65,535   |
| long   | 8 bytes   | -9223372036854775808 to 9223372036854775807  |
| unsigned long   | 8 bytes   | 0 to 18446744073709551615   |

#### Floating-Point Types

| Type    | Storage Size    | Value Range    | Precision    |
|---------------- | --------------- | --------------- | --------------- |
| float    | 4 byts    | 1.2E-38 to 3.4E+38    | 6 decimal places    |
| double    | 8 bytes   | 2.3E-308 to 1.7E+308   | 15 decimal places   |
| long double   | 10 bytes   | 3.4E-4932 to 1.1E+4932   | 19 decimal places   |

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
| Escape Sequence   | Meaning    |
|--------------- | --------------- |
| \\\   | \ character   |
| \\'   | ' character   |
| \\"   | " character   |
| \\?   | ? character   |
| \a   | Alert or bell   |
| \b   | Backspace   |
| \f   | Form feed   |
| \n   | Newline   |
| \r   | Carriage return   |
| \t   | Horizontal tab   |
| \v   | Vertical tab   |
| \ooo   | Octal number of on to three digits   |
| \xhh   | Hecadecimal number of one or more digits   |

### Interpreting Decarations

Operators with identical precedence
- unary * "dereference" operator which denots a pointer
- binary [] "array subscription" operator denotes an array
- (1+n)-ary () "function call" operator denotes a function
- () grouping parentheses override the precedence and associativity of the rest of the listed operators

| Operator    | Relative Precedence    | Associativity    |
|---------------- | --------------- | --------------- |
| [] (array subscription)    | 1    | Left-to-right    |
| () (function call)    | 1    | Left-to-right    |
| * (dereference)   | 2   | Right-to-left   |

| Expression   | Interpretation    |
|--------------- | --------------- |
| thing[x]   | an array of size X of...   |
| thing(t1, t2, t3)   | a function taking t1, t2, t3 and returning   |
| *thing   | a pointer to...   |

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
// fp is a pointer to a functino taking void and
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




