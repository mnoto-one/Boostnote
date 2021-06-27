---
title: 2 - Python Variables
tags:
  - Python
  - Variable
  - W3schools
---

### 💬  Creating Variables

```python
x = 5
y = "John"
print(x)
print(y)
```

▶️ Result

```
5
John
```

^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

📝 Variables do not need to be declared with any particular type, and can even change type after they have been set.

📝 Example


```python
x = 4
x = "Sally"
print(x)

```

▶️ Result

```
Sally
```

^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^


📝 Variables do not need to be declared with any particular type, and can even change type after they have been set.

📝 Example


```python
x = 4
x = "Sally"
print(x)

```

▶️ Result

```
Sally
```

^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

### 💬  Casting

📝 If you want to specify the data type of a variable, this can be done with casting.


📝 Example

```python
x = str(3)    # x will be '3'
y = int(3)    # y will be 3
z = float(3)  # z will be 3.0

```

▶️ Result

```
3
3
3.0
```

^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

### 💬  Case-Sensitive

📝 Variable names are case-sensitive.

📝 Example

```python
a = 4
A = "Sally"

print(a)
print(A)


```

▶️ Result

```
4
Sally
```

^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

### 💬  Variable Names

📝 Legal variable names:

📝 Example

```python
myvar = "John"
my_var = "John"
_my_var = "John"
myVar = "John"
MYVAR = "John"
myvar2 = "John"


print(myvar)
print(my_var)
print(_my_var)
print(myVar)
print(MYVAR)
print(myvar2)


```

▶️ Result

```
John
John
John
John
John
John
```

📝 Illegal variable names:

📝 Example

```python
2myvar = "John"
my-var = "John"
my var = "John"

#This example will produce an error in the result


```

▶️ Result

```
Error
```

^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

### 💬  Python Variables - Assign Multiple Values

📝 Many Values to Multiple Variables

📝 Python allows you to assign values to multiple variables in one line:

📝 Example

```python
x, y, z = "Orange", "Banana", "Cherry"

print(x)
print(y)
print(z)


```

▶️ Result

```
Orange
Banana
Cherry
```


📝 One Value to Multiple Variables

📝 Example

```python
x = y = z = "Orange"

print(x)
print(y)
print(z)
```

▶️ Result

```
Orange
Orange
Orange
```

📝 Unpack a Collection

📝 Array

📝 Example

```python
fruits = ["apple", "banana", "cherry"]
x, y, z = fruits

print(x)
print(y)
print(z)

```

▶️ Result

```
apple
banana
cherry
```

^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

### 💬 Python - Output Variables

📝 The Python **print** statement is often used to output variables.

📝 To combine both text and a variable, Python uses the **+** character:

📝 Example

```python
x = "awesome"
print("Python is " + x)

```

▶️ Result

```
Python is awesome
```

📝 You can also use the + character to add a variable to another variable:



📝 Example

```python
x = "Python is "
y = "awesome"
z = x + y
print(z)

```

▶️ Result

```
Python is awesome
```


📝 For numbers, the + character works as a mathematical operator:





📝 Example

```python
x = 5
y = 10
print(x + y)
```

▶️ Result

```
15
```
