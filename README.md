# TaskFlow — MERN Management System

A full-stack task-management web application built with the **MERN** stack
(**M**ongoDB, **E**xpress, **R**eact, **N**ode). It simulates a real management
system with user accounts, role-based access, and full CRUD over tasks.

---

## What it does

- **Register / Login** with secure, hashed passwords (bcrypt + salt).
- **JWT authentication** — after logging in, the browser stores a token and
  sends it with every request.
- **Role-based authorization** — two roles:
  - `user`: can create, read, update and delete **their own** tasks.
  - `admin`: can see and manage **all** tasks and users.
  - `superadmin`: can see and manage **all** tasks and **all** users.
- **Task management (CRUD)**: create tasks, edit them, change their status
  (todo / in-progress / done), set priority and due dates, search and filter,
  and delete them.
- **Admin panel**: list every account and remove users.
- **Protected routes** on both the server (middleware) and the client (route
  guards).

---

## Tech stack

| Layer        | Technology                                             |
| ------------ | ------------------------------------------------------ |
| Frontend     | React 18 (Vite), React Router, Axios, Context API      |
| Backend      | Node.js, Express                                       |
| Database     | MongoDB + Mongoose (ODM)                               |
| Auth         | JSON Web Tokens (jsonwebtoken), bcryptjs (hashing/salt)|

---

## Project structure

```
mern-task-manager/
├── README.md                  ← you are here
├── .gitignore
│
├── server/                    ← Node + Express + MongoDB API
│   ├── server.js              ← app entry point (Express setup)
│   ├── package.json
│   ├── .env.example           ← copy to .env and fill in
│   ├── config/
│   │   └── db.js              ← MongoDB connection (Mongoose)
│   ├── models/                ← Mongoose schemas (clear data models)
│   │   ├── User.js            ← user + bcrypt password hashing
│   │   └── Task.js            ← task, references its owner
│   ├── controllers/           ← business logic
│   │   ├── authController.js  ← register / login / profile / admin
│   │   └── taskController.js  ← task CRUD
│   ├── routes/                ← URL → controller mapping
│   │   ├── authRoutes.js
│   │   └── taskRoutes.js
│   ├── middleware/
│   │   ├── authMiddleware.js  ← protect (JWT) + admin (role) guards
│   │   └── errorMiddleware.js ← central error & 404 handling
│   └── utils/
│       ├── generateToken.js   ← signs JWTs
│       └── seed.js            ← optional demo data
│
└── client/                    ← React (Vite) frontend
    ├── index.html
    ├── package.json
    ├── vite.config.js         ← dev server + API proxy
    ├── .env.example
    └── src/
        ├── main.jsx           ← mounts the app (Router + AuthProvider)
        ├── App.jsx            ← all routes (React Router)
        ├── index.css          ← design system / styling
        ├── api/
        │   └── axios.js       ← axios instance, attaches JWT
        ├── context/
        │   └── AuthContext.jsx← global auth state (hooks)
        ├── components/
        │   ├── Navbar.jsx
        │   ├── ProtectedRoute.jsx ← client-side route guard
        │   ├── TaskForm.jsx   ← create + edit form
        │   └── TaskItem.jsx
        └── pages/
            ├── Login.jsx
            ├── Register.jsx
            ├── Dashboard.jsx  ← the main CRUD screen
            ├── Admin.jsx      ← admin-only user list
            └── NotFound.jsx
```