---
title: 7 - Python - Slicing Strings
tags:
  - Python
  - W3schools
  - Strings
  - Slicing
---

### 💬 Slicing

📝 You can return a range of characters by using the slice syntax.
📝 Specify the start index and the end index, separated by a colon, to return a part of the string.

📝 Example

📝  Get the characters from position 2 to position 5 (not included):

```python
b = "Hello, World!"
print(b[:5])
```

▶️ Result


```
Hello
```

^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
### 💬 Slice To the End

📝 Example

📝 Get the characters from position 2, and all the way to the end:

```python
b = "Hello, World!"
print(b[2:])
```

▶️ Result


```
llo, World!
```

^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
### 💬 Negative Indexing

📝 Example

📝 Use negative indexes to start the slice from the end of the string:

```python
b = "Hello, World!"
print(b[-5:-2])
```

▶️ Result

```
orl

```
