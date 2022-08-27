## Dynamic API Server
An Express/Node.js based server designed to be a “model agnostic” REST API server, which can perform CRUD operations on any data model

## Business Requirements
We’re opening a online store! In order to support our web application, we need to create an API that will serve specific data (namely, categories and products) to our application. We will write an API to interface with our databases to provide category and product information to our front end app.

As it is highly likely that we will need more data types and sources in the future, it’s imperative that we build this API as a standardized means of working with any data model, using any persistence system, though a common interface. The API Server must operate as follows:

## Support all REST/HTTP methods
* GET: Retrieve record(s) from a data source
All
One (by id)
Some (by filtering)
* POST: Create a new record in a data source
* PUT: Update a single full record in a data source
* PATCH: Update part of a single record in a data source
* DELETE: Delete a record in a data source

GET Records (CRUD: READ)
GET MANY: http://amazingapi.com/api/v1/products or http://amazingapi.com/api/v1.products?category=electronics
```
  {
    count: 300,
    previous: null,
    next: http://amazingapi.com/api/v1/products?page=2
    results: [
      { name: 'camera', ... },
      { name: 'phone', ... },
      { name: 'tv', ... },
      ...
    ]
  }
  ```

  GET ONE: http://amazingapi.com/api/v1/products/12345
```
  {
    id: 12345,
    name: 'camera',
    manufacturer: 'Nikon',
    model: 'xx435',
    price: 99.99,
    inStock: 2200,
    weight: 1.1
  }
  ```
CREATE Records (CRUD: CREATE)
```
  {
    id: 12345,
    name: 'camera',
    manufacturer: 'Nikon',
    model: 'xx435',
    price: 99.99,
    inStock: 2200,
    weight: 1.1
  }
  ```

  Output
```
  {
    id: 12345,
    name: 'camera',
    manufacturer: 'Nikon',
    model: 'xx435',
    price: 99.99,
    inStock: 2200,
    weight: 1.1
  }
  ```

## Authentication Server / Module
An Express/Node.js based server using a custom “authentication” module that is designed to handle user registration and sign in using Basic, Bearer, or OAuth along with a custom “authorization” module that will grant/deny users access to the server based on their role or permissions level.

## Business Requirements
Our business is expanding! We have a real need to manage a list of users of many types, and control their access to our data accordingly. The system to be built will have the following core features:

1. Users can create an account, associated with a “role”
2. User Roles will be pre-defined and will each have a list of allowed capabilities
admin can read, create, update, delete
editor can read, create, update
writer can read, create
user can read

3. Users can then login with a valid username and password
4. Alternatively, users can login using an OAuth provider such as Google or GitHub
In this case, users should be automatically assigned the role of user
5. Once logged in, Users can then access any route on the server, so long as they are permitted by the capabilities that match their role.
For example, a route that deletes records should only work if your user role is “admin”

## Application Structure (proposed)
NOTE: The majority of our work for this server will be done within the src/auth folder. The rest of the system should be generic express. Why? It’s our intention to be able to “lift” the auth folder and “drop” it into any other server (such as our API server) and be able to use authorization to “protect” those CRUD routes. This makes our entire auth system very modular. Think of index.js and server.js as nothing more than the basics to get a server started, with 100% of the actual logic living within the auth module
```
├── .gitignore
├── .eslintrc.json
├── __tests__
│   ├── auth.router.test.js
│   ├── basic-auth.test.js
│   ├── bearer-auth.test.js
│   ├── 500.test.js
│   ├── model-finder.test.js
│   ├── mongo.js
├── src
│   ├── auth
│   │   ├── router.js
│   │   ├── middleware
│   │   │   ├── basic.js
│   │   │   ├── bearer.js
│   │   │   ├── oauth.js
│   │   ├── models
│   │   │   ├── users-model.js
│   ├── middleware
│   │   ├── 404.js
│   │   ├── 500.js
│   │   ├── model-finder.js
│   ├── server.js
├── index.js
└── package.json
```

## I/O Examples
Signup
The signup process will require a POST request to the /signup route.

This route should accept a request body in either JSON or form/urlencoded formats.
POST http://yourauthserver.com/signup
```
  {
    "username":"awesomecoder",
    "password":"youcantguessthis33!",
    "fullname":"Awesome Coder",
    "email":"awesome@coders.com"
  }
  ```

## HTTP Headers:
```
Set-Cookie: auth=ENCRYPTED.JWT.TOKEN; Path=/
token:ENCRYPTED.JWT.TOKEN
Content-Type: application/json
```

## BODY:
```
{
    "token": "ENCRYPTED.JWT.TOKEN",
    "user": {
        "__v": 0,
        "_id": "5ec44dcde458f14f77b3d8c6",
        "acl": [],
        "password": "$2b$10$Bw5tNNSUACEEHW94CaRItuLsoz/nomUMh4eLTD/T23Ks0mCtUp3Iq",
        "role": "user",
        "username": "awesomecoder"
    }
}
```