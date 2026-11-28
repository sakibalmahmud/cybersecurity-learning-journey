# Lists in Python

A built-in data type that stores a set of values.

It can store elements of different types (**integer, float, string, etc.**).

```python
marks = [87, 58, 76]  # marks[0], marks[1]...
student = ["Karan", 85, "Dhaka"]  # student[0], student[1]...

student[0] = "Arjun"  # allowed in Python
```

```python
marks = [95.2, 85.3, 66.4, 70.3]
print(marks)
print(type(marks))
print(marks[0])
print(marks[1])

student = ["sakib", 90.5, 20, "sylhet"]
print(student[0])
student[0] = "arif"
print(student)
```

**List Slicing**

Similar to String Slicing.

```python
list_name[starting_idx : ending_idx]
```

```python
marks = [50, 85, 75, 78, 45]
print(marks[1:4])
```

**List Methods**

```python
list = [1, 2, 3]
```

- `list.append(4)`  # adds one element at the end
- `list.sort()`  # sorts in ascending order
- `list.sort(reverse=True)`  # sorts in descending order
- `list.reverse()`  # reverses the list
- `list.insert(idx, el)`  # inserts an element at the specified index
- `list.remove(1)`  # removes the first occurrence of the value
- `list.pop(idx)`  # removes the element at the specified index

```python
list = [1, 2, 3]
list.append(4)
print(list)

list = [2, 1, 3, 5]
list.sort()
print(list)  # list in ascending order

list = [2, 1, 3, 5]
list.sort(reverse=True)
print(list)  # list in descending order

list = [2, 1, 3, 5]
list.reverse()
print(list)

list = [2, 1, 3]
list.insert(1, 5)
print(list)

list = [2, 1, 3, 1]
list.pop(2)
print(list)
```

**Tuples in Python**

A built-in data type that lets us create **immutable** sequences of values.

```python
tup = (2, 1, 3, 1)  # immutable, meaning we cannot change its elements
print(tup[0])
print(tup[1])

print(tup[1:3])
```

**Tuple Methods**

```python
tup = (2, 1, 3, 1)
```

- `tup.index(el)`  # returns the index of the first occurrence
- `tup.count(el)`  # counts the total occurrences

```python
tup = (1, 2, 5, 4, 1)
print(tup.index(2))
print(tup.count(1))
```

**Let's Practice**

**1. WAP to ask the user to enter the names of their 3 favorite movies and store them in a list.**

```python
moves = []
moves.append(input("enter 1st movie: "))
moves.append(input("enter 2nd movie: "))
moves.append(input("enter 3rd movie: "))

print(moves)
```

**2. WAP to check if a list contains a palindrome of elements.**

```python
list1 = [1, 2, 3, 1]
list2 = [1, 2, 3, 4]

copy_list1 = list1.copy()
copy_list1.reverse()

if copy_list1 == list1:
    print("palindrome")
else:
    print("not palindrome")
```
