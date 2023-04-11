# Learning C

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
