---
title: 6 - Python Strings
tags:
  - Python
  - W3schools
  - Strings
  - Check
---

### 💬 Strings

📝 Strings in python are surrounded by either single quotation marks, or double quotation marks.

📝 **'hello'** is the same as **"hello"**.

📝 You can display a string literal with the **print()** function:

📝 Example

```python
#You can use double or single quotes:

print("Hello")
print('Hello')

```

▶️ Result

```
Hello
Hello
```


^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
### 💬 Assign String to a Variable

📝 Assigning a string to a variable is done with the variable name followed by an equal sign and the string:

📝 Example

```python
a = "Hello"
print(a)
```

▶️ Result

```
Hello
```

^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
### 💬 Multiline Strings

📝 Example

```python
a = """Lorem ipsum dolor sit amet,
consectetur adipiscing elit,
sed do eiusmod tempor incididunt
ut labore et dolore magna aliqua."""
print(a)
```

📝 Or three single quotes:

```python
a = '''Lorem ipsum dolor sit amet,
consectetur adipiscing elit,
sed do eiusmod tempor incididunt
ut labore et dolore magna aliqua.'''
print(a)
```

▶️ Result

```
Lorem ipsum dolor sit amet,
consectetur adipiscing elit,
sed do eiusmod tempor incididunt
ut labore et dolore magna aliqua.
```

^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
### 💬 Strings are Arrays

📝 Example

```python
a = "Hello, World!"
print(a[1])
```

▶️ Result

```
e
```

^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
### 💬  Looping Through a String

📝 Since strings are arrays, we can loop through the characters in a string, with a **for** loop.

📝 Example

📝 Loop through the letters in the word "banana":

```python
for x in "banana":
    print(x) 

```

▶️ Result


```
b
a
n
a
n
a
```

^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
### 💬 String Length

📝 Example

📝 The len() function returns the length of a string:

```python
a = "Hello, World!"
print(len(a))
```

▶️ Result

```
13
```

^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
### 💬  Check String

📝 Example

📝 Check if "free" is present in the following text:

```python
txt = "The best things in life are free!"
print("free" in txt)
```

▶️ Result

```
True

```

^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
### 💬  Use it in an if statement:

📝 Example

📝 Print only if "free" is present:

```python
txt = "The best things in life are free!"
if "free" in txt:
    print("Yes, 'free' is present.")
```

▶️ Result

```
Yes, 'free' is present.
```


### 💬 Check if NOT

📝 To check if a certain phrase or character is NOT present in a string, we can use the keyword **not in**.

📝 Example

📝 Check if "expensive" is NOT present in the following text:

```python
txt = "The best things in life are free!"
print("expensive" not in txt)

```

▶️ Result

```
True
```

📝 Use it in an if statement:

📝 Example

📝 print only if "expensive" is NOT present:

```python
txt = "The best things in life are free!"
if "expensive" not in txt:
    print("Yes, 'expensive' is NOT present.")
```

▶️ Result

```
Yes, 'expensive' is NOT present.
```
