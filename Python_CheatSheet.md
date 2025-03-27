# Python Cheat Sheet

## 1. Basics

### 1.1 Install Python
Download from [Python](https://www.python.org) and verify installation:
```py
python --version
```
### 1.2 Variables & Data Types
```py
x = 10      // Integer
y = 3.14    // Float
z = "Hello" // String
flag = True // Boolean
```

### 1.3 Conditional Statements
```py
if x > 5:
    print("Greater")
elif x == 5:
    print("Equal")
else:
    print("Smaller")
```

### 1.4 Loops
```py
// For loop
for i in range(5):
    print(i)

// For loop with start and end
for i in range(1, 5):
    print(i)  // Output: 1 2 3 4

// For Loop with Step
for i in range(0, 10, 2):
    print(i)  // Output: 0 2 4 6 8

// For Loop with Negative Step
for i in range(5, 0, -1):
    print(i)  // Output: 5 4 3 2 1

// For Loop Over a List
fruits = ["apple", "banana", "cherry"]
for fruit in fruits:
    print(fruit)  // Output: apple banana cherry

//For Loop Over a Dictionary
// Iterate over keys in a dictionary
person = {"name": "John", "age": 25}
for key in person:
    print(key)  // Output: name age

// Iterate over key-value pairs
for key, value in person.items():
    print(f"{key}: {value}")
// Output:
// name: John
// age: 25

// While loop
n = 0
while n < 5:
    print(n)
    n += 1
```
### 1.5 Character Classification Functions in Python
```cpp
// Character checks (all return True/False)
c.isalpha()   // Checks if character is alphabetic (a-z, A-Z)
c.isdigit()   // Checks if character is digit (0-9)
c.isalnum()   // Checks if character is alphanumeric (a-z, A-Z, 0-9)
c.islower()   // Checks if character is lowercase letter
c.isupper()   // Checks if character is uppercase letter
c.isspace()   // Checks if character is whitespace (space, \t, \n, etc.)
              // Note: No direct ispunct() equivalent - see note below
c.isxdigit()  // Checks if character is hexadecimal digit (0-9, a-f, A-F) - custom needed
c.isprintable() // Checks if character is printable (similar to isprint)
              // Note: No direct isgraph() equivalent
              // Note: No direct iscntrl() equivalent

// Conversion functions
c.lower()     // Convert to lowercase (returns new string)
c.upper()     // Convert to uppercase (returns new string)

// Example usage:
c = 'A'
if c.isupper():
    c = c.lower()  // 'a'
if '5'.isdigit():  // True
    // do something
```

## 2. Functions
### 2.1 Function Without Parameters
```py
def greet():
    print("Hello, world!")

greet()  // Output: Hello, world!
```
### 2.2 Function With Parameters
```py
def greet(name):
    print(f"Hello, {name}!")

greet("John")  // Output: Hello, John!
```
### 2.3 Function With Default Parameters
```py
def greet(name="Guest"):
    print(f"Hello, {name}!")

greet()           // Output: Hello, Guest!
greet("John")    // Output: Hello, John!
```
### 2.4 Function With Multiple Parameters
```py
def add(a, b):
    return a + b

result = add(5, 3)  // Output: 8
```
### 2.5 Function With Variable Number of Arguments (*args)
```py
def greet(*names):
    for name in names:
        print(f"Hello, {name}!")

greet("John", "John", "Alice")  // Output: Hello, John! Hello, John! Hello, Alice!
```
### 2.6 Function With Keyword Arguments (**kwargs)
```py
def person_info(**kwargs):
    for key, value in kwargs.items():
        print(f"{key}: {value}")

person_info(name="John", age=25, city="Texas")
// Output:
// name: John
// age: 25
// city: Texas
```
### 2.7 Function Returning a Value
```py
def add(a, b):
    return a + b

result = add(5, 3)  // Output: 8
print(result)

```
### 2.8 Function with Both *args and **kwargs
```py
def func(arg1, arg2, *args, **kwargs):
    print(arg1, arg2)
    print(args)
    print(kwargs)

func(1, 2, 3, 4, 5, name="John", age=25)
// Output:
// 1 2
// (3, 4, 5)
// {'name': 'John', 'age': 25}

```
### 2.9 Lambda Functions (Anonymous Functions)
```py
// Lambda function with parameters
square = lambda x: x * x
print(square(5))  // Output: 25

// Lambda function with multiple parameters
add = lambda x, y: x + y
print(add(3, 4))  // Output: 7

```
### 2.10 Function with Return Type Annotations
```py
def greet(name: str) -> str:
    return f"Hello, {name}!"

print(greet("John"))  // Output: Hello, John!

```
### 2.11 Recursive Functions
```py
def factorial(n):
    if n == 0 or n == 1:
        return 1
    return n * factorial(n-1)

print(factorial(5))  // Output: 120

```
### 2.12 Nested Functions (Functions Inside Functions)
```py
def outer_function():
    def inner_function():
        return "Inner function called!"
    return inner_function()

print(outer_function())  // Output: Inner function called!
```

### 2.13 Built-in Functions
#### 2.13.1 Mathematical Functions
```py
# Absolute value
abs(-5)             # 5

# Power function (x^y)
pow(2, 3)           # 8 (same as 2**3)
pow(2, 3, 5)        # 3 (2^3 % 5)

# Rounding
round(3.14159, 2)   # 3.14
round(3.5)          # 4 (banker's rounding)

# Summation
sum([1, 2, 3])      # 6

# Divmod (returns quotient and remainder)
divmod(10, 3)       # (3, 1)

# Max/Min
max(1, 2, 3)        # 3
min([4, 2, 5])      # 2
```

#### 2.13.2 Math Module (Requires `import math`)
```py
import math

math.sqrt(16)       # 4.0
math.factorial(5)   # 120
math.log(100, 10)   # 2.0
math.sin(math.pi/2) # 1.0
math.ceil(3.2)      # 4
math.floor(3.9)     # 3
math.gcd(12, 18)    # 6
math.isqrt(17)      # 4 (integer square root)
```

#### 2.13.3 Iterables & Sequences
```py
# Range
range(5)            # 0..4 (iterator)
list(range(1, 10, 2)) # [1, 3, 5, 7, 9]

# Length
len("hello")        # 5

# Enumerate
for i, v in enumerate(['a', 'b']):
    print(i, v)     # 0 a, 1 b

# Zip
list(zip([1, 2], ['a', 'b'])) # [(1, 'a'), (2, 'b')]

# Sorted
sorted([3, 1, 2])   # [1, 2, 3]
sorted("cba")       # ['a', 'b', 'c']

# Reversed
list(reversed([1, 2, 3])) # [3, 2, 1]
```

#### 2.13.4 Functional Programming
```py
# Filter
list(filter(lambda x: x>0, [-1, 0, 1])) # [1]

# Map
list(map(str.upper, ['a', 'b'])) # ['A', 'B']

# Reduce (from functools)
from functools import reduce
reduce(lambda x,y: x*y, [1, 2, 3]) # 6

# Any/All
any([False, True])   # True
all([True, True])    # True
```


## 3. Data Structures
### 3.1 Lists (Mutable, Ordered, Indexed, Allows Duplicates)
- A list is a collection of elements that are ordered, indexed, and mutable (can be changed).
#### 3.1.1 Initialization
```py
// Empty list
lst = []

// List with initial values
lst = [1, 2, 3]

// List from a range
lst = list(range(5))  // lst = [0, 1, 2, 3, 4]
```

#### 3.1.2 Methods
```py
// Add an element to the end
lst.append(4)  // lst = [1, 2, 3, 4]

// Insert an element at a specific index
lst.insert(1, 10)  // lst = [1, 10, 2, 3, 4]

// Remove an element by value
lst.remove(10)  // lst = [1, 2, 3, 4]

// Remove an element by index
popped_element = lst.pop(1)  // popped_element = 2, lst = [1, 3, 4]

// Reverse the list
lst.reverse()  // lst = [4, 3, 1]

// Sort the list
lst.sort()  // lst = [1, 3, 4]

// Clear all elements
lst.clear()  // lst = []
```

#### 3.1.3 Operations
```py
// Slicing
sublist = lst[1:3]  // sublist = [3]

// List comprehension
squared_list = [x**2 for x in lst]  // squared_list = [1, 9, 16]

// Check if an element exists
if 3 in lst:
    print("Element found")  // Output: Element found
```

### 3.2 Tuples (Immutable, Ordered, Indexed, Allows Duplicates)
- A tuple is an ordered collection of elements, but it is immutable, meaning it cannot be modified once created.

#### 3.2.1 Initialization
```py
// Empty tuple
t = ()

// Tuple with initial values
t = (1, 2, 3)

// Single-element tuple (note the comma)
t = (1,)
```

#### 3.3.2 Methods
```py
// Count occurrences of an element
count = t.count(2)  // count = 1

// Find index of an element
index = t.index(3)  // index = 2
```

#### 3.3.3 Operations
```py
// Slicing
subt = t[1:3]  // subt = (2, 3)

// Concatenation
t1 = (1, 2)
t2 = (3, 4)
t3 = t1 + t2  // t3 = (1, 2, 3, 4)

// Check if an element exists
if 2 in t:
    print("Element found")  // Output: Element found
```

### 3.3 Dictionaries (Mutable, Unordered (Python 3.6 and below), Key-Value Pairs, Unique Keys)
- A dictionary is an unordered collection of key-value pairs. Keys must be unique.
#### 3.3.1 Initialization
```py
// Empty dictionary
d = {}

// Dictionary with initial key-value pairs
d = {"name": "John", "age": 25}

// Dictionary from a list of tuples
d = dict([("name", "John"), ("age", 25)])
```
#### 3.3.2 Methods
```py
// Add or update a key-value pair
d["city"] = "Texas"  // d = {"name": "John", "age": 25, "city": "Texas"}

// Remove a key-value pair
del d["age"]  // d = {"name": "John", "city": "Texas"}

// Get value by key (raises KeyError if not found)
name = d["name"]  // name = "John"

// Safely get value by key (returns None if not found)
age = d.get("age")  // age = None

// Get all keys
keys = d.keys()  // keys = dict_keys(["name", "city"])

// Get all values
values = d.values()  // values = dict_values(["John", "Texas"])

// Get all key-value pairs
items = d.items()  // items = dict_items([("name", "John"), ("city", "Texas")])

// Check if a key exists
if "name" in d:
    print("Key found")  // Output: Key found

// Clear all key-value pairs
d.clear()  // d = {}
```

#### 3.3.3 Operations
```py
// Merge two dictionaries
d1 = {"name": "John"}
d2 = {"age": 25}
d1.update(d2)  // d1 = {"name": "John", "age": 25}

// Dictionary comprehension
squared_dict = {x: x**2 for x in range(5)}  // squared_dict = {0: 0, 1: 1, 2: 4, 3: 9, 4: 16}
```

### 3.4 Sets (Mutable, Unordered, Unique Elements)
- A set is an unordered collection of unique elements.
#### 3.4.1 Initialization
```py
// Empty set
s = set()

// Set with initial values
s = {1, 2, 3}

// Set from a list
s = set([1, 2, 3, 4])
```

#### 3.4.2 Methods
```py
// Add an element
s.add(4)  // s = {1, 2, 3, 4}

// Remove an element (raises KeyError if not found)
s.remove(2)  // s = {1, 3, 4}

// Discard an element (no error if not found)
s.discard(5)  // s remains {1, 3, 4}

// Remove and return an arbitrary element
popped_element = s.pop()  // popped_element = 1, s = {3, 4}

// Clear all elements
s.clear()  // s = set()

// Check if an element exists
if 3 in s:
    print("Element found")  // Output: Element found
```

#### 3.4.3 Operations
```py
// Union of two sets
s1 = {1, 2, 3}
s2 = {3, 4, 5}
union_set = s1.union(s2)  // union_set = {1, 2, 3, 4, 5}

// Intersection of two sets
intersection_set = s1.intersection(s2)  // intersection_set = {3}

// Difference of two sets
difference_set = s1.difference(s2)  // difference_set = {1, 2}

// Symmetric difference (elements in either set but not both)
symmetric_diff = s1.symmetric_difference(s2)  // symmetric_diff = {1, 2, 4, 5}

// Check if a set is a subset
is_subset = s1.issubset(s2)  // is_subset = False

// Check if a set is a superset
is_superset = s1.issuperset(s2)  // is_superset = False

// Check if two sets are disjoint (no common elements)
is_disjoint = s1.isdisjoint(s2)  // is_disjoint = False
```

## 4. Data Type Conversions
```py
// Convert String to Integer
x = "10"
x = int(x)  // x is now an integer

// Convert String to Float
x = "10.5"
x = float(x)  // x is now a float

// Convert Integer to String
x = 10
x = str(x)  // x is now a string

// Convert List to Tuple
x = [1, 2, 3]
x = tuple(x)  // x is now a tuple

// Convert Tuple to List
x = (1, 2, 3)
x = list(x)  // x is now a list

// Convert List to Set
x = [1, 2, 2, 3]
x = set(x)  // x is now a set

// Convert Set to List
x = {1, 2, 3}
x = list(x)  // x is now a list

```

## 5. Object-Oriented Programming (OOP)
- Classes define the blueprint for objects, and objects are instances of a class.
### 5.1 Classes and Objects
```py
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age
    
    def greet(self):
        return f"Hello, my name is {self.name}."

p = Person("John", 25)
print(p.greet())

```
### 5.2 Encapsulation (Restricts Direct Access to Data)
- Encapsulation hides the internal state and only allows access through public methods.
```py
class BankAccount:
    def __init__(self, balance):
        self.__balance = balance  // Private variable
    
    def deposit(self, amount):
        self.__balance += amount
        return self.__balance
    
    def get_balance(self):
        return self.__balance

account = BankAccount(1000)
print(account.get_balance())  // Accessing through method

```
### 5.3 Inheritance (Allows Code Reuse Between Classes)
- Inheritance allows a class to inherit properties and methods from another class.
```py
class Animal:
    def speak(self):
        return "I make a sound"

class Dog(Animal):
    def speak(self):
        return "Bark"

d = Dog()
print(d.speak())

```
### 5.4 Polymorphism (Same Interface, Different Implementation)
- Polymorphism allows different classes to provide a different implementation for the same method.
```py
class Bird:
    def fly(self):
        return "Flies high"

class Penguin(Bird):
    def fly(self):
        return "Cannot fly"

def flying_test(bird):
    print(bird.fly())

flying_test(Bird())
flying_test(Penguin())

```
### 5.5 Abstraction (Hides Implementation Details)
- Abstraction allows you to define methods that must be implemented in derived classes, while hiding the details of the implementation.
```py
from abc import ABC, abstractmethod

class Vehicle(ABC):
    @abstractmethod
    def start_engine(self):
        pass

class Car(Vehicle):
    def start_engine(self):
        return "Engine started"

c = Car()
print(c.start_engine())

```

### 5.6 Constructor (`__init__`)
- The constructor method is called when a new instance of the class is created. It is used to initialize the object's state.
```py
class Person:
    def __init__(self, name, age):
        self.name = name  # Instance variable
        self.age = age    # Instance variable
        print(f"{self.name} is created.")

// Creating an instance of the class
person1 = Person("John", 25)
```
#### Explanation:
- The `__init__` method is the constructor, and it initializes the instance variables `name` and `age`.

- Whenever an object is created, the constructor is called automatically.

### 5.7 Destructor (`__del__`)
- The destructor method is called when an object is about to be destroyed or when the program terminates. It is used to perform clean-up tasks, such as releasing resources (e.g., closing files or network connections).
```py
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age
        print(f"{self.name} is created.")

    def __del__(self):
        print(f"{self.name} is destroyed.")

// Creating and deleting an object
person1 = Person("John", 25)
del person1
``` 
#### Explanation:
- The `__del__` method is the destructor and is invoked when the object is destroyed (for example, when it is deleted or the program ends).

- The `del` statement is used to explicitly delete an object.

### 6. Functional Programming
#### 6.1  `map()` Function
- The `map()` function applies a given function to all items in an input list (or any iterable).
```py
nums = [1, 2, 3, 4]
squared_nums = list(map(lambda x: x**2, nums))
print(squared_nums)  // Output: [1, 4, 9, 16]
```

#### 6.2  `filter()` Function
- The `filter()` function filters elements from an iterable based on a function that returns a boolean.
```py
nums = [1, 2, 3, 4, 5, 6]
even_nums = list(filter(lambda x: x % 2 == 0, nums))
print(even_nums)  // Output: [2, 4, 6]
```

#### 6.3  `reduce()` Function
- The `reduce()` function from the `functools` module is used to apply a function cumulatively to the items in an iterable, reducing it to a single value.
```py
from functools import reduce

nums = [1, 2, 3, 4]
product = reduce(lambda x, y: x * y, nums)
print(product)  // Output: 24
```

#### 6.4 List Comprehensions
- List comprehensions provide a concise way to create lists in a functional programming style.
```py
nums = [1, 2, 3, 4]
squared_nums = [x**2 for x in nums]
print(squared_nums)  // Output: [1, 4, 9, 16]
```

### 7. File Handling
- File handling in Python allows reading from and writing to files.
```py
// Writing to a file
with open("file.txt", "w") as f:
    f.write("Hello, world!")

// Reading from a file
with open("file.txt", "r") as f:
    print(f.read())  // Output: Hello, world!
```

### 8. Exception Handling
- Exception handling allows you to catch and handle errors gracefully during execution.
```py
try:
    x = 1 / 0
except ZeroDivisionError as e:
    print(f"Error: {e}")  // Output: Error: division by zero
finally:
    print("Execution completed")  // Output: Execution completed
```
