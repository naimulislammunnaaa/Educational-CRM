# Spark CRM - Quick Start (5 minutes)

## ⚡ Fast Track Setup

### 1️⃣ Install Node.js & PostgreSQL
```bash
# macOS (using Homebrew)
brew install node postgresql

# Verify
node -v    # v18+
npm -v     # 9+
psql -v    # 15+
```

### 2️⃣ Create Database
```bash
brew services start postgresql

psql -U postgres << EOF
CREATE DATABASE spark_crm;
\q
EOF
```

### 3️⃣ Navigate to Project
```bash
cd /Users/jewelrashedsarker/Munna/Project/CRM
```

### 4️⃣ Update Environment
Edit `.env.local`:
```
DATABASE_URL="postgresql://postgres:YOUR_PASSWORD@localhost:5432/spark_crm"
```
*Replace `YOUR_PASSWORD` with your PostgreSQL password*

### 5️⃣ Install & Setup
```bash
npm install                 # ~2-5 min
npm run db:push            # Push schema
npm run db:seed            # Add sample data
```

### 6️⃣ Start Server
```bash
npm run dev
```

### 7️⃣ View in Browser
Open: **http://localhost:3000**

---

## 🔑 Default Login Credentials

| Email | Password |
|-------|----------|
| `ceo@spark-crm.com` | `demo123` |
| `consultant1@spark-crm.com` | `demo123` |
| `munna@spark-crm.com` | `demo123` |

---

## 📊 View Database (Optional)

```bash
npm run db:studio
```

Opens interactive GUI at: http://localhost:5555

---

## ✅ Status Codes

| What | Expected | Command |
|------|----------|---------|
| Server running? | `http://localhost:3000` | `npm run dev` |
| Database connected? | No errors | Check `.env.local` |
| Tables created? | 15 tables | `npm run db:studio` |
| Data seeded? | 6 users, 2 universities | `npm run db:studio` |

---

## 🆘 If Something Goes Wrong

```bash
# Check database connection
psql -U postgres -d spark_crm -c "\dt"

# Reset database
npm run db:push -- --force

# Reseed data
npm run db:seed

# Check for errors
npm run type-check

# Fresh install
rm -rf node_modules package-lock.json
npm install
npm run db:push
npm run db:seed
npm run dev
```

---

## 📁 Project Structure

```
CRM/
├── app/                    # Next.js app
├── components/             # React components
├── lib/                   # Utilities
├── types/                 # TypeScript types
├── prisma/                # Database schema
├── ROADMAP.md             # Implementation plan
├── DATABASE_SETUP.md      # Database guide
├── GETTING_STARTED.md     # Full setup guide
└── QUICK_START.md         # This file
```

---

## 🚀 What's Next?

1. ✅ See homepage at http://localhost:3000
2. ✅ View database at http://localhost:5555 (optional)
3. 🔜 Follow ROADMAP.md for Step 4 onwards

---

**Done! Your CRM is running.** 🎉
