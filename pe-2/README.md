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
  
  
