# 🎨 Bab 2: Frontend Development

Frontend adalah bagian yang **dilihat dan diinteraksi** oleh user.

## 2.1 HTML - Struktur

HTML adalah kerangka/tulang dari website.

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Website Saya</title>
  </head>
  <body>
    <header>
      <h1>Selamat Datang!</h1>
    </header>
    <main>
      <p>Ini adalah konten utama.</p>
    </main>
    <footer>
      <p>© 2026</p>
    </footer>
  </body>
</html>
```

**Yang harus dipelajari:**
- ✅ Semantic HTML (header, nav, main, footer)
- ✅ Forms & Input
- ✅ Tables & Lists
- ✅ Accessibility basics

---

## 2.2 CSS - Styling

CSS membuat website menjadi **cantik**.

```css
/* Modern CSS dengan Flexbox */
.container {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 1rem;
}

/* Responsive Design */
@media (max-width: 768px) {
  .container {
    flex-direction: column;
  }
}
```

**Yang harus dipelajari:**
- ✅ Box Model (margin, padding, border)
- ✅ Flexbox & Grid
- ✅ Responsive Design
- ✅ CSS Variables
- ✅ Tailwind CSS (recommended!)

---

## 2.3 JavaScript - Interaktivitas

JavaScript membuat website **hidup dan interaktif**.

```javascript
// Variabel & Tipe Data
const nama = "Budi";
let umur = 25;

// Function
function sapa(nama) {
  return `Halo, ${nama}!`;
}

// Array & Object
const users = [
  { id: 1, nama: "Andi" },
  { id: 2, nama: "Budi" }
];

// Modern JS: Arrow Function & Destructuring
const getUser = (id) => users.find(user => user.id === id);

// Async/Await (untuk API)
async function fetchData() {
  const response = await fetch('/api/users');
  const data = await response.json();
  return data;
}
```

**Yang harus dipelajari:**
- ✅ Variables (let, const)
- ✅ Functions & Arrow Functions
- ✅ Arrays & Objects
- ✅ DOM Manipulation
- ✅ Async/Await & Fetch API
- ✅ ES6+ Features

---

## 2.4 React.js - Framework Frontend

React adalah library untuk membuat UI yang **reusable**.

```jsx
// Komponen React dengan Hooks
import { useState } from 'react';

function Counter() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>
        Tambah
      </button>
    </div>
  );
}

export default Counter;
```

**Yang harus dipelajari:**
- ✅ Components & Props
- ✅ State & useState
- ✅ useEffect (side effects)
- ✅ Event Handling
- ✅ Conditional Rendering
- ✅ Lists & Keys

---

## 📊 Checklist Frontend

```
□ HTML Semantic
□ CSS Flexbox & Grid
□ CSS Responsive Design
□ Tailwind CSS
□ JavaScript ES6+
□ DOM Manipulation
□ React Basics
□ React Hooks
□ State Management
```

---

[← Kembali: Pendahuluan](./01-pendahuluan.md) | [⏭️ Lanjut: Backend Development →](./03-Backend.md)
