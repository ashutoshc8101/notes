# Python in Depth 
derived from [docs.python.org](https://docs.python.org/3/tutorial/)

#### Small points
`//` - floor division, discards fractional part
`_` variable stores last printed expression value in python interpreter
Python supports complex numbers `a = 2 + 3j`

If you donot want to use special characters, you can use  r before string. It will make raw string.
String literals can span multiple lines, so you can use `"""...."""`, `'''....'''` (triple quotes)

`3 * string` makes, repeats sring 3 times
String next to each other are automatically concatenated
``` Python
>>> 'Py' 'thon'
'Python'
```
0 and -0 are same in indexing, negative indexing starts from -1

Python strings cannot be changed -- they are *immutable*. 
Assigning to an indexed position in the string results in an error.

#### List
list is used to group data, it can contain different types
Lists support concatenation, 
```Python
if [1,2,3] + [4,5,6] == [1,2,3,4,5,6]:
    pass
```
new items can be added using append() method.

***Assignment to slices is also possible.***
```Python
>>> letters = ['a', 'b', 'c', 'd', 'e', 'f', 'g']
>>> letters
   ['a', 'b', 'c', 'd', 'e', 'f', 'g']
>>> # replace some values
>>> letters[2:5] = ['C', 'D', 'E']
>>> letters
    ['a', 'b', 'C', 'D', 'E', 'f', 'g']
>>> # now remove them
>>> letters[2:5] = []
>>> letters
    ['a', 'b', 'f', 'g']
>>> # clear the list by replacing all the elements with an empty list
>>> letters[:] = []
>>> letters
    []
```
It is possible to created nested lists

#### Control Flow:

- Python doesnot have switch statement.
- Ternary operator `value1 if condition else value2`.

***Code that modifies a collection while iterating over that collection can be tricky to get right.***
```Python
# Strategy:  Iterate over a copy
for user, status in users.copy().items():
    if status == 'inactive':
        del users[user]

# Strategy:  Create a new collection
active_users = {}
for user, status in users.items():
    if status == 'active':
        active_users[user] = status
```
Just like list, `range(n)` is iterable
```Python
>>> sum(range(4))  # 0 + 1 + 2 + 3
6
>>> list(range(4))
[0, 1, 2, 3]
```
***pass Statements***

The pass statement does nothing. It can be used when a statement is required syntactically 
but the progra required no action.
```Python
>>> while True:
...     pass  # Busy-wait for keyboard interrupt (Ctrl+C)
...
```

This is commonaly used for creating minimal classes.
```Python
>>> class MyEmptyClass:
...     pass
```
When defining functions
```Python
>>> def initlog(*args):
		pass
```
two variables can be assigned in one statement.
```Python
>>> a, b = 0, 1
a,b=b,a (swapping without third variable)
```

- Even functions without a return value do return a value that is `None`

***Important warning: The default value is evaluated only once. This makes a difference when the default is a mutable object such as a list, dictionary, or instances of most classes. For example, the following function accumulates the arguments passed to it on subsequent calls:***
#### Keyword Arguments
```Python
def parrot(voltage, state='a stiff', action='voom', type='Norwegian Blue'):
    print("-- This parrot wouldn't", action, end=' ')
    print("if you put", voltage, "volts through it.")
    print("-- Lovely plumage, the", type)
    print("-- It's", state, "!")
```

Functions can also be called using keyword arguments of the form kwarg=value
```Python
parrot(1000)                                          # 1 positional argument
parrot(voltage=1000)                                  # 1 keyword argument
parrot(voltage=1000000, action='VOOOOOM')             # 2 keyword arguments
parrot(action='VOOOOOM', voltage=1000000)             # 2 keyword arguments
parrot('a million', 'bereft of life', 'jump')         # 3 positional arguments
parrot('a thousand', state='pushing up the daisies')  # 1 positional, 1 keyword
```

Following calls are invalid:
```Python
parrot()                     # required argument missing
parrot(voltage=5.0, 'dead')  # non-keyword argument after a keyword argument
parrot(110, voltage=220)     # duplicate value for the same argument
parrot(actor='John Cleese')  # unknown keyword argument
```
***\*arguments receives a list of tuples (args)***

***\**keywords receives dictionary of arguments (kwargs)***

- A function defination may look this:
 ```Python
def f(pos1, pos2, /, pos_or_kwd, *, kwd1, kwd2):
      -----------    ----------     ----------
        |             |                  |
        |        Positional or keyword   |
        |                                - Keyword only
         -- Positional only
         
>>> def standard_arg(arg):
...     print(arg)
...
>>> def pos_only_arg(arg, /):
...     print(arg)
...
>>> def kwd_only_arg(*, arg):
...     print(arg)
...
>>> def combined_example(pos_only, /, standard, *, kwd_only):
...     print(pos_only, standard, kwd_only)
>>> pos_only_arg(1)
1

>>> pos_only_arg(arg=1)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: pos_only_arg() got an unexpected keyword argument 'arg'
```
***Unpacking argument list***
```Python
args = [3,6]
list(range(*args))
```
***dictionaries can unpacked with ** operator***
```Python
d = {'volatage': 'four million', 'state': 'bleding\' demised'}
func(**d) 
# is same as calling with keywords
func(voltage='four million', state='bleeading\ demised')
```
#### Lambda expressions:
Small anonymous functions can be created with the lambda keyword.

```Python
# example
sum = lambda a,b: a+b
```

#### Ternary operator like functionality in python
```Python
# syntax value1 if condition else vale2
greatest = lambda a,b: a if a > b else b
```

## PEP 8

For Python, PEP 8 has emerged as the style guide that most projects adhere to.

***Important points about PEP 8.***
- 4 spaces for indentation
- Wrap lines so that they don't exceed 79 characters.
- Use blank lines to seperate functions and classes, and larger blocks of code inside functions.
- When possible, put comments on a line of their own.
- Use docstrings
- Use spaces around operators and after commas
- Convention for class name is UpperCamelCase and for functions and methods is lowercase_with_underscores
- Always use self as the name for the first method argument
- Don't use fancy encodings if your code is meant to be used in international environment. Python's default is UTF-8
- Don't use non-ASCII characters in identifiers if there is only the slightest chance people speaking a different language will read or maintain code.
        
## Data Structures    
#### List
Here are all of the methods of list objects:
- `list.append(x)`
- `list.extend(iterable)`
- `list.insert(i,x)` The first argument is index of element before which to insert.
- `list.remove(x)` Removes first item whose value is equal to x
- `list.pop(x)` Removes item at given position and returns it
- `list.clear()` Removes all elements from the list
- `list.index(x[, start[, end]])` Return zero-based index in the list of first item equal to x
- `list.count(x)` Return number of times x appears in the list
- `list.sort(*, key=None, reverse=False)` Sort the items of the list in place
- `list.reverse()` Reverse the elements of the list in place
- `list.copy()` Return a shallow copy of the list. Equivalent to a[:]
```Python
# Example
>>> fruits = ['orange', 'apple', 'pear', 'banana', 'kiwi', 'apple', 'banana']
>>> fruits.count('apple')
2
>>> fruits.count('tangerine')
0
>>> fruits.index('banana')
3
>>> fruits.index('banana', 4)  # Find next banana starting a position 4
6
>>> fruits.reverse()
>>> fruits
['banana', 'apple', 'kiwi', 'banana', 'pear', 'apple', 'orange']
>>> fruits.append('grape')
>>> fruits
['banana', 'apple', 'kiwi', 'banana', 'pear', 'apple', 'orange', 'grape']
>>> fruits.sort()
>>> fruits
['apple', 'apple', 'banana', 'banana', 'grape', 'kiwi', 'orange', 'pear']
>>> fruits.pop()
'pear'
```

- Some methods like `list`, `remove` or `sort` that only modify the list have no return value. This is a design principle for all mutable data strucutres in python
- Not all data can be sorted or compared. `[None, 'hello', 10]` cannot be sorted or compared.
- `3 + 4j < 5+7j` is not a valid comparison

#### Using Lists as Stacks (Last In First Out)
- To add item, use append()
- To remove item, use pop()
```Python
>>> stack = [3, 4, 5]
>>> stack.append(6)
>>> stack.append(7)
>>> stack
[3, 4, 5, 6, 7]
>>> stack.pop()
7
>>> stack
[3, 4, 5, 6]
>>> stack.pop()
6
>>> stack.pop()
5
>>> stack
[3, 4]
```

#### Using Lists as Queues (First In First Out)
- It can be done using list, but it is not efficient.
- While append and pop from the end of list are very fast, doing inserts or props for beggining of list is slow.
- To implement a queue , use collections.deque which was designed to have fast appends and pops from both ends.
```Python
# Example deque
>>> from collections import deque
>>> queue = deque(["Eric", "John", "Michael"])
>>> queue.append("Terry")           # Terry arrives
>>> queue.append("Graham")          # Graham arrives
>>> queue.popleft()                 # The first to arrive now leaves
'Eric'
>>> queue.popleft()                 # The second to arrive now leaves
'John'
>>> queue                           # Remaining queue in order of arrival
deque(['Michael', 'Terry', 'Graham'])
```

#### List Comprehensions
List comprehensions provide concise way to create lists. Commn applications are to make new lists where each element is result of some operations applied to each member of another sequence or iterable.

***Three ways to create new list which square of given list.***
- Using for loop:
```Python
numbers = [1,2,3,4,5]
squared_numbers = []
for num in numbers:
	squared_numbers.append(num**2)
```
- Using map function
```Python
numbers = [1,2,3,4,5]
squared_numbers = list(map(lambda x: x**2, numbers))
```
- Using list comprehensions
```Python
numbers = [1,2,3,4,5]
squared_numbers = [x**2 for x in numbers]
```
- if can be used in list comprehension
```Python
only_even = [x for x in range(11) if x%2==0]
```

- Some more examples
```Python
>>> vec = [-4, -2, 0, 2, 4]
>>> # create a new list with the values doubled
>>> [x*2 for x in vec]
[-8, -4, 0, 4, 8]
>>> # filter the list to exclude negative numbers
>>> [x for x in vec if x >= 0]
[0, 2, 4]
>>> # apply a function to all the elements
>>> [abs(x) for x in vec]
[4, 2, 0, 2, 4]
>>> # call a method on each element
>>> freshfruit = ['  banana', '  loganberry ', 'passion fruit  ']
>>> [weapon.strip() for weapon in freshfruit]
['banana', 'loganberry', 'passion fruit']
>>> # create a list of 2-tuples like (number, square)
>>> [(x, x**2) for x in range(6)]
[(0, 0), (1, 1), (2, 4), (3, 9), (4, 16), (5, 25)]
>>> # the tuple must be parenthesized, otherwise an error is raised
>>> [x, x**2 for x in range(6)]
  File "<stdin>", line 1, in <module>
    [x, x**2 for x in range(6)]
               ^
SyntaxError: invalid syntax
>>> # flatten a list using a listcomp with two 'for'
>>> vec = [[1,2,3], [4,5,6], [7,8,9]]
>>> [num for elem in vec for num in elem]
[1, 2, 3, 4, 5, 6, 7, 8, 9]
```


#### Nested Comprehensions
The initial expresssion in  list comprehension can be any arbitrary expresssion, including another list comprehension.

```Python
# Transpose matrix example
>>> matrix = [
...     [1, 2, 3, 4],
...     [5, 6, 7, 8],
...     [9, 10, 11, 12],
... ]
>>> [[row[i] for row in matrix] for i in range(4)]
[[1, 5, 9], [2, 6, 10], [3, 7, 11], [4, 8, 12]]
```

#### The del statement
`del` statement is used to remove element from list using its index.
pop(index) removes one element, del can be used remove slices also
```Python
#example
>>> a = [-1, 1, 66.25, 333, 333, 1234.5]
>>> del a[0]
>>> a
[1, 66.25, 333, 333, 1234.5]
>>> del a[2:4]
>>> a
[1, 66.25, 1234.5]
>>> del a[:]
>>> a
[]
```

`del` can also be used to delete entire variables
```Python
del a
```
Referencing the name a hereafter is an error

#### Tuples and Sequences
Tuples are immutable unlike lists
Empty tuples are created using empty paranthesis
```Python
# Empty tuple
t = ()
```
Tuple containing one element is created using value followed by ,
```Python
singleton = 'hello',
```
The statement t = 12345, 54321, 'hello!' is an example of tuple packing
`x, y, z = t` Reverse is also possible
`a,b = 5, 10` is just a combination of tuple packing and unpacking.

#### Sets
A set is an unordered collection with no duplicate elements.
Set objects aalso support mathematical operators like union, intersection, difference and symmetric difference

```Python
# Set example
>>> basket = {'apple', 'orange', 'apple', 'pear', 'orange', 'banana'}
>>> print(basket)                      # show that duplicates have been removed
{'orange', 'banana', 'pear', 'apple'}
>>> 'orange' in basket                 # fast membership testing
True
>>> 'crabgrass' in basket
False

>>> # Demonstrate set operations on unique letters from two words
...
>>> a = set('abracadabra')
>>> b = set('alacazam')
>>> a                                  # unique letters in a
{'a', 'r', 'b', 'c', 'd'}
>>> a - b                              # letters in a but not in b
{'r', 'd', 'b'}
>>> a | b                              # letters in a or b or both
{'a', 'c', 'r', 'd', 'b', 'm', 'z', 'l'}
>>> a & b                              # letters in both a and b
{'a', 'c'}
>>> a ^ b                              # letters in a or b but not both
{'r', 'd', 'b', 'm', 'z', 'l'}
```

#### Dictionaries
- It is best to think of a dictionary as a set of key: value pairs, with the requirement that the keys are unique (within one dictionary). 
- Dictionaries are indexed using keys, which can be any immutable type, strings and numbers can always be keys.
- Tuples can be used as keys if they contain only immutable types.
- You can't use lists as keys, as they mutuable.
- You can use delete a key:value pair with `del`
- Performing `list(d)` on a dictionary returns a list of all the keys, in insertion order.
- To check wheather a single key is in the dictionary use the `in` keyword

```Python

>>> tel = {'jack': 4098, 'sape': 4139}
>>> tel['guido'] = 4127
>>> tel
{'jack': 4098, 'sape': 4139, 'guido': 4127}
>>> tel['jack']
4098
>>> del tel['sape']
>>> tel['irv'] = 4127
>>> tel
{'jack': 4098, 'guido': 4127, 'irv': 4127}
>>> list(tel)
['jack', 'guido', 'irv']
>>> sorted(tel)
['guido', 'irv', 'jack']
>>> 'guido' in tel
True
>>> 'jack' not in tel
False

```
- The `dict()` constructor builds dictionaries directly from sequencies of key-value pairs:
```Python
>>> dict([('sape', 4139), ('guido', 4127), ('jack', 4098)])
{'sape': 4139, 'guido': 4127, 'jack': 4098}
```
- dict comprehensions can be used to create dictionaries
```Python
>>> {x: x**2 for x in (2, 4, 6)}
{2: 4, 4: 16, 6: 36}
```
- When the keys are simple strings, it is easier to use keyword arguments
```Python
>>> dict(sape=4139, guido=4127, jack=4098)
{'sape': 4139, 'guido': 4127, 'jack': 4098}
```

#### Modules
A module is a file containing definitions and statements.
Within module, the module's name is available as the value of the global variable `__name__`. 

```Python
# fibo.py
# Fibonacci numbers module

def fib(n):    # write Fibonacci series up to n
    a, b = 0, 1
    while a < n:
        print(a, end=' ')
        a, b = b, a+b
    print()

def fib2(n):   # return Fibonacci series up to n
    result = []
    a, b = 0, 1
    while a < n:
        result.append(a)
        a, b = b, a+b
    return result

```

Module can be imported using
```Python
import fibo
```
Usage:
```Python
>>> fibo.fib(1000)
0 1 1 2 3 5 8 13 21 34 55 89 144 233 377 610 987
>>> fibo.fib2(100)
[0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89]
>>> fibo.__name__
'fibo'
```

#### More on Modules

- A module can contain executable statements as well as functions definitions.
- These statements are intended to initalize the module. They are executed only the first time the module name is encountered in an import statement.
- Each module has its own private symbol table, which is used as the global symbol table by all functions defined in the module.
- It is customary but not required to place all `import` statements at the beginning of a module.

- There is a variant of the import statement that imports names from a module directly into the importing module’s symbol table. For example:

```Python
>>> from fibo import fib, fib2
>>> fib(500)
0 1 1 2 3 5 8 13 21 34 55 89 144 233 377
```
- This does not introduce the module name from which the imports are taken in the local symbol table (so in the example, `fibo` is not defined)

- There is even a variant to import all names that a module defines:
```Python
>>> from fibo import *
>>> fib(500)
0 1 1 2 3 5 8 13 21 34 55 89 144 233 377
```
- This imports all names except those beginning with an underscore (`_`).
- Note that in general the practice of importing * from a module or package is frowned upon, since it often causes poorly readable code.

- If module name is followed by as, the name following as in bound directly to the import module

```Python
>>> import fibo as fib
>>> fib.fib(500)
0 1 1 2 3 5 8 13 21 34 55 89 144 233 377
```
as with from

```Python
>>> from fibo import fib as fibonacci
>>> fibonacci(500)
0 1 1 2 3 5 8 13 21 34 55 89 144 233 377
```
***Note: For efficiency reasons, each module is only imported once per interpreter session. Therefore, if you change your modules, you must restart the interpreter – or, if it’s just one module you want to test interactively, use importlib.reload(),***

```Python
import importlib; 
importlib.reload(modulename).
```

#### Executing modules as scripts
```sh
python fibo.py <arguments>
```

```Python
if __name__ == "__main__":
    import sys
    fib(int(sys.argv[1]))
```



#### 'Compiled' Python files
- To speed up loading modules, Python caches the compiled version of each module in the `__pycache__` directory under the name `module.version.pyc`
This naming convention allows compiled modules from different realeases and different versions of Python to coexist

Python does not check the cache in two circumstances. First, it always recompiles and does not store the result for the module that’s loaded directly from the command line. Second, it does not check the cache if there is no source module. To support a non-source (compiled only) distribution, the compiled module must be in the source directory, and there must not be a source module.

Some tips for experts:
- You can use the -O or -OO switches on the Python command to reduce the size of a compiled module. 
- A program doesn’t run any faster when it is read from a .pyc file than when it is read from a .py file; the only thing that’s faster about .pyc files is the speed with which they are loaded.
- The module compileall can create .pyc files for all modules in a directory.

#### Standard Modules

1. `dir()`

#### Packages
- Packages are a way of structuring Python’s module namespace by using “dotted module names”.
- For example, the module name A.B designates a submodule B in a package named A.
- Just like the use of modules saves the authors of different modules from having to worry about each other’s global variable names, the use of dotted module names saves the authors of multi-module packages like NumPy or Pillow from having to worry about each other’s module names.
- The `__init__.py` files are required to make Python treat directories containing the file as packages.


#### Errors and Exceptions
Errors detected during execution are called exceptions

Multiple Exceptions can be handled simultaneously
```Python
expect (RuntimeError, TypeError, NameError):
    pass
```

- An exception of base class is compatible with derived class.
```python
class B(Exception):
    pass

class C(B):
    pass

class D(C):
    pass

for cls in [B, C, D]:
    try:
        raise cls()
    except D:
        print("D")
    except C:
        print("C")
    except B:
        print("B")
```



