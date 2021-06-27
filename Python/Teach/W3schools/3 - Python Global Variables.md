---
title: 3 - Python Global Variables
tags:
  - Python
  - Variable
  - Global
  - W3schools
---

### 💬 Global Variables

📝 Example 1

```python
x = "awesome"

def myfunc():
    print("Python is " + x)

myfunc()
```

▶️ Result

```
Python is awesome
```


📝 Example 2

```python
x = "awesome"

def myfunc():
    x = "fantastic"
    print("Python is " + x)

myfunc()

print("Python is " + x)

```

▶️ Result

```
Python is fantastic
Python is awesome
```

^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

### 💬  The global Keyword

📝 Example 3

```python
def myfunc():
    global x
    x = "fantastic"

myfunc()

print("Python is " + x)


```

▶️ Result

```
Python is fantastic
```


📝 Example 4

```python
x = "awesome"

def myfunc():
    global x
    x = "fantastic"

myfunc()

print("Python is " + x)



```

▶️ Result

```
Python is fantastic
```
