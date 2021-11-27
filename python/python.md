###### tags : `tutorial` `python`
# Python Cheat Sheet
> Python is a popular programming language. It was created by Guido van Rossum, and released in 1991.

### 1. Comments
> A line of code that will not executed by compiler
- Single line comment : `#` symbol
```
#this is single line comment
```
- Multiple line comment : triple of `"` or `'`
```
"""
This is multiple line
comment in python
"""

'''
This is multiple line
comment in python
'''
```
### 2. Variable
#### 2.1 Definition
> Variables are memory locations reserved for storing values. This means that when you create a variable you reserve some space in memory.

#### 2.2 Naming Variable
- A variable name must start with a letter or the underscore character
- A variable name cannot start with a number
- A variable name can only contain alpha-numeric characters and underscores (A-z, 0-9, and _ )
- Variable names are case-sensitive (age, Age and AGE are three different variables)
- Variable is a symbolic name given to an unknown quantity that permits the name to be used independent of the information it represents.
```
# valid variable
firstName = "Yudi"
book1 = "Harry Potter"
_age = 24

# invalid variable
1movie = "The Lord of the Ring" # start with number
string = "this is a string" # use reserved word in python
```

#### 2.3 Assigning / Delete Variable
```
# assigning a variable
name = "Yudi"

# assigning multiple variable with different value
midTest, finalTest = 80, 90

# assigning multiple variable with same value
a = b = c = 0

# delete variable
del(varName)

```
#### 2.4 Print to console
```
print(varName)
```

### 3. Data Type
- A data type is a medium or memory on a computer that is used to store information.
- A syntax to know a data type of variable is `type(varName)`
#### 3.1 Python data types
| Data Type | Example | Description |
| -------- | -------- | -------- |
| String     | `"Let's learn python"` | Text |
| Integer   | `25` or `1209`| Integer number |
| Float   | `0.14` or `0.99`| Real number |
| Boolean     | `True` or `False`     | - |
| Hexadecimal |	`9a` or `1d3` | Number in  hexadecimal format|
| Complex |	`1 + 5j` | Complex number|
| List |	`['xyz', 786, 2.23]` | Array  |
| Tuple	 | `('xyz', 768, 2.23)` |	Unchanged Array |
| Dictionary |	`{'name': 'Yudi Aditya','id':2}` | Data type that contains key - value pair |

#### 3.2 Notes
a. String
- use triple `"` or `'` to assign multiple line string
```
multipleLineString = """Lorem ipsum dolor sitamet,
consectetur adipiscing elit,
sed do eiusmod tempor incididunt
ut labore et dolore magna aliqua.
"""
```
- to assign `'` or `"`, use escape character `\`
- There are several ways to print a string along with another variable
```
# print multiple variable
print(a, b, c)

# Old Style
print('Hello i am %s i am %d years old' % (name, age))

# 'New Style' string formatting
print('Hello i am {0} i am {1} years old'.format(name, age))

# String interpolation
print(f'Hello i am {name} i am {age} years old')
```
- String Operation
```
a = "2"+"3" # a = 23
b = "2"*3   # b = 222
```

b. Number (Integer / Float)
- Number Operation
 
| Operator | Description | Example |
| -------- | -------- | -------- |
| `+, -, *, /`     | -     | -     |
| `**`     | Power     | `2**3 = 8`     |
| `%`     | Modulo     | `9%2 = 1`     |
| `//`     | Floor Division     | `13//2 = 6` |

- python is smart enough to inference the data type of number operation's result
```
a = 2*3      # a = 6   => integer
b = 6/3      # b = 2.0 => float
c = 2.3 + 5  # c = 7.3 => float
```
- if you want to convert to specific data type, you can use type casting
```
a = int(11/4)   # a = 2 => convert to integer (floor rounded) 
```

- Type Casting
```
x = int("123")   # x = 123 is a integer number
y = str(3.14)    # y = "3.14" is a string
z = float("123") # z = 123.0 is a float number
```

c. Bool
- Boolean Operation

| Operator | Description |
| -------- | -------- | 
| `not`    | negation operator     | 
| `and`    | and operator     | 
| `or`     | or operator     |

d. List 
- Create a List
```
a = ["Yudi", True, 32]
```
- Access element on a list
```
names = ["Yudi", "Fitria", "Ghazi", "Azzam"]
# access an element
names[0] # Yudi
names[-1] # Azzam

# Slicing a List
# Slice a list start from index p(include) to index q(exclude)
names[1:3] # ["Fitria", "Azzam"]  

```
- Combine two lists
```
# Combine a List
a = [1,2,3,4]
b = [5,6]
c = b+a
print(c) # [5,6,1,2,3,4] 
```
- Filter a list
```
values = [1,2,3,4,5,6,7,8]
evenValues = [val for val in values if val%2==0]
```

- Check element on a list `el in <list>`
- List Method 

