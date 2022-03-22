# Advanced Perspective of Classes and Object-Oriented Programming in Python: 1

## Classes

- Instances can also refer Class Variables
- If class instances (objects) modify a Class Variable, a new instance variable with the same name is created --> Leads to bugs
- Use **Class Name** to refer to Class Variable
- `__class__` variable returns the class, an object belongs to
- `type` is the most basic class

## Inheritance

- Gives an `is a` relation among objects. **Car is a Vehicle**
- Objects are tightly coupled
- Avoid Multiple Inheritance --> Can cause Diamond Problem
- If multiple inheritance is required, take care of **Method Resolution Order**
- **Method Resolution Order**: Order in which a method is looked up in the base classes. This should be same as the order of inheritance. Ex A.a(), B.a() and if C inherits both A and B and calls a(), the order in which C is inherting the base classes will determine which **a()** method would be called.
- **Polymorphism**: Overriding Base Class Methods, in Derived Class
- `__` : Double Underscore ==> DUNDER
- Each operation corresponds to a method. When using operators with objects, these methods are called magic methods. (surrounded by DUNDERs)
- [List](https://docs.python.org/3/reference/datamodel.html#special-method-names) of magic methods

![image](https://user-images.githubusercontent.com/43227329/158736552-8906f9be-242d-456a-950f-7ce4b2c9adf7.png)

## Function Argument Syntax

- `*args` : Collects all unmatched positional arguments in a tuple
- `**kwargs` : Collects all unmatched keyword arguments in a dictionary

```py
def fn(a,b, *args, **kwargs):
  pass

fn(1,2,3,4,5,6,x=1,y=2)
# a, b : Required arguments
# 3-6: would be collected in args
# x, y: would be collected in kwargs
```

## Function Decorators

- Design Pattern. Used to surround functions with one other function
- Used to perform operations, before and after a call to a wrapped object


```py

def decorator(function):
  def interal_wrapper(*args, **kwargs):
    # Code to run before fn() runs
    function(*args, **kwargs)
    # Code to run after fn() runs

@decorator
def fn():
  pass

fn()
```

### Decorator with arguments

```py
def decorator(decorator_arguments):
    def wrapper(decorated_function):
        def internal_wrapper(*decorated_function_args):
            # code to run before decorated_function()
            decorated_function(*decorated_function_args)
            # Code to run after decorated_function()
        return internal_wrapper
    return wrapper

@decorator('hi')
def decorated_function(*decorated_function_args):
  pass
```

### Stacked_decorators

```py
def outer_decorator(decorator_arguments):
    def wrapper(decorated_function):
        def internal_wrapper(*decorated_function_args):
            # code to run before decorated_function()
            decorated_function(*decorated_function_args)
            # Code to run after decorated_function()
        return internal_wrapper
    return wrapper

def inner_decorator(decorator_arguments):
    def wrapper(decorated_function):
        def internal_wrapper(*decorated_function_args):
            # code to run before decorated_function()
            decorated_function(*decorated_function_args)
            # Code to run after decorated_function()
        return internal_wrapper
    return wrapper

@outer_decorator('bye')
@inner_decorator('hi')
def decorated_function(*decorated_function_args):
  pass

# this is equivalent of calling outer_decorator(inner_decorator(decorated_function))
```

### Class based function decorators

```py
class SimpleDecorator:
    def __init__(self, decorated_function):
        self.func = decorated_function

    def __call__(self, *args, **kwargs):
        # Code before running decorated_function
        self.func(*args, **kwargs)
        # Code after running decorated_function

@SimpleDecorator
def fn():
  print(1,2)
```

### Class based function decorator with arguments

- When an argument is passed to the decorator, its constructor takes in that argument instead of the function reference

```py
class Decorator:
    def __init__(self, argument_to_decorator):
        pass

    def __call__(self, decorated_function):
        def internal_wrapper(*args, **kwargs):
            # Code before running decorated_function
            decorated_function(*args, **kwargs)
            # Code after running decorated_function

        return internal_wrapper
```

## Class Decorators

- Used to modify behavior of classes

```py
def class_decorator(class_reference):
    class_reference.__getattr__orig = class_.__getattribute__

    def new_getattr(self, name):
        if name == 'mileage':
            print('We noticed that the mileage attribute was read')
        return class_reference.__getattr__orig(self, name)

    class_reference.__getattribute__ = new_getattr
    return class_reference

```

## Methods in a class

### Static Methods
- Used to link logic with the Class
- Used with `@staticmethod` decorator
- Takes neither `self` or `cls` methods
- Cannot modify the state of object or classes
- Utility method

### Class Methods

- Used with `@classmethod` decorator
- Invoke the **__init__** automatically
- Takes a `cls` argument
- Used to create an instance of the class

### Instance Methods

- Linked with an instance of the class 
- Take a mandatory `self` argument

## Abstract Class

- Blueprint for other classes
- Contains declaration of methods which need to be implemented in the Derived Classes
- A separate module tests if all the abtract methods are implmeneted or not in the derived class.
- Can not instantiate an abstract class
- `abc` module (Abstract Base Class) of python provides packages to deal with abstract classes
- `@abstractmethod` is used to make a method abstract and to enforce its implementation in the derived classes

### `property` decorator
- Used to encapsulate Class Attributes
- When set over a method's name, that can be accessed directly to be read

### getter/setter

- `@var_name.getter`, `@var_name.setter`, `@var_name.deleter` are used to access private variables

## Composition

- Provides a `has a` relationship among objects
- Laptop `has a` graphic card
- Objects are loosely coupled

```py
class Car:
    def __init__(self, engine):
        self.engine = engine

class GasEngine:
    def __init__(self, horse_power):
        self.hp = horse_power

    def start(self):
        print('Starting {}hp gas engine'.format(self.hp))

class DieselEngine:
    def __init__(self, horse_power):
        self.hp = horse_power

    def start(self):
        print('Starting {}hp diesel engine'.format(self.hp))

my_car = Car(GasEngine(4))

```

> IBAN (International Bank Account Number) is an algorithm to specify account numbers

## Exception Handling

- `except Exception as e`
- `e` variable is bound to the type of exception
- e.args contains all the arguments of the exception

### Exception Chaining

- If an exception is raised while handling another exception, we should not lost context of the first exception
- Implicitly, the original exception is also saved if a new exception is raised
- Explicitly we need to use `raise from` clause to raise a new exception while preserving the old one
- The inner exception has two new attributes
  - `__cause__`
  - `__context__`

- Each exception has a `__traceback__` attribute. This can be formatted with `format_tb()` method of the `traceback` module

```py
    except Exception as e:
        raise NewException from e
```
