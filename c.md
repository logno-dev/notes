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


