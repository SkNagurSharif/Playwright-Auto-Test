# JWT Token Management in Playwright BDD Project (TypeScript and Python)

## Overview
This document explains how to manage JSON Web Tokens (JWT) in a Playwright BDD project using both TypeScript and Python. JWTs are commonly used for authentication and can be generated, stored, and utilized within your application.

## What is a JWT?
A JSON Web Token (JWT) is a compact, URL-safe means of representing claims to be transferred between two parties. The claims in a JWT are encoded as a JSON object that is used as the payload of a JSON Web Signature (JWS) structure.

## Generating a JWT

### TypeScript Example
To generate a JWT in a Node.js application using TypeScript, you can use the `jsonwebtoken` library:

```typescript
import jwt from 'jsonwebtoken';

const secretKey = 'your_secret_key'; // Use a secure key
const payload = {
    userId: '12345',
    username: 'exampleUser',
};

const token = jwt.sign(payload, secretKey, { expiresIn: '1h' });
console.log(token);
```

### Python Example
To generate a JWT in a Python application, you can use the `PyJWT` library:

```python
import jwt
import datetime

secret_key = 'your_secret_key'  # Use a secure key
payload = {
    'userId': '12345',
    'username': 'exampleUser',
    'exp': datetime.datetime.utcnow() + datetime.timedelta(hours=1)  # Token expiration
}

token = jwt.encode(payload, secret_key, algorithm='HS256')
print(token)
```

## Storing the JWT

### TypeScript Example
Once you have generated the JWT, you can store it in local storage using Playwright:

```typescript
await page.evaluate((token) => {
    localStorage.setItem('jwt', token);
}, token);
```

### Python Example
In a Python application, you might store the JWT in a session or a cookie, depending on your web framework. Here’s an example using Flask:

```python
from flask import Flask, session

app = Flask(__name__)
app.secret_key = 'your_flask_secret_key'

@app.route('/login', methods=['POST'])
def login():
    # After successful login
    session['jwt'] = token  # Store the JWT in the session
```

## Using the JWT in Requests

### TypeScript Example
To use the stored JWT in your API requests, retrieve it from local storage:

```typescript
const token = await page.evaluate(() => localStorage.getItem('jwt'));

await page.goto('https://example.com/protected-resource', {
    headers: {
        Authorization: `Bearer ${token}`,
    },
});
```

### Python Example
In Python, you can retrieve the JWT from the session and include it in your requests:

```python
import requests

@app.route('/protected-resource')
def protected_resource():
    token = session.get('jwt')
    headers = {'Authorization': f'Bearer {token}'}
    response = requests.get('https://example.com/protected-resource', headers=headers)
    return response.json()
```

## Clearing the JWT

### TypeScript Example
When the user logs out, clear the JWT from local storage:

```typescript
await page.evaluate(() => {
    localStorage.removeItem('jwt');
});
```

### Python Example
In Python, clear the JWT from the session upon logout:

```python
@app.route('/logout')
def logout():
    session.pop('jwt', None)  # Remove the JWT from the session
    return 'Logged out'
```

## Encrypting and Decrypting JWTs

### TypeScript Example
To encrypt and decrypt JWTs in TypeScript, you can use the `jsonwebtoken` library along with a secure key. Here’s how to do it:

#### Encrypting a JWT
```typescript
import jwt from 'jsonwebtoken';

const secretKey = 'your_secret_key'; // Use a secure key
const payload = {
    userId: '12345',
    username: 'exampleUser',
};

const token = jwt.sign(payload, secretKey, { expiresIn: '1h' });
console.log('Encrypted Token:', token);
```

#### Decrypting a JWT
```typescript
const decoded = jwt.verify(token, secretKey);
console.log('Decoded Token:', decoded);
```

### Python Example
In Python, you can use the `PyJWT` library to encrypt and decrypt JWTs:

#### Encrypting a JWT
```python
import jwt
import datetime

secret_key = 'your_secret_key'  # Use a secure key
payload = {
    'userId': '12345',
    'username': 'exampleUser',
    'exp': datetime.datetime.utcnow() + datetime.timedelta(hours=1)  # Token expiration
}

token = jwt.encode(payload, secret_key, algorithm='HS256')
print('Encrypted Token:', token)
```

#### Decrypting a JWT
```python
decoded = jwt.decode(token, secret_key, algorithms=['HS256'])
print('Decoded Token:', decoded)
```

## Conclusion
Managing JWT tokens in your Playwright BDD project allows for efficient authentication. By generating, storing, encrypting, and using JWTs in both TypeScript and Python, you can maintain user sessions and secure access to protected resources. Ensure that you handle tokens securely and clear them when no longer needed.
