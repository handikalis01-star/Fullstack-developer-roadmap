# 🗄️ Bab 4: Database

Database adalah tempat **menyimpan data** secara permanen.

## 4.1 Jenis Database

```
┌─────────────────────────────────────────────────────────────┐
│                       DATABASE                               │
├─────────────────────────────┬───────────────────────────────┤
│           SQL               │            NoSQL              │
│    (Structured Query)       │      (Non-Structured)         │
├─────────────────────────────┼───────────────────────────────┤
│  - PostgreSQL               │  - MongoDB                    │
│  - MySQL                    │  - Firebase                   │
│  - SQLite                   │  - Redis                      │
├─────────────────────────────┼───────────────────────────────┤
│  Cocok untuk:               │  Cocok untuk:                 │
│  - Data terstruktur         │  - Data fleksibel             │
│  - Relasi kompleks          │  - Skala besar                │
│  - Transaksi penting        │  - Real-time apps             │
└─────────────────────────────┴───────────────────────────────┘
```

---

## 4.2 PostgreSQL (SQL)

PostgreSQL adalah database relasional yang **powerful dan gratis**.

```sql
-- Membuat tabel users
CREATE TABLE users (
  id SERIAL PRIMARY KEY,
  name VARCHAR(100) NOT NULL,
  email VARCHAR(255) UNIQUE NOT NULL,
  created_at TIMESTAMP DEFAULT NOW()
);

-- Membuat tabel posts (relasi dengan users)
CREATE TABLE posts (
  id SERIAL PRIMARY KEY,
  title VARCHAR(255) NOT NULL,
  content TEXT,
  user_id INTEGER REFERENCES users(id),
  created_at TIMESTAMP DEFAULT NOW()
);

-- INSERT data
INSERT INTO users (name, email) 
VALUES ('Budi', 'budi@email.com');

-- SELECT dengan JOIN
SELECT 
  posts.title,
  posts.content,
  users.name as author
FROM posts
JOIN users ON posts.user_id = users.id;

-- UPDATE
UPDATE users SET name = 'Budi Updated' WHERE id = 1;

-- DELETE
DELETE FROM users WHERE id = 1;
```

---

## 4.3 Menggunakan Database di Node.js

### Dengan Query Langsung (Neon/Supabase)

```javascript
import { neon } from '@neondatabase/serverless';

const sql = neon(process.env.DATABASE_URL);

// GET all users
async function getUsers() {
  const users = await sql`SELECT * FROM users`;
  return users;
}

// GET user by id
async function getUserById(id) {
  const [user] = await sql`
    SELECT * FROM users WHERE id = ${id}
  `;
  return user;
}

// CREATE user
async function createUser(name, email) {
  const [user] = await sql`
    INSERT INTO users (name, email)
    VALUES (${name}, ${email})
    RETURNING *
  `;
  return user;
}

// UPDATE user
async function updateUser(id, name) {
  const [user] = await sql`
    UPDATE users 
    SET name = ${name}
    WHERE id = ${id}
    RETURNING *
  `;
  return user;
}

// DELETE user
async function deleteUser(id) {
  await sql`DELETE FROM users WHERE id = ${id}`;
}
```

---

## 4.4 Supabase - Backend as a Service

Supabase menyediakan database + authentication **siap pakai**.

```javascript
import { createClient } from '@supabase/supabase-js';

const supabase = createClient(
  process.env.NEXT_PUBLIC_SUPABASE_URL,
  process.env.NEXT_PUBLIC_SUPABASE_ANON_KEY
);

// SELECT
const { data: users } = await supabase
  .from('users')
  .select('*');

// SELECT dengan filter
const { data: user } = await supabase
  .from('users')
  .select('*')
  .eq('id', 1)
  .single();

// INSERT
const { data: newUser } = await supabase
  .from('users')
  .insert({ name: 'Budi', email: 'budi@email.com' })
  .select()
  .single();

// UPDATE
const { data: updatedUser } = await supabase
  .from('users')
  .update({ name: 'Budi Updated' })
  .eq('id', 1)
  .select()
  .single();

// DELETE
await supabase
  .from('users')
  .delete()
  .eq('id', 1);
```

---

## 4.5 MongoDB (NoSQL)

MongoDB menyimpan data dalam format **JSON-like (BSON)**.

```javascript
import { MongoClient } from 'mongodb';

const client = new MongoClient(process.env.MONGODB_URI);
const db = client.db('myapp');
const users = db.collection('users');

// INSERT
await users.insertOne({
  name: 'Budi',
  email: 'budi@email.com',
  hobbies: ['coding', 'gaming'],
  address: {
    city: 'Jakarta',
    country: 'Indonesia'
  }
});

// FIND
const allUsers = await users.find({}).toArray();
const user = await users.findOne({ email: 'budi@email.com' });

// UPDATE
await users.updateOne(
  { email: 'budi@email.com' },
  { $set: { name: 'Budi Updated' } }
);

// DELETE
await users.deleteOne({ email: 'budi@email.com' });
```

---

## 4.6 Perbandingan

| Fitur          | PostgreSQL      | MongoDB          | Supabase        |
|----------------|-----------------|------------------|-----------------|
| Tipe           | SQL             | NoSQL            | SQL + BaaS      |
| Struktur       | Fixed Schema    | Flexible Schema  | Fixed Schema    |
| Relasi         | ✅ Strong       | ⚠️ Limited       | ✅ Strong       |
| Skalabilitas   | Vertikal        | Horizontal       | Managed         |
| Cocok untuk    | Enterprise      | Startup/Agile    | Rapid Dev       |

---

## 📊 Checklist Database

```
□ SQL Basics (SELECT, INSERT, UPDATE, DELETE)
□ Table Relations (JOIN)
□ PostgreSQL / MySQL
□ MongoDB basics
□ Supabase / Firebase
□ Database security
□ Indexing & Performance
```

---

[← Kembali: Backend](./03-backend.md) | [⏭️ Lanjut: DevOps →](./05-devops.md)
