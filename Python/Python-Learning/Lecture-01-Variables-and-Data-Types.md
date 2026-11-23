# Lecture 01: Variables and Data Types

## What is Python?

- Python is simple & easy.
- Free & Open Source.
- High-Level Language.
- Developed by Guido van Rossum.
- Portable.

## Python Installation & Setup

We have to download Python from the official Python webpage and also have to download Visual Studio Code for running Python.

## Our First Program

```python
# Input
print("Hello world")
print("My age is 20")

print("My name is Sakib.", "My age is 20")

print(23 + 50)

# Output
Hello world
My age is 20
My name is Sakib. My age is 20
73
```

Here, `print` is a function which is used for getting output.

## Variables

**A Variable is a name given to a memory location in a program.**

```python
# Input
name = "john"  # string
age = 20
price = 25.99

print(name)
print(age)
print("my name is: ", name)
print("my age is: ", age)

# Output
john
20
my name is: john
my age is: 20
```

Here, we can get the output of a value by simply printing the variable name.

## Rules for Identifiers

1. Identifiers can be a combination of uppercase and lowercase letters, digits or an underscore (_).

   So `myVariable`, `variable_1`, `variable_for_print` are all valid Python identifiers.

2. An Identifier cannot start with a digit. So while `variable1` is valid, `1variable` is not valid.

3. We can't use special symbols like !, #, @, %, $ etc. in our Identifier.

4. Identifier can be of any length.

## Data Types

It tells us which types of values we add to a variable.

- **Integers →** +ve, -ve [ 25, -25 ]
- **String →** "john", 'sakib'
- **Float →** 30.50, 3.00
- **Boolean →** True, False
- **None →** a = None

```python
# Input
name = "john"
age = 20
price = 25.99
Old = False
a = None

print(type(name))
print(type(age))
print(type(price))
print(type(Old))
print(type(a))

# Output
<class 'str'>
<class 'int'>
<class 'float'>
<class 'bool'>
<class 'NoneType'>
```

## Keywords

Keywords are some **reserved words** in Python which are specifically used for Python's specified meaning. Also, we cannot use them as a variable name.

| and      | else    | in       | return |
| -------- | ------- | -------- | ------ |
| as       | except  | is       | True   |
| assert   | finally | lambda   | try    |
| break    | False   | nonlocal | with   |
| class    | for     | None     | while  |
| continue | match   | not      | yield  |
| def      |         | or       |        |
| del      | if      | pass     |        |
| elif     | import  | raise    |        |

## Print Sum & Diff

```python
a = 5000
b = 1000

sum = a + b
diff = a - b

print(sum)
print(diff)

# Output
6000
4000
```

## Comments in Python

It's a part of a program which is never executed.

We start a single-line comment with (#) and multiline comments with (""" ... """).

```python
print("hello world")

# world is beautiful

"""
Friday
Saturday
"""

# Output
hello world
```

## Types of Operators

An operator is a symbol that performs a certain operation between operands.

- **Arithmetic Operators** ( +, -, *, /, %, ** )
- **Relational / Comparison Operators** ( ==, !=, >, <, >= )
- **Assignment Operators** ( =, +=, -=, *=, %=, /=, **= )
- **Logical Operators** ( not, and, or )

```python
# Arithmetic Operators
a = 5
b = 2

print(a + b)
print(a - b)
print(a * b)
print(a / b)
print(a % b)  # remainder
print(a ** b)  # a^b

# Relational Operators
a = 50
b = 20

print(a == b)  # False
print(a != b)  # True
print(a >= b)  # True

# Output
False
True
True

# Assignment Operators

num = 10
num = num + 10  # 10+10 => 20
num += 10
num -= 5
num *= 5
num %= 5
num /= 5
num **= 5

print("num : ", num)

# Output
num :  0.0

# Logical Operators
a = 50
b = 20

# not
print(not False)
print(not (a > b))

# and
val1 = True
val2 = False

print("And operators:", val1 and val2)

# OR
print("OR operators:", (a == b) or (a > b))

# Output
True
False
And operators: False

OR operators: True

# If one value is False, it prints False.
# When both values are True, it prints True.
# OR: If one value is True, it prints True.
```

## Type Conversion

It means we can convert one type of value into another type. Python does it automatically.

## Type Casting

Here, we have to convert a value forcefully from one type to another type.

```python
# Type Conversion
a = 3
b = 4.25

sum = a + b  # 3.0 + 4.25
print(sum)

# Output
7.25

# Type Casting
a = int("2")
b = 4.25

print(a + b)

# Output
6.25
```

## Input in Python

**input()** statement is used to accept a value (using the keyboard) from the user.

`input()` always returns a **str**.

```python
name = input("Enter your name: ")
print("Welcome", name)

name = input("Enter name: ")
age = int(input("Enter age: "))
mark = float(input("Enter marks: "))

print("Welcome", name)
print("Your age:", age)
print("Your mark:", mark)
```

## Let's Practice

### 1. Write a program to input two numbers & print their sum.

```python
first = int(input("Enter first num: "))
second = int(input("Enter second num: "))

print("sum =", first + second)
```

### 2. WAP to input the side of a square & print the area.

```python
side = float(input("Enter square side: "))

print("area =", side * side)
```

### 3. Enter 2 floating numbers & print their average.

```python
a = float(input("Enter first num: "))
b = float(input("Enter second num: "))

print("avg =", (a + b) / 2)
```

### 4. WAP to input 2 int numbers a & b. Print True if a is greater than b or a = b. If not, print False.

```python
a = int(input("Enter first num: "))
b = int(input("Enter second num: "))

print(a >= b)
```
