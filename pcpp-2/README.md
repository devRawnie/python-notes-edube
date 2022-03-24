# PCPP 2 (Python Styling and Code Standards)

## PEP (Python Enhancement Proposal)

- Outlines the language standards
- Gives guidelines and best :
- Provides information about changes and processes related to Python
- [PEP 0](https://peps.python.org/) is the index of all available PEPs

## PEP 1 : PEP Purpose and Guidelines

Types of PEP

1. Standard Track: Describe new language features and implementation
2. Informational: Describe Python's design issues + Provides Guidelines
3. Process: Describe processes such as (Change proposal, Recommendation Proposal)

PEP 1 also defines
- Python's Steering Council: 5 Person committee and final authorities who accept or reject PEPs
- Python Core Developers: Group of volunteers who manage python
- Python BDFL: (Benevolent Dictator for life)

> PEP Champion: Someone who writes a PEP Proposal


## PEP 20: The Zen of Python

- Collection of 19 Axioms
- 19 Line poem by Tim Peters
- Its one of the easter eggs (Run `import this` in an interpreter)

### Beautiful is better than Ugly

- 79 Character maximum length
- Placing statement on separate lines
- Variable naming convention

### Explicit is better than implicit

```py
# Avoid this
from foo import *

# use this
from foo import bar
```

### Simple is better than complex

### Complex is better than complicated
- If simple solution is making the code look complicated, resort to a complex solution which is more readable

### Flat is better than Nested

- Avoid nested `if`
- Use fail first approach

### Sparse is better than Dense

### Readability counts

- Meaningful naming scheme
- Block of comments

### Special cases aren't special enough to break the rules
- Be consistent with the naming scheme and style of code

### practicality beats purity

### Errors should never pass silently
- Raise errors proactively, which will help debug easily

### In the face of ambiguity, refuse the temptation to guess

- Always test the code before moving to production
- Run a script in interpreter instead of guessing the output

### There should be one – and preferably only one – obvious way to do it

- Follow one method of doing things throughout

### Now is better than never

### If the implementation is hard to explain, it's a bad idea, If the implementation is easy to explain, it may be a good idea
- Keep things simple

### Namespaces are one honking great idea – let's do more of those!

- Whenever you define a variable, Python “remembers” two things: the variable’s identifier, and the value you pass to it.
- Python implicitly adds them to an internal dictionary which resides within a particular scope, i.e., the region of a Python program where namespaces are accessible
- Using the global keyword before a global variable inside the function is a mechanism that allows you to alter that variable, even though it resides in a different scope (bad practice).
- 
```py
# Do this
from instruments import guitars

guitars.fender(page)
guitars.ibanez(vai)

# Avoid this
from instruments.guitars import fender, ibanez

fender(page)
ibanez(vai)
```

## PEP 8

- Provides Coding convention
- Follow to be more consistent throughout the project
- Don't follow if it breaks backward compatibility, readability, or inconsistency with an existing project
- There are tools that check code against PEP 8 Standards `autopep8`, `pycodestyle`
- Online tool: [here](http://pep8online.com/about)

### Indentation
- Leading whitespace at the beginning of each logical line
- Use spaces rather than tabs
- Four spaces per indentation level

### Continuation Lines
- Are allowed if used with **brackets**
- Break line before binary operators

```py
# Good:
my_list_two = [
    1, 2, 3,
    4, 5, 6,
]


def my_fun(
        a, b, c,
        d, e, f):
    return (a + b + c) * (d + e + f)

total_fruits = (apples
                + pears
                + grapes
                - (black currants - red currants)
                - bananas
                + oranges)
```

### Maximum Line Length: 79

### Blank lines

- Two blank lines to surround **Top Level Functions** and **Class Definitions**
- One blank line to surround **Method Definitions** inside a class
- Single blank lines inside functions to separate logical sections

### Use UTF-8 Encoding for Python 3 and ASCII for Python 2

### Imports
- Put imports at the beginning of script
- Follow this order for import statements
  1. Standard library imports
  2. Related third-party imports
  3. Local application/library specific imports
- Prefer absolute imports instead of general `*` 

### Whitespace
- Don't use excessive whitespace inside declarations of list, inside parantheses
- Colon's `:` should be surrounded by equal whitespace
- Surround binary operators with single whitespace
- Don'y use whitespace with `=` in Default arguments

Cont: [Here](https://edube.org/learn/pcpp1-python-enhancement-proposals-peps/pep-8-comments)


### Comments
- Keep 72 characters per line
- Use as a sentence
- Avoid Inline Comments
- If inline comments are used, separate them from the expression with two spaces

### Docstring

- Used for documentation purpose
- Inside triple double-quotes

### Variable Naming
- Snake Case / Camel Case
- Capitalize all letters of acronym
- Follow [this](https://peps.python.org/pep-0008/#prescriptive-naming-conventions)

### Comparison

- Use `is` , `is not` operator for comparing with `None` and Boolean Objects
- Programming Recommendations: [Here](https://peps.python.org/pep-0008/#programming-recommendations)

