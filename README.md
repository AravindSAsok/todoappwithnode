# Todo App API

<p align="center"><strong>A small Express and MongoDB API for authenticated, user-scoped todo lists.</strong></p>

<p align="center">
  <img alt="Node.js" src="https://img.shields.io/badge/Node.js-ESM-339933?logo=node.js&logoColor=white" />
  <img alt="Express" src="https://img.shields.io/badge/Express-4-000000?logo=express&logoColor=white" />
  <img alt="MongoDB" src="https://img.shields.io/badge/MongoDB-Mongoose-47A248?logo=mongodb&logoColor=white" />
  <img alt="Authentication" src="https://img.shields.io/badge/Auth-JWT%20%2B%20bcrypt-6C47FF" />
</p>

This repository contains the API for a simple todo application. It uses Express for HTTP routes, MongoDB through Mongoose for persistence, bcrypt for password hashing, and JWT cookies for session identity. Todo records are associated with the authenticated user's database ID.

## Features

- Register users with a bcrypt password hash.
- Sign in and issue a JWT in a cookie.
- Read the current user from the session cookie.
- Sign out by clearing the session cookie.
- List the current user's todos.
- Create a todo for the current user.
- Update a todo's completion state while scoping the update to its owner.

## Technology

| Layer | Technology |
| --- | --- |
| Runtime | Node.js with ES modules |
| HTTP API | Express 4 |
| Database | MongoDB |
| ODM | Mongoose 5 |
| Password hashing | bcrypt |
| Session token | jsonwebtoken |
| Middleware | body-parser, cookie-parser, cors |

## API routes

| Method | Path | Description |
| --- | --- | --- |
| GET | / | Basic service response |
| POST | /register | Create an account |
| POST | /login | Authenticate and set the JWT cookie |
| GET | /user | Return the current user when authenticated |
| POST | /logout | Clear the JWT cookie |
| GET | /todos | List todos belonging to the current user |
| PUT | /todos | Create a todo for the current user |
| POST | /todos | Update a todo's done state |

Authenticated routes expect the JWT cookie set by the login or registration endpoint.

## Run locally

### Requirements

- Node.js 20 or later
- MongoDB running locally or a MongoDB connection string
- npm

### Install

~~~bash
git clone https://github.com/AravindSAsok/todoappwithnode.git
cd todoappwithnode/api
npm install
~~~

Create a local environment file from the template:

~~~bash
cp .env.example .env
~~~

Set MONGODB_URI to your own MongoDB database and JWT_SECRET to a long, random value. CLIENT_ORIGIN should match the frontend origin.

Node.js can load the local environment file directly:

~~~bash
node --env-file=.env index.js
~~~

The API listens on PORT (default 4000).

## Security status and limitations

This is an older learning project, not a production-ready authentication service. The repository previously contained hard-coded database and JWT credentials; the current source now reads MONGODB_URI and JWT_SECRET from the environment. **Rotate any credentials that were ever committed.** Removing a secret from the latest file does not remove it from Git history or revoke it at the provider.

Before production use, this API needs additional security work, including secure cookie settings (HttpOnly, Secure, SameSite), JWT expiry and revocation strategy, input validation, rate limiting, robust error handling, CORS allowlist review, and CSRF protections appropriate to the frontend's cookie-based authentication. The current routes should not be exposed publicly until those controls are implemented and tested.

## Project structure

~~~text
todoappwithnode/
└── api/
    ├── index.js
    ├── .env.example
    ├── models/
    │   ├── Todo.js
    │   └── User.js
    ├── package.json
    └── package-lock.json
~~~

## Maintainer

Built by **Aravind S Asok** · [GitHub](https://github.com/AravindSAsok) · [Portfolio](https://aravindsasok.netlify.app/)