| Method | Description | 
| -------- | -------- | 
| `arr.append(<value>)`     | add element on the last     | 
| `arr.pop(<idx>)`     | remove element by index     | 
| `arr.remove(<value>)`     | remove element by value     | 
| `arr.insert(<idx>, <value> )`     | insert value on specific index     | 
| `arr.copy()`     | duplicate a list     |

e. Tuple
> A tuple is a collection which is ordered and unchangeable.
```
# Create a tuple
a = ("Medan", "Bogor", "Jakarta")
# Access an element
print(a[0]) # "Medan"
```
- Tuple Method

| Method | Description | 
| -------- | -------- | 
| tup.count(<value>)     | count <value> on tuple     | 
| tup.index(<value>)     | find index <value> on tuple     | 


e. Set
> A set is a collection which is unordered, unchangeable, and unindexed.

- Initiate a Set
```
a = Set([1,3,5])
b = {2,3,5}
c = Set()
```

- Set Method 

| Method | Description | 
| -------- | -------- | 
| `a.remove(<el>)` , `a.remove(<el>)`     | Remove el from a set, **raise an error if not exist** |
| `a.discard(<el>)` | Remove el from a set, pass if not exist  |
| `a.add(<el>)`     | Add element to a set     | 
| `a.update([<el>])`     | Add multiple element to a set     | 
| `a.copy()`     | Copy a set     |
| `a.issubset()`     | Check is subset     |
| `a.issuperset()`     | Check is subset     |
| `a.isdisjoint()`     | Check wheter intersection is null     |


- Set Operator

| Method | Description | 
| -------- | -------- | 
| `a | b`, `a.union(b)`     | Union     
| `a & b`, `a.intersection(b)`     | Intersection     | 
| `a - b`, `a.difference(b)`     | Difference     |
| `a ^ b`, `a.symmetric_difference(b)`     | (A Union B) - (A Intersection B)      |

f. Dictionary
> key value pair
- Initiate a dictionary
```
a = {name: "Yudi Aditya", isMale: True, city: "Bandung"}
b = {} # initiate empty dictionary

# Access value
print(a["name"]) # "Yudi Aditya", raise error if empty
print(a.get("name")) # "Yudi Aditya"

```

- Dictionary Method

| Method | Description | 
| -------- | -------- | 
| `a.copy()`   | clone a dictionary |
| `a.get(<key>)`   | access item on a dictionary, will not raise an error |
| `a.items()`   | return object of list values |
| `a.keys()`   | return object of list keys |
| `a.update(<dict>)`   | add new key value pair |
| `a.pop(<key>)`   | remove key value pair, raise error if key not exist |

> To get list of items/keys, convert the result with method `list()`, or in complete syntax `list(a.items())` 

### 4. Conditional
#### 4.1 Comparison Operator

| Method | Description | 
| -------- | -------- | 
| `==`   | Equality |
| `>`   | Greater than |
| `>=`   | Greater than or equal |
| `<`   | Less Than |
| `<=`   | Less Than or equal |
| `!=`   | Not Equal |

#### 4.2 Conditional Syntax
- Base Syntax
```
# case 1
if <condition>: 
    <code>

# case 2
if <condition>: 
    <code>
else :
    <code>

# case 3
if <condition_1>: 
    <code>
elif <condition_2>:
    <code>
else :
    <code>    
```

- Ternary operator
```
# variable assignment
# Syntax : variable = <value_if_true> if <condition> else <value_if_false>
# Example
value = 80
x = "Pass" if value>=75 else "Not Pass" # x= "Pass"
```

### 5. Loop
#### 5.1 Loop Control

| Argument | Description | 
| -------- | -------- | 
| pass     | null statement     | 
| continue     | continue to the next iteration, and skip line bellow the argument      | 
| break     | break loop      | 

#### 5.2 While Loop
```
while <condition>:
    <code>
```
> It's important to change the `<condition>` into `False` after meet specific condition. If no, you'll make infinite looping

#### 5.3 For Loop
```
# loop from i=0 to i=n-1
for i in range(n):
    <code>

for x in range(<start>, <end_exclude>, <inc>):
  print(x)
  
# loop in a list, tuple, or set
numbers = [80, 71, 72, 65, 80]
for el in <list>:
    <code>

# loop in a dictionary
data = {"name": "Yudi", isMale: True}
for key in <dictionary>:
    <code>

# access index using enumerate 
for index,area in enumerate(<list>) :
    <code>
```

### 6. Function
- A function is a block of code which only runs when it is called.
#### 6.1 Function
- basic function
```
# Create A Function
def foo():
    <code>

# Call A Function
foo()

# Function with default param
def foo(param1, param2=<default_value>):
    <code>

# Arbitrary Function : 1. args Param 
def foo(*param):
    # param is a tuple
    <code>

# Arbitrary Function : 2. kwargs Param 
def foo(**param):
    # param is a dictionary
    <code>
```

