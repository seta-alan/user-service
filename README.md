# User Service

A standalone GraphQL service to handle user operations.

## Installation

```node
npm install
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

