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

## Objects Persistence

- `id()`: Function returns the identity of an object. Unique and Constant Integer for an object throughout its lifetime

```py
  var_1 = 1
  var_2 = var_1
  var_1 == var_2  # Since var_2 is only a reference to var_1
```

- `==` : Checks equality based on value of two objects (Will return true for, var_1 == var_1 AND var_1 == var_2 \[If var_1 = 1, var_2 = 1\] )
- `is` : Checks if two objects are equal or not (Both in value and in id())

### Shallow Copy

- `list_name[:]` this expression creates a shallow copy of the list
- This is a different object which points to the same location in memory

### Deep Copy

- `copy.deepcopy`
- Different object which points to a different location in memory
- Construct a new object and recursively copy all objects found in it
- Copies an already initialized object (so `__init__` method is not invoked for the copied object)
![image](https://user-images.githubusercontent.com/43227329/159628493-9f7d2fdc-652b-4ccf-8157-973d37b40800.png)


### Serialization

- pickle library is used for object serialization. comes from the word `pickled` which means saving for later use
- `pickle.dump(object, file_name), pickle.load(file_name)` to serialize and deserialize to binary files
- `pickle.dumps(object), pickle.loads(bytes)` to serialize and deserialize to bytes
- Function/Class defitions cannot be pickled (So that a pickled object can still be deserialized if class definition changes)
- the code that calls the load() or loads() functions of pickle should already know the function/class definition.
- `shelve` module is built on top of pickle module and is used to serialize multiple objects


## Metaclasses
- Metaclasses -> Class whose instance is also a class
- type(Classname, tuple of base classes to inherit from, dict of method definitions and variables)

```py
def bark(self):
    print('Woof, woof')

class Animal:
    def feed(self):
        print('It is feeding time!')

Dog = type('Dog', (Animal, ), {'age':0, 'bark':bark})
```

- `type()` calls the `__call__` method which in turn calls 
  -  `__new__`: Responsible for creating class instance in computer memory
  -  `__init__` method which is responsible for object initialization

- Defining a meta class in another way

```py
class My_Meta(type):
    def __new__(mcs, name, bases, dictionary):
        obj = super().__new__(mcs, name, bases, dictionary)
        obj.custom_attribute = 'Added by My_Meta'
        return obj

class My_Object(metaclass=My_Meta):
    pass
```

- `mcs` is used to refer to the class
