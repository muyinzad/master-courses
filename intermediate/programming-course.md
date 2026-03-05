# Intermediate Programming Course

## Course Overview

This course builds on the basics and introduces more advanced programming concepts including object-oriented programming, databases, APIs, and web development.

---

## Module 1: Object-Oriented Programming

### Classes and Objects

```python
# Create a class
class Dog:
    def __init__(self, name, breed):
        self.name = name
        self.breed = breed
    
    def bark(self):
        print(f"{self.name} says woof!")
    
    def get_info(self):
        return f"{self.name} is a {self.breed}"

# Create objects
my_dog = Dog("Buddy", "Golden Retriever")
my_dog.bark()
print(my_dog.get_info())
```

### Class Inheritance

```python
class Animal:
    def __init__(self, name):
        self.name = name
    
    def speak(self):
        pass

class Cat(Animal):
    def speak(self):
        return "Meow!"

class Dog(Animal):
    def speak(self):
        return "Woof!"

# Use inheritance
cat = Cat("Whiskers")
dog = Dog("Buddy")

print(cat.speak())  # Meow!
print(dog.speak())  # Woof!
```

---

## Module 2: Working with APIs

### What is an API?

An API (Application Programming Interface) allows programs to communicate with each other.

### Making API Requests

```python
import requests

# GET request
response = requests.get("https://api.example.com/data")
data = response.json()
print(data)

# POST request
new_data = {"name": "John", "age": 30}
response = requests.post("https://api.example.com/users", json=new_data)
print(response.status_code)
```

### Building a Simple API

```python
from flask import Flask, jsonify

app = Flask(__name__)

@app.route('/api/hello')
def hello():
    return jsonify({"message": "Hello, World!"})

@app.route('/api/users/<int:user_id>')
def get_user(user_id):
    return jsonify({"id": user_id, "name": "John"})

if __name__ == '__main__':
    app.run(debug=True)
```

---

## Module 3: Database Basics

### SQL Fundamentals

```sql
-- Create a table
CREATE TABLE users (
    id INTEGER PRIMARY KEY,
    name TEXT NOT NULL,
    email TEXT UNIQUE
);

-- Insert data
INSERT INTO users (name, email) VALUES ('John', 'john@email.com');

-- Query data
SELECT * FROM users;
SELECT name FROM users WHERE id = 1;

-- Update data
UPDATE users SET name = 'Jane' WHERE id = 1;

-- Delete data
DELETE FROM users WHERE id = 1;
```

### Python with SQLite

```python
import sqlite3

# Connect to database
conn = sqlite3.connect('mydatabase.db')
cursor = conn.cursor()

# Create table
cursor.execute('''CREATE TABLE users 
    (id INTEGER PRIMARY KEY, name TEXT, email TEXT)''')

# Insert data
cursor.execute("INSERT INTO users (name, email) VALUES (?, ?)", 
    ('John', 'john@email.com'))

# Query data
cursor.execute("SELECT * FROM users")
results = cursor.fetchall()

for row in results:
    print(row)

conn.commit()
conn.close()
```

---

## Module 4: Web Development Basics

### HTML Structure

```html
<!DOCTYPE html>
<html>
<head>
    <title>My Website</title>
</head>
<body>
    <h1>Welcome!</h1>
    <p>This is my website.</p>
    <a href="about.html">About</a>
</body>
</html>
```

### CSS Styling

```css
body {
    font-family: Arial, sans-serif;
    background-color: #f0f0f0;
}

h1 {
    color: blue;
    text-align: center;
}

.container {
    max-width: 800px;
    margin: auto;
    padding: 20px;
}
```

### JavaScript Interactivity

```javascript
// Change content
document.getElementById("demo").innerHTML = "Hello JavaScript!";

// Handle click
function myFunction() {
    alert("Button clicked!");
}

// Fetch data
fetch('https://api.example.com/data')
    .then(response => response.json())
    .then(data => console.log(data));
```

---

## Module 5: Testing Code

### Writing Tests

```python
import unittest

def add(a, b):
    return a + b

class TestMath(unittest.TestCase):
    def test_add(self):
        self.assertEqual(add(2, 3), 5)
        self.assertEqual(add(-1, 1), 0)
        self.assertEqual(add(0, 0), 0)

if __name__ == '__main__':
    unittest.main()
```

### Test-Driven Development

```python
# Write test first
def test_calculator():
    assert calculator.add(2, 3) == 5
    assert calculator.subtract(10, 5) == 5

# Then write code
class Calculator:
    def add(self, a, b):
        return a + b
    
    def subtract(self, a, b):
        return a - b
```

---

## Module 6: Version Control

### Git Basics

```bash
# Initialize repository
git init

# Add files
git add .
git commit -m "Initial commit"

# Create branch
git checkout -b new-feature

# Merge branch
git checkout main
git merge new-feature

# Push to remote
git push origin main
```

### Working with GitHub

```bash
# Clone repository
git clone https://github.com/user/repo.git

# Pull changes
git pull origin main

# Create pull request
# (via GitHub web interface)
```

---

## Module 7: Intermediate Project

### Build a REST API

```python
from flask import Flask, jsonify, request
import sqlite3

app = Flask(__name__)

# Initialize database
def init_db():
    conn = sqlite3.connect('app.db')
    c = conn.cursor()
    c.execute('''CREATE TABLE IF NOT EXISTS items 
                 (id INTEGER PRIMARY KEY, name TEXT, price REAL)''')
    conn.commit()
    conn.close()

# Get all items
@app.route('/api/items', methods=['GET'])
def get_items():
    conn = sqlite3.connect('app.db')
    c = conn.cursor()
    c.execute("SELECT * FROM items")
    items = [{"id": row[0], "name": row[1], "price": row[2]} 
             for row in c.fetchall()]
    conn.close()
    return jsonify(items)

# Add item
@app.route('/api/items', methods=['POST'])
def add_item():
    data = request.json
    conn = sqlite3.connect('app.db')
    c = conn.cursor()
    c.execute("INSERT INTO items (name, price) VALUES (?, ?)",
              (data['name'], data['price']))
    conn.commit()
    conn.close()
    return jsonify({"message": "Item added"}), 201

if __name__ == '__main__':
    init_db()
    app.run(debug=True)
```

---

## Module 8: Next Steps

### Topics to Explore

- **Frameworks**: Django, Flask, FastAPI
- **ORMs**: SQLAlchemy, Prisma
- **Authentication**: JWT, OAuth
- **Deployment**: Docker, AWS, Heroku

### Practice Projects

1. Blog application
2. Todo list app
3. REST API
4. Weather app

---

## Congratulations!

You've completed the intermediate course! Continue to the Advanced course for expert-level content.
