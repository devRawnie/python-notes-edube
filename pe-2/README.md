# PE 2

## [Modules](https://docs.python.org/3/py-modindex.html)

- **Namespace** : Space in which some names exist which do not conflict with each other
- Import statements supersedes any previous declarations of the same name. Similarly if `from x import y` syntax is used, and y is also defined manually later on, then the latest definition would be considered
- **dir(ob)** : Returns an alphabetically sorted list of entity names available in `ob`, which can be a module, a function or a variable
- `math`: **pow, log, log10, log2, exp, sin, cos, tan**
- `random`: 
- - random() : float ∈ [0,1)
- - seed(int): If nothing is passed, it sets the seed as current time
- - randrange(beg, end, step)
- - randint(left, right)
> Right side is excluded by default
- - choice(seq): Picks one random element
- - sample(seq, n): Picks n random elements
- `platform`: Gives access to underlying platform data
- - platform(): Gives platform name
- - machine(): Gives machine architecture (32, 64)
- - processor(): Processor name
- - system(): returns OS name as string
- - version(): OS Version
- - python_implementation(), python_version_tuple()

## Package 

> Collection of modules

**__pycache__**: This will put the imported module in a semi compiled form with name `module-name.cpython-xy.pyc`
- pyc: Python compiled
- xy: Python version

**__name__** : If a file is executed directly, this is set to `__main__`, and if it is imported then this is set to the module name
**__init__.py**: Used to initialize a package
`sys.path` contains all the paths where python would search for installed packages

## Package Manager

### PyPI (Python Package Index): Repository for distributing python packages

Command line tool to handle packages: `pip` short for (pip installs packages)
- `pip help operation-name`
- `pip show package-name`
- `pip search package-name`


### Dependencies
- Dependent packages that need to be installed to use a specific package
- Ex. To use `django`, `asgiref` is a dependency

## Strings

- Immutable sequences
- methods:
  - "".index(char)
  - "".count(char)
  - "".capitalize() `First Character`
  - "".center(n, char) "Tries to put the string in the center adding spaces or `char` as specfied
  - "".endswith(pattern), "".startswith()
  - "".find(): Looks for substrings, "".rfind(): Starts from the right
  - "".isalnum(), "".isalpha(), "".isdigit(), "".islower(), "".isupper(), "".isspace()
  - "".swapcase(): Swaps the case for all letters in the string
  - "".title(): Every word's first letter to upper case turning all other ones to lower case
  - "<sep>".join([]) : Joins the contents of list with the separater string
  - "".lstrip() : Remove leading whitespaces, "".rstrip(): Trailing whitespaces, "".strip(): Both leading and trailing whitespaces
  - "".replace(n1, n2, max_count): Replace `n1` in the string with `n2` for `max_count` no of times
  - "".split(char)

### I18N
Internationalization is shortened as I18N 
I - 18 letters - N

- ASCII: American Standard Code for Information Interchange
- Uses 8 Bits -> 256 possible characters
- **Code Point**: Is a number which makes up a character. Ex: 32 -> Space
- First 128 Code Points Makes up Upper + Lower case English characters
- **Code Page**: Standard for using upper 128 code points to store specific national characters
- > For example, the code point 200 makes Č (a letter used by some Slavic languages) when utilized by the ISO/IEC 8859-2 code page, and makes Ш (a Cyrillic letter) when used by the ISO/IEC 8859-5 code page.
- **BOM (Byte Order Mark)** is a special combination of bits announcing encoding used by a file's content (eg. UCS-4 or UTF-B).

### Universal Character Set

UCS -32 Bytes

### UTF 8

- Unicode transformation format
- Uses as many bits as it needs to represent a character
- Ex: Latin characters -> 8 bits
- Non latin -> 16 bits

## Exceptions

