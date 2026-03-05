# Beginner Programming Course

## Course Overview

Welcome to the Beginner Programming Course! This course is designed for people with no prior programming experience. You'll learn the fundamentals of programming using Python.

---

## Module 1: Getting Started

### What is Programming?

Programming is giving instructions to a computer to perform specific tasks. Like following a recipe, you write steps that the computer executes.

### Your First Program

```python
print("Hello, World!")
```

This simple line of code tells the computer to display "Hello, World!" on the screen.

### Variables

Variables are like labeled containers that store information:

```python
# Creating variables
name = "John"
age = 25
height = 5.9
is_student = True

print(name)
print(age)
```

### Data Types

| Type | Example | Description |
|------|---------|-------------|
| String | "Hello" | Text |
| Integer | 42 | Whole numbers |
| Float | 3.14 | Decimal numbers |
| Boolean | True/False | Yes/No values |

---

## Module 2: Making Decisions

### Comparison Operators

```python
# Compare values
10 > 5      # True
10 == 10    # True (equal)
10 != 5     # True (not equal)
```

### If Statements

Make decisions in your code:

```python
age = 18

if age >= 18:
    print("You can vote!")
else:
    print("You're too young to vote.")
```

### Multiple Conditions

```python
age = 25
has_license = True

if age >= 18 and has_license:
    print("You can drive!")
```

---

## Module 3: Repeating Tasks

### For Loops

Repeat actions a specific number of times:

```python
# Count from 1 to 5
for i in range(1, 6):
    print(i)

# Loop through a list
fruits = ["apple", "banana", "cherry"]
for fruit in fruits:
    print(fruit)
```

### While Loops

Repeat while a condition is true:

```python
count = 0

while count < 5:
    print(count)
    count = count + 1
```

---

## Module 4: Organizing Data

### Lists

Store multiple items in one variable:

```python
# Create a list
colors = ["red", "green", "blue"]

# Add to list
colors.append("yellow")

# Get items
print(colors[0])    # First item
print(colors[-1])   # Last item

# Loop through
for color in colors:
    print(color)
```

### Dictionaries

Store key-value pairs:

```python
# Create dictionary
person = {
    "name": "Alice",
    "age": 30,
    "city": "New York"
}

# Get values
print(person["name"])
print(person.get("age"))

# Add new item
person["job"] = "Engineer"
```

---

## Module 5: Reusable Code

### Functions

Create reusable blocks of code:

```python
# Define a function
def greet(name):
    print("Hello, " + name + "!")

# Call the function
greet("John")
greet("Alice")
```

### Functions with Return Values

```python
def add_numbers(a, b):
    return a + b

result = add_numbers(5, 3)
print(result)  # 8
```

---

## Module 6: Working with Files

### Reading Files

```python
# Read a file
with open("myfile.txt", "r") as file:
    content = file.read()
    print(content)
```

### Writing Files

```python
# Write to a file
with open("myfile.txt", "w") as file:
    file.write("Hello, World!")
```

---

## Module 7: Error Handling

### Try/Except

Handle errors gracefully:

```python
try:
    result = 10 / 0
except ZeroDivisionError:
    print("Cannot divide by zero!")
except Exception as e:
    print("Error: " + str(e))
```

---

## Module 8: Final Project

### Build a Simple Calculator

```python
def calculator():
    print("Simple Calculator")
    print("1. Add")
    print("2. Subtract")
    print("3. Multiply")
    print("4. Divide")
    
    choice = input("Enter choice (1-4): ")
    num1 = float(input("Enter first number: "))
    num2 = float(input("Enter second number: "))
    
    if choice == '1':
        print(num1 + num2)
    elif choice == '2':
        print(num1 - num2)
    elif choice == '3':
        print(num1 * num2)
    elif choice == '4':
        print(num1 / num2)

calculator()
```

---

## What's Next?

You've completed the beginner course! Continue to the Intermediate course to learn more advanced concepts.

**Next Steps:**
- Practice coding daily
- Build small projects
- Join coding communities
