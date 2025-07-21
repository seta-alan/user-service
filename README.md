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

-- seed sample users
-- password is "JohnDoe01@" (for all sample users)
INSERT INTO "Users"
  ("userId",                           "username",         "email",                           "password",                                                               "role",     "createdAt",           "updatedAt")
VALUES
  -- Managers
  ('a3f47e1b-4d2c-4e5f-9a11-1a2b3c4d5e6f', 'manager_olivia',  'olivia.manager@example.com',     '$2b$10$f.2V43IZDKoq3YtB2fu4IOhK762U0BVydmntsnvOMlrJeygLpzZuW', 'MANAGER', NOW(), NOW()),
  ('b1d2c3e4-5f6a-7b8c-9d01-2e3f4g5h6i7j', 'manager_lucas',   'lucas.manager@example.com',      '$2b$10$f.2V43IZDKoq3YtB2fu4IOhK762U0BVydmntsnvOMlrJeygLpzZuW', 'MANAGER', NOW(), NOW()),
  ('k1l2m3n4-5o6p-7q8r-9s01-2t3u4v5w6x7y', 'manager_emily',   'emily.manager@example.com',      '$2b$10$f.2V43IZDKoq3YtB2fu4IOhK762U0BVydmntsnvOMlrJeygLpzZuW', 'MANAGER', NOW(), NOW()),
  ('n5o6p7q8-9r0s-1t2u-3v4w-5x6y7z8a9b0c', 'manager_james',   'james.manager@example.com',      '$2b$10$f.2V43IZDKoq3YtB2fu4IOhK762U0BVydmntsnvOMlrJeygLpzZuW', 'MANAGER', NOW(), NOW()),

  -- Members
  ('c9e8d7f6-5a4b-3c2d-1e0f-9a8b7c6d5e4f', 'member_emma',     'emma.member@example.com',        '$2b$10$f.2V43IZDKoq3YtB2fu4IOhK762U0BVydmntsnvOMlrJeygLpzZuW', 'MEMBER',  NOW(), NOW()),
  ('d0e1f2a3-4b5c-6d7e-8f9a-0b1c2d3e4f5g', 'member_noah',     'noah.member@example.com',        '$2b$10$f.2V43IZDKoq3YtB2fu4IOhK762U0BVydmntsnvOMlrJeygLpzZuW', 'MEMBER',  NOW(), NOW()),
  ('e2f3a4b5-6c7d-8e9f-0a1b-2c3d4e5f6g7h', 'member_ava',      'ava.member@example.com',         '$2b$10$f.2V43IZDKoq3YtB2fu4IOhK762U0BVydmntsnvOMlrJeygLpzZuW', 'MEMBER',  NOW(), NOW()),
  ('f1a2b3c4-5d6e-7f8a-9b0c-1d2e3f4g5h6i', 'member_liam',     'liam.member@example.com',        '$2b$10$f.2V43IZDKoq3YtB2fu4IOhK762U0BVydmntsnvOMlrJeygLpzZuW', 'MEMBER',  NOW(), NOW()),
  ('g3h4i5j6-7k8l-9m0n-1o2p-3q4r5s6t7u8v', 'member_sophia',   'sophia.member@example.com',      '$2b$10$f.2V43IZDKoq3YtB2fu4IOhK762U0BVydmntsnvOMlrJeygLpzZuW', 'MEMBER',  NOW(), NOW()),
  ('h5i6j7k8-9l0m-1n2o-3p4q-5r6s7t8u9v0w', 'member_mason',    'mason.member@example.com',       '$2b$10$f.2V43IZDKoq3YtB2fu4IOhK762U0BVydmntsnvOMlrJeygLpzZuW', 'MEMBER',  NOW(), NOW());
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
