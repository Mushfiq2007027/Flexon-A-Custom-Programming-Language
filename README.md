<div align="center">

# Flexon
### A Custom Interpreted Programming Language

*Built with Flex & Bison · Designed from scratch · Runs on C*

![Language](https://img.shields.io/badge/Language-C-blue?style=flat-square&logo=c)
![Lexer](https://img.shields.io/badge/Lexer-Flex-orange?style=flat-square)
![Parser](https://img.shields.io/badge/Parser-Bison-green?style=flat-square)
![Platform](https://img.shields.io/badge/Platform-Linux%20%7C%20Windows-lightgrey?style=flat-square)
![License](https://img.shields.io/badge/License-MIT-yellow?style=flat-square)

</div>

---

## Overview

**Flexon** is a fully custom-designed interpreted programming language built using **Flex** (lexical analyzer) and **Bison** (parser generator). It features its own unique syntax, supports common programming constructs like conditionals, loops, functions, and type declarations, and comes equipped with built-in mathematical utilities.

This project was developed as part of a **Compiler Design** course, demonstrating end-to-end language implementation — from tokenization and grammar parsing to runtime expression evaluation.

---

## Features

- **Custom Syntax** — Unique, human-readable keywords (`iff`, `elif`, `rtn`, `show`, `take`, etc.)
- **Data Types** — `integer`, `float`, `character`, `double`
- **I/O Operations** — `show()` for output, `take()` for input
- **Control Flow** — `iff / elif / else`, `switch / case / default`
- **Loops** — `for` and `while` with range-based syntax
- **Math Functions** — `sin`, `cos`, `tan`, `log`, `squaroot`, `power`, `gcd`, `prime`, `evenodd`, `factorial`
- **User-Defined Functions** — via the `func` keyword
- **Directives** — include external files like `directive <stdio.h>`
- **Block Comments** — `**- your comment here -**`
- **Error Handling** — detects undeclared variables, duplicate declarations, and invalid syntax


## Flexon Language Syntax Reference

### Program Structure

Every Flexon program begins with `function main()`, includes directives, and wraps the body between `start` and `end`.

```flexon
function main()
directive <stdio.h>
directive <stdlib.h>

start
    **- your code goes here -**
    rtn;
end
```

---

### Data Types & Declarations

```flexon
integer x = 10;
float pi = 3.14;
character ch;
double d = 9.99;
integer a, b, c;       **- multiple declarations -**
```

---

### Input / Output

```flexon
take(x);               **- reads integer input into x -**
show(x);               **- prints value of x -**
show("Hello World");   **- prints a string literal -**
show(x + y * 2);       **- prints expression result -**
```

---

### Arithmetic & Comparison Operators

| Operator  | Symbol | Example   |
|-----------|--------|-----------|
| Add       | `+`    | `a + b`   |
| Subtract  | `-`    | `a - b`   |
| Multiply  | `*`    | `a * b`   |
| Divide    | `/`    | `a / b`   |
| Greater   | `gt`   | `a gt b`  |
| Less      | `lt`   | `a lt b`  |
| Equal     | `eq`   | `a eq b`  |
| Not Equal | `neq`  | `a neq b` |

---

### Conditional Statements

```flexon
iff <x gt 5>
{
    show(x);
}
elif <x eq 5>
{
    show("x is five");
}
else
{
    show("x is less than five");
}
```

---

### Switch-Case

```flexon
switch <x> :
start
    case (1 + 1) :
        x = 100
        break

    case (2 + 2) :
        x = 200
        break

    default :
        x = 999
        break
end
```

---

### Loops

**For Loop** (range-based):
```flexon
for i : 1 to 5
start
    show(i);
end
```

**While Loop** (comparison-based):
```flexon
while <1 lt 10>
start
    integer counter;
end
```

---

### Built-in Mathematical Functions

```flexon
prime(17);            **- checks if 17 is prime -**
evenodd(8);           **- checks even or odd -**
factorial(6);         **- computes 6! -**
sin(90);              **- sine of 90 degrees -**
cos(45);
tan(45);
log(100);
squaroot(144);        **- square root -**
power(2, 10);         **- 2^10 -**
gcd(48, 18);          **- greatest common divisor -**
```

---

### User-Defined Functions

```flexon
func myFunc(integer n)
{
    show(n);
}
```

---

### Comments

Flexon supports block-style comments using the `**-...-**` delimiter:

```flexon
**- This is a comment -**
```

---

## Getting Started

### Prerequisites

Make sure the following tools are installed on your system:

| Tool  | Purpose                       | Install Command (Ubuntu/Debian) |
|-------|-------------------------------|----------------------------------|
| Flex  | Lexical analyzer generator    | `sudo apt install flex`          |
| Bison | Parser generator (LALR)       | `sudo apt install bison`         |
| GCC   | C compiler to link everything | `sudo apt install gcc`           |

> **Windows users:** Use [WSL](https://learn.microsoft.com/en-us/windows/wsl/) or [MinGW](https://www.mingw-w64.org/) and ensure `flex`, `bison`, and `gcc` are accessible from the terminal.

---

### Build & Run

Open your terminal in the project directory and run the following commands **in order**:

```bash
# Step 1: Generate the parser (tab.c and tab.h) from the Bison grammar file
bison -d mushfiq027.y

# Step 2: Generate the lexer (lex.yy.c) from the Flex specification
flex mushfiq027.l

# Step 3: Compile both generated files with GCC
gcc mushfiq027.tab.c lex.yy.c -o output -lm

# Step 4: Run the compiler on your Flexon source code
./output
```

> The program reads from `input.txt` and writes the result to `output.txt` automatically.

---

## Sample Program

**`input.txt`**
```flexon
function main()
directive <stdio.h>

start
    integer x = 10;
    integer y = 3;
    integer result;

    result = x + y;
    show(result);

    iff <x gt y>
    {
        show("x is greater");
    }
    else
    {
        show("y is greater");
    }

    prime(13);
    squaroot(49);
    power(2, 8);

    rtn;
end
```

**`output.txt`**

Directive Included
x declared with value 10
y declared with value 3
result declared
13 is assigned to result
Value of result is : 13
If block: True
printed: x is greater
If block executed
13 is a prime number.
square root of 49 is 7.000000
power of 2^8 is 256
Succesfully Compiled!




## Known Limitations

- All variables are stored as integers internally; float support is partial
- No support for string variables (only string literals in `show()`)
- User-defined function calls with return values are not fully implemented
- No nested loop support beyond one level
- `for` loop variable does not auto-iterate the body with the loop variable's value

---