#### 6.2 Lambda Function
- A lambda function is a small anonymous function.
- A lambda function can take any number of arguments, but can only have one expression.
- Syntax : `lambda arguments : expression`
```
# lambda with an argument
f = lambda x : x + 10
print(f(5)) # 15

# lambda with multiple argument
f = lambda x,y : x*y
print(f(5,3)) # 15

```

#### 6.3 Map, Filter, and Reduce

- syntax : `<method>(<function>,<list>)`
- It's a neccessary to import `reduce` from `functools`

```
# Map
double = lambda x: x*2
data = [1,2,3]

result = list(map(double,data))
#result = [2,4,6]

# filter
odd = lambda x: x%2==0
data = [1,2,3]
result = list(filter(odd,data))
# result = [1,3]

# reduce
from functools import reduce

multiply = lambda x,y: x*y
data = [1,2,3]
result = reduce(multiply,data)
# result = 6

```

#### 6.4 Import Library
```
# import a library
# syntax : import <package>
import math
pi = math.pi

# import library using alias
# syntax : import <package> as <alias>
import matplotlib.pyplot as plt
plt.show()

```

### 7. Object Oriented Programming

#### 7.1 Class
```
# define a class
class <Object>:
    <code>

#create an instance
<instance> = <object>()

# constructor function
def __inif__(self, param1, param2):
    self.param1 = param1
    self.param2 = param2
    ...

# class method
def foo(self, param1, param2):
    <code>


# example

class Item:
    pay_rate = 0.8
    all = []
    
    def __init__(self, name:str, price:float, quantity=0):
        # validate input
        assert price>=0, f"price should be greater than or equal to zero"
        assert quantity>=0, f"quantity should be greater than or equal to zero"
        
        # assigning variable
        self.name = name
        self.price = price
        self.quantity = quantity
        
        # add to list
        Item.append(self)
    
    def calculate_total_price(self):
        return(self.price * self.quantity)
        
    def apply_discount(self):
        self.price = self.price * self.pay_rate
    
    def __repr__(self):
        return f"Item ({self.name}, {self.price}, {self.quantity})"
    
    @classmethod
    def printAllItem(cls):
        for instance in Item.all:
            print(instance)
        

laptop = Item("Laptop", 1000, 1)
laptop.apply_discount()
print(laptop.calculate_total_price()) #800

handphone = Item("handphone", 100, 2)
print(Item.all) # access static variable
Item.printAllItem() # access static method

```

#### 7.2 Public, Protected, and Private Variable
- Public variable : The members of a class that are declared public are easily accessible from any part of the program. All data members and member functions of a class are public by default. 
- Protected access Modifier : The members of a class that are declared protected are only accessible to a class derived from it. Data members of a class are declared protected by adding a single underscore ‘_’ symbol before the data member of that class. 
- Private Access Modifier: The members of a class that are declared private are accessible within the class only, private access modifier is the most secure access modifier. Data members of a class are declared private by adding a double underscore ‘__’ symbol before the data member of that class. 

```
class Person:
    __id = None // private
    _name = None // protected
    profession = None // public
    
    def __init__(self, id, name, profession):
        self.__id = id
        self._name = name
        self.profession = profession


    
    
    
    
```

#### 7.2 Getter and Setter
```
class Geek:
    
    def __init__(self, age = 0):
         self.age = age
      
    # getter method
    def get_age(self):
        return self.age
      
    # setter method
    def set_age(self, x):
        self.age = x
  
yudi = Geek()
  
# setting the age using setter
yudi.set_age(21)
  
# retrieving age using getter
print(yudi.get_age())

```
#### 7.3 Inheritance
- Inheritance adalah sifat penurunan, yaitu menurunkan sifat yang dimiliki kelas utama (parent) class kepada kelas yang diturunkan (childc class). Sekarang mari kita coba menerapkan inheritance

```
class Worker:
  def __init__(self, name, id):
      self.name = name
      self.id
      
  def work(self):
    print (f"{self.name} is working")

class Teacher(Worker):
  
  def __init__(self, name, id subject):
    Super().__init__(name, id)
    self.subject = subject
  
  def teach(self):
    print(f"{self.name} is teaching {self.subject}")

yudi = Teacher("Yudi", 1, "Math")
yudi.work()
yudi.teach()

```
- Inheritance : Inheritance adalah sifat penurunan, yaitu menurunkan sifat yang dimiliki kelas utama (parent) class kepada kelas yang diturunkan (childc class). Sekarang mari kita coba menerapkan inheritance

- Encapsulation : Suatu objek pada python dapat kita batasi akses yang dimiliki terhadap objek tersebut dengan menggunakan encapsulation. caranya adalah dengan menggunakan dua garis bawah (__) sebelum nama variabel.

- Polymorphism : Seperti pada namanya, polymophism adalah kemampuan suatu metode memiliki banyak bentuk.
