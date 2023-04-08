# Learning Python

## Python Objects and Data Structures Basics

```python
2 + 3 # Addition
3 - 2 # Subtraction
3 * 2 # Multiplication
3 / 2 # Division
3 ** 2 # Exponential
3 % 2 # Modulo

value = 5
```

```python
# String Slicing with [Start : Stop : Step]

user = 'alex'
print(user[0:3])

# ale , Stop is not included.

print(user[::-1])

# Reverse a string

len(user)

# 4
```

### String Methods

```python
user = 'alex'

user.lower()
user.upper()

user.split() # Returns a list
```

### Print Formatting

```python
print('{0} {1} {2}'.format('one', 'two', 'three'))

print('{one} {two} {three}'.format(one = 'one', two = 'two', three = 'three'))

print('Result is {r:10.2f}'.format(r = result))

print('%s %s %s' %('one', 'two', 'three'))

print(f' {one} {two} {three}')
```

### Lists

```python
list_example = [1, 2, 3]

list_example[0]

# 1

list_example[:1]

# [1]

```

```python
list_another_example = ['b', 'a']

list_another_example.append('Value')

# It will add the value at end

list_another_example.pop()

# Returns last value which is removed

list_another_example.sort()

# Mutates original list, so returned type is None

list_another_example.reverse()

# Reverses the list,
```

### Dictionaries

```python
dict_example = {
  'key1' : 'value1',
  'key2' : 'value2'
}

dict_example['key1']

# value1

dict_example['key3'] = 'value3'

dict_example.keys()

# Returns keys

dict_example.values()

# Returns Values

dict_example.items()

# Returns all the items
```

### Tuples

Tuples are immutable, and have a pair of `()`.

```python
tuple_example = (1, 2, 3)

tuple_example.count(1)

# Count Number of 1's.

tuple_example.index(1)

# Return index of 1
```

### Sets

```python
set_example = Set()

set_example.add(1)

# {1}
```

### File I/O

```python
file_example = open('./file_example.txt')

file_example.read()

# Returns the file content

file_example.seek(0)

# Set cursor back to start

file_example.readlines()

# Returns a list of strings
```

```python
with open('./file_example.txt', mode='r') as file_example:
  file = file_example
```

## Python Statements

`if-elif-else` statements,

```python
user = 'root'

if user == 'root':
  print("Root user, you can access it.")
elif user == 'normal':
  print("Normal user, you can't access it.")
else:
  print("Please log in, as root user.")
```

`for` loops,

```python
list_example = [1, 2, 3]

for list_item in list_example:
  print(list_item)

for list_index in range(len(list_example)):
  print(list_example[list_index])

for list_item in enumerate(list_example):
  print(list_item)

# (0, 1) (1, 2) (2, 3)

list_example_one = [1, 2, 3]
list_example_two = [4, 5, 6]

for list_item in zip(list_example_one, list_example_two):
  print(list_item)

# (1, 4) (2, 5) (3, 6)
```

`while` loops,

```python
while True:
  print("Until it becomes False, it will loop over.")
```

`break` is used to exit out of the loop, `continue` is used to loop over from the start, and `pass` is used to simplt pass the execution.

### List Comprehension

```python
list_example = [letter for letter in 'helloworld']

# ['h', 'e', 'l', ...]
```