![Python exception tree](https://user-images.githubusercontent.com/43227329/157039228-1c0590f1-06ae-46de-a0ea-846525b31cf9.png)

> `raise` keyword can be used directly without specifying an exception type, with a restriction that it can only sit inside a `catch` block. It will immediately re-raise the current exception
  
- `assert` : Keyword that evaluates an expression. If it results in True -> Continues with the flow. If it results in False -> Raises an `AssertionError` exception
  
  
## Object Oriented Programming

### Procedural Programming

- Code and Data are separate
- Code can use/abuse data

### Object Oriented Approach

- Data and Code both live together in `Classes`
- Can create hierarchies using Superclasses and Subclasses
- Class : Set of properties, used to create objects
- Instance: Instantiation of the Class, an object of the class which has values for its variables
- Object: Contains `name`, `properties`, `methods` to modify its properties
- Properties
  - **Instance Variables**: Declared using `self`, are tied to an instance of the class
  - New instance variables can be added on an existing class object, even if it did not exist in the class definition
  - Append two underscores `__`, before the name of a property, and it becomes private. i.e. it is not accessible outside the class
  - **Mangling**: If a private instance variable is added using a Class method, it is renamed as `_classname__variablename`. It is accessible from the outer world, but using this special syntax only. This mangling does not happen when a private variable is added from the object instance
  - **Class Variable**: These variables are tied to the Class itself. Only one copy of such variables exist. For multiple objects, multiple copies are not created. These are not visible in the objects `__dict__` method. These are visible in the `Class's` __dict__ method
    - __dict__
    - __name__
    - __module__: name of the module currently being run
    - __bases__ : A tuple, contains all classes which the current class has inherited from. If no explicit inheritance is specified, `object` class is returned as output
  ![image](https://user-images.githubusercontent.com/43227329/157433356-17a9d94d-767f-4428-a157-cc33bf8dfe92.png)


### Inheritance

- A subclass inherits all the properties of the superclass
- issubclass(Subclass, Baseclass)
- super() can be used to invoke a method of the baseclass like: `super().function_name(parameter)`
- `BaseClassName.function_name(self, parameter)` is original way of doing this
- Python searches for the class name in `current-object` -> `immediate base class` -> `base class of the immediate base class` . . .
- In case of multiple inheritance it searches `current-object` -> `first base class` -> `second base class` ...
- Multiple inheritance have a [problem](https://en.wikipedia.org/wiki/Single-responsibility_principle)
- Multiple inhertiance also has the `Diamond Problem`

> Constructor for the superclass is to be invoked explicitly, SUPERCLASS.__init__(self)
> Any method of the superclass which needs calling in sub-class will require the `self` argument. SUPERCLASS.method(self)

### Polymorphism

 ![image](https://user-images.githubusercontent.com/43227329/157437300-a5d5da8b-0344-4caa-84c9-c546f2843d3f.png)

### Method Resolution Order (MRO)
  
It is a strategy in which a particular programming language scans through the upper part of a class’s hierarchy in order to find the method it currently needs. It works as explained under [inhertiance](./#Inheritance)

  
## Miscellaneous
  
### Generators

Using `generators`, we can:
- produce a series of values
- control the iteration process
- also known as `iterators`
- using paranthesis `()` and the syntax used for list comprehension, we can create generators
- Ex: `(1 for 1 in range(10))` -> Generator

Iterator protocol
- a way in which an object should behave to conform to the rules imposed by the context of the `for` and `in` statements
- it should have one `__iter__` method which returns the object itself
- it should have one `__next__` method which will return the next available method or raise a `StopIteration` Exception

> An object may be used as an Iterator only if it returns `self` inside its implementation of the `__iter__` method

`yield` keyword
 - Provides the value of an expression specified after it, without losing the state
 - Variable values are frozen and used at the time of next invocation
 - Used inside of a function. The function becomes a `generator` on using this keyword

### Lambda Function

`lambda parameter(s) : expression`
- Its an anonymous function
- Can be used as arguments

### map function

`map(function, list)`
- invokes the function for each element of the list
- returns a generator

### filter function

`filter(function, list)`
- invokes the function on each element of the list and expect a True/False from the function
- if the function returns true for element x of the list, that element will be collected by `filter` function
- returns a list of all elements which return True after going through the specified function

### Closure
```py
def outer(val): # Closure function
  loc = val
  def inner():
    return loc
  return inner
```

## File Handling

- Files are accessed via `handlers` and `streams` which help us write code that is OS Independent
- Connecting with stream -> Opening the file. Disconnecting this link -> closing the file
  
### Modes of interacting with the file
![image](https://user-images.githubusercontent.com/43227329/157675545-9d0bfa94-da04-4791-a1ed-1b5814dd8516.png)

1. read mode
2. write mode
3. update/append mode

Different objects that deal with Files
![image](https://user-images.githubusercontent.com/43227329/157667654-34d1fee2-7857-4279-8915-5c84f487e988.png)

1. Text Streams: Structured in lines, read and written one line (sequence of typographic characters) at a time 
2. Binary Streams: Contain sequence of bytes. Data is read and written byte by byte, or block by block (where block is a fixed size of no of bytes)

File opening [errors](https://edube.org/learn/pe-2/processing-files-42)
Processing text [files](https://edube.org/learn/pe-2/working-with-real-files-42)
> During reading and writing in Windows based system, if a file is open in `text-mode`, every pair of `\r\n` is replaced with `\n` while reading and vice-versa while writing.


### Bytearray
  
- Used to store a series of `bytes`
- `bytearray(10)` : can hold 10 bytes of data, filled with 0s

### Read a binary file

- `fp.readinto(bytearray)` : will read the contents of file pointed to by `fp` in the bytearray
- `bytearray(fp.read())` : this also creates a bytearray, but this one is immutable

## OS module

- `os.uname` : Operating System, Network Name, Machine architecture details. This is available on Linux. For windows: use `platform.uname`
- `os.mkdir` : Creates one directory
- `os.makedirs` : Creates directories recursively
- `os.rmdir` / `os.removedirs`
- `os.system(command)`: 0 -> Success | 1 -> Error
