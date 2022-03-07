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

### I18N
Internationalization is shortened as I18N 
I - 18 letters - N

- ASCII: American Standard Code for Information Interchange
- Uses 8 Bits -> 256 possible characters
- **Code Point**: Is a number which makes up a character. Ex: 32 -> Space
- First 128 Code Points Makes up Upper + Lower case English characters
- **Code Page**: Standard for using upper 128 code points to store specific national characters
- > For example, the code point 200 makes Č (a letter used by some Slavic languages) when utilized by the ISO/IEC 8859-2 code page, and makes Ш (a Cyrillic letter) when used by the ISO/IEC 8859-5 code page.
