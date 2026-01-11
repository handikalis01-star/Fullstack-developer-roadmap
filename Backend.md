# ⚙️ Bab 3: Backend Development

Backend adalah bagian yang **tidak terlihat** user, tapi sangat penting!

## 3.1 Node.js - JavaScript di Server

Node.js memungkinkan JavaScript berjalan di **server**.

```javascript
// Membaca file dengan Node.js
const fs = require('fs');

fs.readFile('data.txt', 'utf8', (err, data) => {
  if (err) throw err;
  console.log(data);
});
```

**Yang harus dipelajari:**
- ✅ Node.js basics
- ✅ NPM (Node Package Manager)
- ✅ Modules (import/export)
- ✅ File System
- ✅ Environment Variables

---

## 3.2 Express.js - Framework Backend

Express adalah framework untuk membuat **API** dengan mudah.

```javascript
const express = require('express');
const app = express();

app.use(express.json());

// Data dummy
let todos = [
  { id: 1, task: "Belajar Node.js", done: false }
];

// GET - Ambil semua todos
app.get('/api/todos', (req, res) => {
  res.json(todos);
});

// POST - Tambah todo baru
app.post('/api/todos', (req, res) => {
  const newTodo = {
    id: todos.length + 1,
    task: req.body.task,
    done: false
  };
  todos.push(newTodo);
  res.status(201).json(newTodo);
});

// PUT - Update todo
app.put('/api/todos/:id', (req, res) => {
  const todo = todos.find(t => t.id === parseInt(req.params.id));
  if (!todo) return res.status(404).json({ error: "Not found" });
  
  todo.task = req.body.task || todo.task;
  todo.done = req.body.done ?? todo.done;
  res.json(todo);
});

// DELETE - Hapus todo
app.delete('/api/todos/:id', (req, res) => {
  todos = todos.filter(t => t.id !== parseInt(req.params.id));
  res.status(204).send();
});

app.listen(3000, () => {
  console.log('Server running on port 3000');
});
```

---

## 3.3 REST API Concept

REST API adalah standar komunikasi antara Frontend & Backend.

```
┌──────────────┐         HTTP Request          ┌──────────────┐
│              │  ──────────────────────────▶  │              │
│   FRONTEND   │                               │   BACKEND    │
│   (React)    │  ◀──────────────────────────  │   (Node.js)  │
│              │         JSON Response         │              │
└──────────────┘                               └──────────────┘
```

**HTTP Methods:**

| Method | Fungsi              | Contoh              |
|--------|---------------------|---------------------|
| GET    | Ambil data          | GET /api/users      |
| POST   | Tambah data baru    | POST /api/users     |
| PUT    | Update data         | PUT /api/users/1    |
| DELETE | Hapus data          | DELETE /api/users/1 |

---

## 3.4 Next.js - Fullstack Framework

Next.js adalah framework yang menggabungkan **React + Backend**.

```javascript
// app/api/hello/route.js - API Route
export async function GET(request) {
  return Response.json({ message: "Hello from API!" });
}

export async function POST(request) {
  const body = await request.json();
  return Response.json({ received: body });
}
```

```jsx
// app/page.js - Server Component
async function getData() {
  const res = await fetch('https://api.example.com/data');
  return res.json();
}

export default async function Home() {
  const data = await getData();
  
  return (
    <main>
      <h1>Data dari Server</h1>
      <pre>{JSON.stringify(data, null, 2)}</pre>
    </main>
  );
}
```

**Keunggulan Next.js:**
- ✅ Server-Side Rendering (SEO friendly)
- ✅ API Routes (Backend dalam satu project)
- ✅ File-based Routing
- ✅ Optimized Performance

---

## 3.5 Authentication

```javascript
// Contoh sederhana JWT Authentication
const jwt = require('jsonwebtoken');
const bcrypt = require('bcrypt');

// Login endpoint
app.post('/api/login', async (req, res) => {
  const { email, password } = req.body;
  
  // Cari user di database
  const user = await findUserByEmail(email);
  if (!user) {
    return res.status(401).json({ error: "User not found" });
  }
  
  // Verify password
  const valid = await bcrypt.compare(password, user.password);
  if (!valid) {
    return res.status(401).json({ error: "Invalid password" });
  }
  
  // Generate token
  const token = jwt.sign(
    { userId: user.id },
    process.env.JWT_SECRET,
    { expiresIn: '7d' }
  );
  
  res.json({ token });
});

// Middleware untuk protect routes
function authMiddleware(req, res, next) {
  const token = req.headers.authorization?.split(' ')[1];
  
  if (!token) {
    return res.status(401).json({ error: "No token" });
  }
  
  try {
    const decoded = jwt.verify(token, process.env.JWT_SECRET);
    req.userId = decoded.userId;
    next();
  } catch (error) {
    res.status(401).json({ error: "Invalid token" });
  }
}
```

---

## 📊 Checklist Backend

```
□ Node.js Basics
□ NPM & Modules
□ Express.js
□ REST API (CRUD)
□ Middleware
□ Authentication (JWT)
□ Next.js API Routes
□ Error Handling
```

---

[← Kembali: Frontend](./02-frontend.md) | [⏭️ Lanjut: Database →](./04-database.md)
