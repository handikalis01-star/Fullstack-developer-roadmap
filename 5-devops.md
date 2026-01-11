# 🚀 Bab 5: DevOps & Deployment

Setelah aplikasi selesai, saatnya **deploy ke internet**!

## 5.1 Version Control - Git

Git adalah alat untuk **melacak perubahan kode**.

```bash
# Perintah dasar Git
git init                    # Inisialisasi repo baru
git clone <url>             # Clone repo dari remote
git status                  # Lihat status file
git add .                   # Stage semua perubahan
git commit -m "pesan"       # Commit dengan pesan
git push origin main        # Push ke remote
git pull origin main        # Pull dari remote

# Branching
git branch feature-login    # Buat branch baru
git checkout feature-login  # Pindah ke branch
git checkout -b feature-x   # Buat dan pindah sekaligus
git merge feature-login     # Merge branch ke current

# Melihat history
git log --oneline           # Lihat history singkat
```

**Git Workflow:**

```
┌──────────┐     ┌──────────┐     ┌──────────┐     ┌──────────┐
│ Working  │────▶│ Staging  │────▶│  Local   │────▶│  Remote  │
│Directory │     │  Area    │     │  Repo    │     │  (GitHub)│
└──────────┘     └──────────┘     └──────────┘     └──────────┘
              git add         git commit       git push
```

---

## 5.2 GitHub

GitHub adalah platform untuk **menyimpan dan kolaborasi kode**.

```bash
# Setup awal
git config --global user.name "Nama Kamu"
git config --global user.email "email@kamu.com"

# Hubungkan repo lokal ke GitHub
git remote add origin https://github.com/username/repo.git
git branch -M main
git push -u origin main
```

**Struktur Repository yang Baik:**

```
my-project/
├── .github/
│   └── workflows/          # GitHub Actions
├── src/                    # Source code
├── tests/                  # Unit tests
├── docs/                   # Dokumentasi
├── .env.example            # Contoh env variables
├── .gitignore              # File yang diabaikan
├── README.md               # Dokumentasi utama
├── package.json            # Dependencies
└── LICENSE                 # Lisensi
```

---

## 5.3 Deployment Platforms

### Vercel (Recommended untuk Next.js)

```bash
# Install Vercel CLI
npm i -g vercel

# Deploy
vercel

# Deploy production
vercel --prod
```

**Atau langsung dari GitHub:**
1. Push ke GitHub
2. Buka vercel.com
3. Import repository
4. Klik Deploy ✨

### Environment Variables

```bash
# .env.local (JANGAN di-push ke GitHub!)
DATABASE_URL=postgresql://...
JWT_SECRET=rahasia-super-aman
NEXT_PUBLIC_API_URL=https://api.example.com
```

```bash
# .gitignore
.env
.env.local
.env.production
node_modules/
.next/
```

---

## 5.4 CI/CD dengan GitHub Actions

Otomatis test dan deploy setiap push.

```yaml
# .github/workflows/deploy.yml
name: Deploy

on:
  push:
    branches: [main]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      
      - name: Setup Node.js
        uses: actions/setup-node@v4
        with:
          node-version: '20'
          
      - name: Install dependencies
        run: npm ci
        
      - name: Run tests
        run: npm test
        
      - name: Build
        run: npm run build
```

---

## 5.5 Domain & DNS

```
┌─────────────┐      ┌─────────────┐      ┌─────────────┐
│   Browser   │─────▶│     DNS     │─────▶│   Server    │
│ example.com │      │  Resolver   │      │ 123.45.67.89│
└─────────────┘      └─────────────┘      └─────────────┘
```

**DNS Records:**
| Type  | Fungsi                    | Contoh                |
|-------|---------------------------|-----------------------|
| A     | Domain → IP               | example.com → 1.2.3.4 |
| CNAME | Domain → Domain lain      | www → example.com     |
| TXT   | Verifikasi kepemilikan    | verify=abc123         |

---

## 5.6 Monitoring & Logging

```javascript
// Logging sederhana
console.log('[INFO]', 'Server started');
console.error('[ERROR]', 'Database connection failed');
console.warn('[WARN]', 'Memory usage high');

// Dengan timestamp
function log(level, message) {
  const timestamp = new Date().toISOString();
  console.log(`[${timestamp}] [${level}] ${message}`);
}

log('INFO', 'User logged in');
```

**Tools populer:**
- 📊 **Vercel Analytics** - Traffic & performance
- 🐛 **Sentry** - Error tracking
- 📈 **LogRocket** - Session replay

---

## 📊 Checklist DevOps

```
□ Git basics (add, commit, push, pull)
□ Git branching
□ GitHub repository
□ README.md yang baik
□ .gitignore
□ Environment variables
□ Vercel deployment
□ Custom domain
□ CI/CD basics
```

---

[← Kembali: Database](./04-database.md) | [⏭️ Lanjut: Tips & Resources →](./06-tips-resources.md)
