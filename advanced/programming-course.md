# Advanced Programming Course

## Course Overview

This advanced course covers expert-level topics including system design, microservices, cloud architecture, security, and performance optimization.

---

## Module 1: System Design

### Design Principles

```
System Design Fundamentals
────────────────────────

┌────────────────────────────────────────────┐
│  Scalability                               │
│  ├── Horizontal vs Vertical Scaling        │
│  ├── Load Balancing                       │
│  └── Caching Strategies                   │
├────────────────────────────────────────────┤
│  Reliability                               │
│  ├── Fault Tolerance                      │
│  ├── Redundancy                          │
│  └── Disaster Recovery                   │
├────────────────────────────────────────────┤
│  Maintainability                          │
│  ├── Modularity                          │
│  ├── Observability                       │
│  └── Documentation                       │
└────────────────────────────────────────────┘
```

### Designing for Scale

```python
# Horizontal Scaling
class LoadBalancer:
    def __init__(self, servers):
        self.servers = servers
    
    def route_request(self, request):
        # Round-robin
        server = self.servers[self.current_index]
        self.current_index = (self.current_index + 1) % len(self.servers)
        return server.handle(request)

# Caching
class Cache:
    def __init__(self):
        self.store = {}
    
    def get(self, key):
        if key in self.store:
            return self.store[key]
        return None
    
    def set(self, key, value, ttl=3600):
        self.store[key] = {
            'value': value,
            'expires': time.time() + ttl
        }
```

---

## Module 2: Microservices Architecture

### Microservices Fundamentals

```
Microservices Architecture
─────────────────────────

┌──────────┐ ┌──────────┐ ┌──────────┐
│ Service  │ │ Service  │ │ Service  │
│   A      │ │   B      │ │   C      │
└────┬─────┘ └────┬─────┘ └────┬─────┘
     │            │            │
     └────────────┼────────────┘
                  │
           ┌──────┴──────┐
           │ API Gateway  │
           └─────────────┘
```

### Service Communication

```python
# Service Discovery
class ServiceRegistry:
    def __init__(self):
        self.services = {}
    
    def register(self, service_name, url):
        self.services[service_name] = url
    
    def discover(self, service_name):
        return self.services.get(service_name)

# Inter-service Communication
class ServiceClient:
    def __init__(self, service_name):
        self.service_name = service_name
    
    def call(self, endpoint, data):
        import requests
        url = f"http://{self.service_name}/{endpoint}"
        return requests.post(url, json=data).json()
```

---

## Module 3: Cloud Architecture

### Cloud Services

| Service Type | Examples | Use Case |
|-------------|----------|----------|
| Compute | EC2, Lambda | Running code |
| Storage | S3, EBS | Storing files |
| Database | RDS, DynamoDB | Data storage |
| Networking | VPC, CloudFront | Connectivity |

### AWS Example: Lambda Function

```python
import boto3

def lambda_handler(event, context):
    # Process event
    record = event['Records'][0]
    body = record['Sns']['Message']
    
    # Process data
    result = process_data(body)
    
    # Store result
    s3 = boto3.client('s3')
    s3.put_object(
        Bucket='my-bucket',
        Key='result.json',
        Body=json.dumps(result)
    )
    
    return {
        'statusCode': 200,
        'body': json.dumps(result)
    }
```

### Kubernetes Deployment

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-app
spec:
  replicas: 3
  selector:
    matchLabels:
      app: my-app
  template:
    metadata:
      labels:
        app: my-app
    spec:
      containers:
      - name: my-app
        image: my-app:latest
        ports:
        - containerPort: 8080
        resources:
          limits:
            memory: "128Mi"
            cpu: "500m"
```

---

## Module 4: Security

### Authentication & Authorization

```python
# JWT Token
import jwt

def create_token(user_id):
    payload = {
        'user_id': user_id,
        'exp': datetime.datetime.utcnow() + datetime.timedelta(hours=24)
    }
    return jwt.encode(payload, 'secret_key', algorithm='HS256')

def verify_token(token):
    try:
        payload = jwt.decode(token, 'secret_key', algorithms=['HS256'])
        return payload['user_id']
    except jwt.ExpiredSignatureError:
        return None

# OAuth 2.0 Flow
def get_oauth_token(code):
    response = requests.post('https://oauth.example.com/token', data={
        'grant_type': 'authorization_code',
        'code': code,
        'client_id': 'your_client_id',
        'client_secret': 'your_client_secret'
    })
    return response.json()
```

### Security Best Practices

```python
# Input Validation
def validate_input(data):
    if not isinstance(data.get('email'), str):
        raise ValueError("Invalid email")
    if '@' not in data['email']:
        raise ValueError("Email must contain @")
    
    # Sanitize
    data['email'] = data['email'].strip().lower()
    
    return data

# SQL Injection Prevention (use parameterized queries)
cursor.execute("SELECT * FROM users WHERE id = ?", (user_id,))

# Password Hashing
import bcrypt
hashed = bcrypt.hashpw(password.encode(), bcrypt.gensalt())
```

---

## Module 5: Performance Optimization

### Profiling & Optimization

```python
import cProfile
import pstats

# Profile code
profiler = cProfile.Profile()
profiler.enable()

# Run code to profile
your_function()

profiler.disable()
stats = pstats.Stats(profiler)
stats.sort_stats('cumulative')
stats.print_stats(10)

