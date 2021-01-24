# Python in Depth 
derived from [docs.python.org](https://docs.python.org/3/tutorial/)

#### Small points
`//` - floor division, discards fractional part
`_` variable stores last printed expression value in python interpreter
Python supports complex numbers `a = 2 + 3j`

If you donot want to use special characters, you can use  r before string. It will make raw string.
String literals can span multiple lines, so you can use `"""....""", '''....'''` (triple quotes)

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
