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
  print('Root user, you can access it.')
elif user == 'normal':
  print('Normal user, you can't access it.')
else:
  print('Please log in, as root user.')
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
  print('Until it becomes False, it will loop over.')
```

`break` is used to exit out of the loop, `continue` is used to loop over from the start, and `pass` is used to simplt pass the execution.

### List Comprehension

```python
list_example = [letter for letter in 'helloworld']

# ['h', 'e', 'l', ...]
```

## Methods

```python
help(list_example.append)
```

```python
def greet(user):
  """
  Greets the user.
  """
  print(f'Hello {user}')
```

### Tuple Unpacking

```python
list_tuple_example = [(1, 'a'), (2, 'b')]

for (a, b) in list_tuple_example:
  print(a, b)
```

### args and kwargs

```python
def print_values(*args):
  print(args)

print_values(1, 2, 3, 4)

# 1, 2, 3, 4
```

```python
def print_values(**kwargs):
  print(kwargs)

print_values(a = 1, b = 2)

# {'a' : 1, 'b' : 2}
```

### Map and Filter

`Map`,

```python
def square(n):
  return n ** 2

list_example = [1, 2, 3]

for item in map(square, list_example):
  print(item)

list(map(square, list_example))
```

`Filter`,

```python
def is_even(n):
  return n % 2 == 0

list_example = [1, 2, 3]

list(filter(is_even, list_example))

# [2]
```

`Lambda Expression`,

```python
lambda_example = lambda n : n ** 2
```

## Object Oriented Programming

```python
class GreetUsers():
  def __init__(self, root, normal):
    self.root = root
    self.normal = normal

  def sayHello(self):
    print(f'Hello {self.root}, {self.normal}!')

user = GreetUser('Alex', 'Amit')

user.sayHello()

# Hello Alex, Amit!
```

### Inheritance and Polymorphism

```python
class GreetSimple(GreetUser):
  def __init__(self, user):
    self.user = user

  def sayHello(self):
    print(f'Hello there, {self.user}')

user = GreetSimple()

# Now the GreetSimple (Child class) inherits all the properties and methods from GreetUser class (Parent class)

# Polymprphism allows us to write different function definations with same name
```

## Modules and Packages

In python `pip` is used install packages created by others.

```bash
pip install requests
```

### Organising Files

```python
# pwd - Documents
# It has `main.py` and then `mainPackage` directory, now
# create a `__init__.py` file in that directory, now python
# will treat it as a module, and create `subPackages` directory
# in that and create another `__init__.py`, now create python
# scripts,

from mainPackage import main_function

from mainPackage.subPackage import sub_function
```

```python
# The name of python file is assigned to `__name__` and if it's
# equal to `__main__` then it will be executed.

if __name__ == '__main__':
  main()
```

## Error Handling

```python
try:
  file_example = open('./file.txt')
except:
  print('File not found.')
else:
  print('Running \'else\' block.')
finally:
  print('I always run.')
```

### Pylint and Unitest

`Pylint` can be used to get a full report on a python script.

`main.py`

```python
def square(n):
  return n ** 2
```

`script.py`

```python
import unitest
import main

class test_square(unitest.TestCase):
  def check_square(self):
    value = 2
    result = main.square(value)
    self.assertEqual(result, 4)

if __name__ == '__main__':
  unitest.main()
```

## Decorators and Generators

`Decorators`,

```python
def decorator_function(original_function):
  def wrap_function():
    print('Code before original_function.')

    original_function()

    print('Code after original_function.')

  return wrap_function

def original_function():
  print('Need to decorate.')

after_decoration = decorator_function(original_function)

# Or

@decorator_function
def original_another_function():
  print('It also need to decorate.')
```

`Generators`,

```python
def squares(n):
  for i in range(n):
    yield i ** 2

list(square(4))

# [1, 4, 9, 16]

generator_square = squares(n)

print(next(generator_square))

user = 'root'
genrator_sequence = iter(user)

print(next(generator_sequence))
```

## Advanced Python Modules

### `collections module`

```python
from collection import counter, defaultdict, namedtuple

list_example = [1, 1, 1, 2, 2]

counter(list_example)

# {1 : 3, 2 : 2}

counter_example = counter(list_example)

counter_example.most_common()

# {1 : 3, 2 : 2}
```

`defaultdict`,

```python
default_dict_example = defaultdict(lamda : 0)

default_dict_example['key_not_found']

# 0
```

`namedtuple`

```python
named_tuple_example = namedtuple('named_tuple_example', ['value'])

tuple_example = named_tuple_example(value = 5)

tuple_example

# named_tuple_example(value = 5)

tuple_example.value

# 5
```

### `os module`

```python
import os

os.getcwd()

# print pwd

os.listdir()

# list all items in pwd

os.rmdir()

# Deletes directory

os.unlink(path)

# Deletes file

os.walk()

# Generate directory tree

for folder, sub_folders, files in os.walk(path):
  print(folder)
  for sub_folder in sub_folders:
    print(sub_folder)
  for file in files:
    print(file)
```

### `shutil module`

```python
import shutil

shutil.move(source, destination)

shutil.rmtree(path)
```

### `datetime module`

```python
import datetime

time_example = datetime.time(2, 20, 2, 2)

time_example.hour

# 2

time_example.minutes

# 20

print(time_example)

# 02:20:02.000002
```

```python
date_example = datetime.date.today()

date_example.ctime()

# Fri Jun 12 00:00:00 2023

datetime_example = datetime(2023, 4, 9, 11, 39, 2)

# Year, Month, Date, Hour, Minute, Second, Micro Second

datetime_example.replace()
```

```python
from datetime import date

date_example = date(2023, 4, 9)
```

## `math and random module`

```python
import math

help(math)

# For all the available methods

math.floor()

math.ceil()

round()

math.e

math.pi

math.log()
```

```python
import random

random_example = random()

random_example.randint(0, 100)

# Generate random integers between 0, 100, including both

random_example.choice(list_example)
```
