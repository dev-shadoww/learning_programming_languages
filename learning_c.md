# Learning C

## Dynamic memory allocation

The routines for dynamic memory allocation are defined in `stdlib.h`, the function are `malloc`, `calloc` and `realloc`, each of these functions returns a `void*` pointer to a block of memory in the heap space.

`void*` is a pointer type that is of an unknown or generic type; a pointer of the `void*` type must be cast to the required pointer type before you can use that pointer.

```c
int *int_first_ = (int *)malloc(sizeof(int));
*int_first = 3;
```

```c
free(int_first);
```

## Formatted output

It begins with the `%` character and has the following elements,

Zero or more flag characters:

- Left-aligned: This is the - character. If missing, the value will be right-aligned.
- The `+` sign to show a positive or negative value, or a space to only show a `–` sign.
- Zero-padding: 0.
- A variant of formatting: This is the # character; the variant depends on the conversion type.Revisiting printf()

An optional minimum field width denoted by a decimal integer constant. 3. An optional precision specification denoted by a period (.) and optionally followed by a decimal integer constant.

An optional size modifier is expressed as one of the following letters:

- Long or long-long: l, ll, or L
- Short or byte: h or hh
- Specific type: j, z, or t

The conversion operation, which is a single character that may be one of

- An unsigned integer: d, i, o, u, x, or X
  the following:
- A pointer: n or p
- A signed integer: d or i
- A floating-point: a, A, e, E, f, F, g, or G
- A character (c) or string (s)
- The % character itself

## Input from command line

The `main()` has two forms, the program name itself is always placed in `argv[0]`. Therefore, argc will always be at least 1.

```c
void main(void);
void main(int argc, char *argv[]);
```

## Building Multi File Programs With Make

```bash
gcc -c a.c -wall -werror -std=c17
gcc -c b.c -wall -werror -std=c17
```

```bash
gcc a.o b.o -o last
```

`make` operates on a file named `makefile` or `Makefile` where the rules are specified by user.

Simply calling `make` is similar to,

```bash
make -f makefile
```

```make
CC = gcc
CCFLAGS = -wall -werror -std=c17

target: a.c b.c
  $(CC) a.c b.c -o target $(CCFLAGS)
```

Special macros,

- `$@` - FileName of the target
- `$<` - FileName of the first dependency
- `$^` - A space-separated list of all dependencies; duplicates are removed

We can change the `makefile` as,

```make
target: a.c b.c
  $(CC) $^ -o $@ $(CCFLAGS)
```

### Creating Rules

It consist of,

`target: dependency`

`action`

Each action line begins with `tab`. Here `SRCS` is macro for source files and `INCS` is macro for header files.

```make
CC = gcc
CCFLAGS = -wall -werror -std=c17
SRCS = a.c b.c
INCS = a.h
LDLIBS =

target: $(SRCS) $(INCS)
  $(CC) $(SRCS) -o target $(CCFLAGS)
```

```make
.PHONY: clean
clean:
  rm -f *.o dealer
.PHONY: run
run:
  dealer
```
