**Strings**

Strings are a data type that stores a sequence of characters.

```python
str1 = "this is a string .\n we use backslash n as an escape character for the next line "
str2 = 'my name is sakib '
print(str1)

```

**Basic Operation**

1. **concatenation**

“hello” + “world”   —> “helloworld”

```python
str1 = "my name is "
str2 = "sakib "
final_str = (str1+str2)
print(final_str)

```

1. **length of str [ len(str) ]**

we count the length of str using this **len** function .

```python
str1 = "i love bangladesh"
len1 = len(str1)
print(len1)

str2 = "what is your name "
len2 = len(str2)
print(len2)

final_str = str1 + " " + str2
print(final_str)
print(len(final_str))

```

**Indexing**

It is a process to read specific characters inside a string . [ index counting always starts from 0 - …. ]

```python
str = "love bangladesh"
ch = str[2]
print(ch) #or
print(str[0])

```

**Slicing**

Accessing parts of a string .

str[ starting_idx : ending_idx ]

str = “b**ang**ladesh”

str[ 1 : 4 ] is “ang”

```python
str = "cyber24 academy"
print(str[1:4])
print(str[0:5])
print(str[5:len(str)])

#negative index
str = "apple"
print(str[-5:-2])

```

**String Functions**

str = “I am a hacker”

str.**endswith**(”er”)  #returns True if string ends with substr

str.**capitalize**( )   #capitalizes 1st char

str.**replace**( old , new )  #replaces all occurrences of old

str.**find**( word )   #returns the index of the first occurrence

str.**count**(”am”)   #counts the occurrences of substr

we can also know about lots of functions inside Visual Studio by typing (str.)

```python

str = "i am a hacker"
print(str.endswith("ker"))
print(str.endswith("ash"))

print(str.capitalize())

str = "i am learning python on youtube"
print(str.replace("o", "a"))
print(str.replace("learning", "studying"))

str = "i am learning python on youtube"
print(str.find("o"))
print(str.find("python"))

print(str.count("on"))

```

**Let's Practice**

WAP to input user's first name & print its length .

```python
first = input("enter your name :")
print("length of your name :", len(first))

```

WAP to find the occurrence of ‘$’ in a string .

```python
str = "i earn $10 and my friend salary is $1000"
print(str.find("$"))
print(str.count("$"))

```

**Conditional Statement**

**if - elif - else** (SYNTAX)

```python
if (condition):

    Statement 1

elif (condition):

    Statement 2

else:

    StatementN
```

```python
#if
age = int(input("enter your age :"))
if(age >= 18):
    print("Welcome .\nyou can vote & apply for licence")

#elif
light = "green"
if(light == "red"):
    print("stop")
elif(light == "green"):
    print("go")
elif(light == "yellow"):
    print("look")

#else
light = "pink"
if(light == "red"):
    print("stop")
elif(light == "green"):
    print("go")
elif(light == "yellow"):
    print("look")
else:
    print("light is broken")


#Print students grade
marks = int(input("enter students marks:"))
if marks >= 80:
    grade = "A+"
elif marks >= 70 and marks < 80:
    grade = "A"
elif marks >= 60 and marks < 70:
    grade = "A-"
elif marks >= 33 and marks < 60:
    grade = "pass"
else:
    grade = "fail"

print("your grade:", grade)

#nesting
age = 25
if(age >= 18):
    if age >= 80:
        print("cannot drive")
    else:
        print("can drive")
else:
    print("cannot drive")

```

**Let's Practice**

WAP to check if a num entered by the user is odd or even. [WAP = write a program]

```python
num = int(input("enter your num:"))

if num % 2 == 0:
    print("Even")
else:
    print("Odd")

```

WAP to find the greatest of 3 numbers entered by user.

```python

a = int(input("enter first num:"))
b = int(input("enter second num:"))
c = int(input("enter third num:"))

if a >= b and a >= c:
    print("first number is largest:", a)
elif b >= c:
    print("second number is largest:", b)
else:
    print("third number is largest:", c)

```

WAP to check if a num is a multiple of 7 or not .

```python
x = int(input("enter your num:"))
if x % 7 == 0:
    print("multiple of 7 yes")
else:
    print("not")

```
