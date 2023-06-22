# Learning C

## Types

- Basic types
  - Standard and extended integer types
  - Real and complex floating-point types
- Enumerated types
- The type void
- Derived types
  - Pointer types
  - Array types
  - Structure types
- Union types
- Function types

The `basic types` and the `enumerated types` together make up the arithmetic types. The `arithmetic types` and the `pointer types` together are called the scalar types. `Array types` and `structure types` are referred to collectively as the aggregate types.

### Integer Types

- signed char
- int, signed, signed int
- short, short int, signed short, signed short int
- long, long int, signed long, signed long int
- long long (C99) long long int, signed long long, signed long long int

`Unsigned Types`,

- \_Bool, bool (defined in stdbool.h )
- unsigned char
- unsigned int, unsigned
- unsigned short, unsigned short int
- unsigned long, unsigned long int
- unsigned long long, unsigned long long int

The `char` type holds 1 byte of data.

To obtain the exact size of a type or variable, use the `sizeof` operator.

```c
sizeof(char);
```

### Integer Types In Standard Headers

The types ptrdiff_t, size_t, and wchar_t are defined in the header stddef.h (and in other headers); the types char16_t and char32_t are defined in the header uchar.h. For special requirements, integer types with specifed bit widths, in signed and unsigned variants, are defined in the header stdint.h.

- intN_t, uintN_tAn, integer type whose width is exactly N bits, Optional
- int_leastN_t, uint_leastN_t, An integer type whose width is at least N bits, Required for N = 8, 16, 32, 64
- int_fastN_t, uint_fastN_t, The fastest type to process whose width is at least N bits, Required for N = 8, 16, 32, 64
- intmax_t, uintmax_t, The widest integer type implemented, Required
- intptr_t, uintptr_t, An integer type wide enough to store the value of a pointer, Optional

### Floating Point Types

- float, For variables with single precision
- double, For variables with double precision
- long double, For variables with extended precision

### Enumerated Types

The definition of an enumeration begins with the keyword enum, possibly followed by an identifier for the enumeration, and contains a list of the type’s possible values, with a name for each value.

```c
enum identifier {enumerator_list};
```

### Void Type

The type specifier void indicates that no value is available. It can be used in functions to indicate there is no return value or in function parameter to indicate the function doesn't take any arguments.

### Alignment Of Objects

The alignment of a type is expressed as a number of bytes equal to the minimum distance between two objects of that type in storage.

There are operators such as `_Alignof` to determine alignment, `_Alignas` to specify alignment.

An alignment value less than or equal to `_Alignof(max_align_t)` is called a fundamental alignment. If it is greater then it is called as extended alignment.

```c
_Alignof(int)
_Alignas(4) short var;
```