# Memory profiling
from memory_profiler import profile

@profile
def memory_intensive_function():
    data = [i ** 2 for i in range(1000000)]
    return data
```

### Caching Strategies

```python
# Redis Cache
import redis

r = redis.Redis(host='localhost', port=6379)

def get_with_cache(key, fetch_function, ttl=3600):
    # Check cache
    cached = r.get(key)
    if cached:
        return json.loads(cached)
    
    # Fetch from source
    result = fetch_function()
    
    # Store in cache
    r.setex(key, ttl, json.dumps(result))
    
    return result

# Cache invalidation
def invalidate_cache(key):
    r.delete(key)
```

---

## Module 6: Asynchronous Programming

### Async/Await

```python
import asyncio

async def fetch_data(url):
    async with aiohttp.ClientSession() as session:
        async with session.get(url) as response:
            return await response.json()

async def main():
    # Run multiple requests concurrently
    tasks = [
        fetch_data('https://api.example.com/1'),
        fetch_data('https://api.example.com/2'),
        fetch_data('https://api.example.com/3')
    ]
    
    results = await asyncio.gather(*tasks)
    return results

# Run async
results = asyncio.run(main())
```

### Message Queues

```python
import pika

# Producer
def send_message(queue, message):
    connection = pika.BlockingConnection(
        pika.ConnectionParameters('localhost')
    )
    channel = connection.channel()
    channel.queue_declare(queue=queue, durable=True)
    channel.basic_publish(
        exchange='',
        routing_key=queue,
        body=json.dumps(message),
        properties=pika.BasicProperties(delivery_mode=2)
    )
    connection.close()

# Consumer
def consume_messages(queue):
    connection = pika.BlockingConnection(
        pika.ConnectionParameters('localhost')
    )
    channel = connection.channel()
    
    def callback(ch, method, properties, body):
        data = json.loads(body)
        process_message(data)
        ch.basic_ack(delivery_tag=method.delivery_tag)
    
    channel.basic_qos(prefetch_count=1)
    channel.basic_consume(queue=queue, on_message_callback=callback)
    channel.start_consuming()
```

---

## Module 7: DevOps & CI/CD

### CI/CD Pipeline

```yaml
# .github/workflows/ci.yml
name: CI/CD Pipeline

on:
  push:
    branches: [main]
  pull_request:
    branches: [main]

jobs:
  test:
    runs-on: ubuntu-latest
    
    steps:
    - uses: actions/checkout@v2
    
    - name: Set up Python
      uses: actions/setup-python@v2
      with:
        python-version: '3.9'
    
    - name: Install dependencies
      run: |
        pip install -r requirements.txt
    
    - name: Run tests
      run: |
        pytest tests/
    
    - name: Deploy
      if: github.ref == 'refs/heads/main'
      run: |
        ./deploy.sh
```

### Docker

```dockerfile
# Dockerfile
FROM python:3.9-slim

WORKDIR /app

COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY . .

EXPOSE 8000

CMD ["python", "main.py"]
```

---

## Module 8: Advanced Project

### Complete Distributed System

```python
# Main application with all components

from flask import Flask, request, jsonify
import asyncio
import aiohttp
import redis
import jwt
import boto3

app = Flask(__name__)

# Initialize services
cache = redis.Redis(host='redis', port=6379)
s3 = boto3.client('s3')

# Authentication middleware
@app.before_request
def authenticate():
    token = request.headers.get('Authorization')
    if token:
        try:
            user_id = verify_token(token.replace('Bearer ', ''))
            request.user_id = user_id
        except:
            return jsonify({'error': 'Unauthorized'}), 401

# Main endpoint with caching
@app.route('/api/data')
async def get_data():
    # Check cache first
    cached = cache.get('data')
    if cached:
        return jsonify(json.loads(cached))
    
    # Fetch from multiple services concurrently
    async with aiohttp.ClientSession() as session:
        tasks = [
            fetch_service(session, 'http://service-a/api'),
            fetch_service(session, 'http://service-b/api'),
            fetch_service(session, 'http://service-c/api')
        ]
        results = await asyncio.gather(*tasks)
    
    # Combine results
    combined = {'results': results}
    
    # Cache result
    cache.setex('data', 300, json.dumps(combined))
    
    return jsonify(combined)

async def fetch_service(session, url):
    async with session.get(url) as response:
        return await response.json()

# Health check
@app.route('/health')
def health():
    return jsonify({'status': 'healthy'})

if __name__ == '__main__':
    app.run(debug=False, host='0.0.0.0', port=8000)
```

---

## Module 9: Career & Beyond

### Expert Skills

```markdown
## What Makes an Expert

1. **Deep Understanding**
   - Know WHY, not just HOW
   - Understand trade-offs
   - Can debug complex issues

2. **System Thinking**
   - See the big picture
   - Understand dependencies
   - Design for failure

3. **Continuous Learning**
   - Stay updated
   - Read source code
   - Contribute to open source

4. **Communication**
   - Explain complex topics
   - Write documentation
   - Mentor others
```

### Resources for Growth

- Read technical books
- Contribute to open source
- Attend conferences
- Build side projects
- Teach others

---

## Congratulations!

You've completed the Advanced Programming Course! You're now ready to tackle complex engineering challenges and build production-ready systems.

**Keep learning and building!** 🚀
