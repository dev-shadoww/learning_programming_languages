# Learning C++

In C and C++ the program execution starts from function called `main`,

A function definition has four elements: a `return type`, a `function name`, a (possibly empty) `parameter list` enclosed in parentheses, and a `function body`.

```cpp
int main() {
  return 0;
}
```

Program files are normally referred to as a source files. To execute a C++ program,

```bash
g++ source_file.cpp
```

## Variables and data types

The data types are,

- `bool` - Boolean,
- `char` - Character,
- `wchar_t` - wide character,
- `char16_t` - Unicode character,
- `char32_t` - Unicode character,
- `short` - short integer,
- `int` - integer,
- `long` - long integer,
- `long long` - long integer,
- `float` - single-precision floating-point,
- `double` - double-precision floating-point,
- `long double` - extended-precision floating-point.

A `signed type` represents negative or positive numbers (including zero); an `unsigned type` represents only values greater than or equal to zero.

A value, such as 42, is known as a `literal` because its value self-evident.

`20 /* decimal */ 024 /* octal */ 0x14 /* hexadecimal */`

Escape sequences,

- `newline` - \n
- `vertical tab` - \v
- `backslash` - \\\
- `carriage return` - \r
- `horizontal tab` - \t
- `backspace` - \b
- `question mark` - \?
- `formfeed` - \f
- `alert (bell)` - \a
- `double quote` - \"
- `single quote` - \’

A `variable` provides us with named storage that our programs can manipulate.

```cpp
int evenNumber; // Declaration
evenNumber = 2; // Assignment

int oddNumber = 1; // Initialization
```
