# User Service

A standalone GraphQL service to handle user operations.

## Installation

```node
cd user-service
npm install
```

```
-- set the password for the built-in "postgres" user
ALTER USER postgres
  WITH ENCRYPTED PASSWORD '191102';

\c postgres

-- create the "personnel" database
CREATE DATABASE personnel
  WITH 
    OWNER = postgres
    ENCODING = 'UTF8'
    LC_COLLATE = 'en_US.utf8'
    LC_CTYPE = 'en_US.utf8'
    TEMPLATE = template0;

-- enable UUID generation
CREATE EXTENSION IF NOT EXISTS "uuid-ossp";

-- seed sample users
INSERT INTO "Users" 
  ("userId", "username", "email", "password", "role", "createdAt", "updatedAt")
VALUES
  (
    uuid_generate_v4(),
    'manager_anna',
    'anna.manager@example.com',
    '$2b$10$7uPmZ1y9Kq3A6a1byIN.X.crUh5o1T2pC1N1TfzOX54dJzwwMJDfS',
    'MANAGER',
    NOW(),
    NOW()
  ),
  (
    uuid_generate_v4(),
    'member_bob',
    'bob.member@example.com',
    '$2b$10$9v4SzZa5B3lS7Q0bYnL/Hui5d6F1nX7ABY1zGxwU6k1PDfX3Qc5Ai',
    'MEMBER',
    NOW(),
    NOW()
  ),
  (
    uuid_generate_v4(),
    'member_charlie',
    'charlie.member@example.com',
    '$2b$10$8yV7PoT4Qk6GnB2vYfLiK.jr3z5sH8dM4N0WxEfT9bP3Er6sJy8uG',
    'MEMBER',
    NOW(),
    NOW()
  );
```

## Usage

```node
npm start
```

*open link on browser

*the documentation is on the left for reference

<img width="1926" height="961" alt="image" src="https://github.com/user-attachments/assets/857e779b-0659-4afd-a54c-4ac3b71a5279" />


*example usage:
```
mutation CreateUser {
  createUser(input: {username: "john", email: "johndoe@hello.com", password: "JohnDoe01@", role: MEMBER}) {
   code
   success
   message
   errors
   user {
     userId
     username
   }
  }
}
```
<img width="1278" height="430" alt="image" src="https://github.com/user-attachments/assets/29a5e620-2c99-4d9a-9724-1965c1e84394" />

```
mutation Login {
  login(input: {email: "johndoe@hello.com", password: "JohnDoe01@"}) {
    code
    success
    message
    errors
    accessToken
    refreshToken
  }
}
```
<img width="1279" height="477" alt="image" src="https://github.com/user-attachments/assets/1bbc187b-32dd-4422-b905-f360e2aa5fdd" />

```
query User {
  user(userId: "1be478f1-f842-40fa-8f0b-ad7ecfe5db3b") {
   email
   role
   userId
   username
   createdAt 
  }
}
```
<img width="1280" height="377" alt="image" src="https://github.com/user-attachments/assets/9998ffb0-b987-421d-8072-6399c8360302" />

```
query Users {
  users(role: MEMBER) {
    userId
    username
    email
    role
    createdAt
  }
}
```
<img width="1273" height="734" alt="image" src="https://github.com/user-attachments/assets/c8ffa731-ce0e-4455-93fb-fc6fc1ca3826" />
