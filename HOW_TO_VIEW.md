# How to View Your Spark CRM

## 🎯 Quick Answer: 7 Simple Steps

### Step 1: Open Terminal
Open your terminal/command prompt

### Step 2: Navigate to Project
```bash
cd /Users/jewelrashedsarker/Munna/Project/CRM
```

### Step 3: Ensure PostgreSQL is Running
```bash
# macOS
brew services start postgresql

# Windows - Use Services app or:
# pg_ctl -D "C:\Program Files\PostgreSQL\15\data" start

# Linux
sudo systemctl start postgresql
```

### Step 4: Create Database (First Time Only)
```bash
psql -U postgres -c "CREATE DATABASE spark_crm;"
```

### Step 5: Update Connection String
Edit `.env.local` file and set:
```
DATABASE_URL="postgresql://postgres:YOUR_PASSWORD@localhost:5432/spark_crm"
```
Replace `YOUR_PASSWORD` with your PostgreSQL password

### Step 6: Setup & Start
```bash
npm install              # Install all dependencies (first time only)
npm run db:push        # Create database tables
npm run db:seed        # Add sample data
npm run dev            # Start development server
```

### Step 7: Open in Browser
Visit: **http://localhost:3000**

---

## 🖥️ What You'll See

### Initial Page (Now)
```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
            Spark Education CRM
  Complete CRM for Educational Agency
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

      [Login Button]    [Register Button]

✓ Project Setup Complete
✓ Next.js 14 + TypeScript
✓ Tailwind CSS Configured
```

### After Implementation (Step 4 onwards)
- Login page with email/password
- Dashboard with KPIs
- Lead management interface
- Student profiles
- Applications tracking
- Finance management
- Reports and analytics
- Team management
- And more...

---

## 📊 View Your Database

### Option 1: Prisma Studio (Easiest)
```bash
npm run db:studio
```
Opens interactive GUI at: **http://localhost:5555**

You can:
- ✅ See all 15 tables
- ✅ View data records
- ✅ Create/Edit/Delete records
- ✅ Test database structure

### Option 2: PostgreSQL CLI
```bash
psql -U postgres -d spark_crm

# View tables
\dt

# View users
SELECT * FROM "User";

# Exit
\q
```

---

## ⏱️ Timing

| Task | Time |
|------|------|
| npm install | 2-5 minutes |
| npm run db:push | 30 seconds |
| npm run db:seed | 10 seconds |
| npm run dev | 5 seconds |
| **Total** | **~3-6 minutes** |

---

## ✅ Success Indicators

After running `npm run dev`, you should see:

```
> next dev

  ▲ Next.js 14.0.4
  - Local:        http://localhost:3000
  - Environments: .env.local

 ✓ Ready in 1.2s
```

Then in browser at http://localhost:3000:
- ✅ "Spark Education CRM" title visible
- ✅ Login and Register buttons visible
- ✅ Gradient background working
- ✅ No console errors

---

## 🔑 Sample Login Credentials

After seeding, login with any of these:

```
Email:    ceo@spark-crm.com
Password: demo123

Email:    consultant1@spark-crm.com
Password: demo123

Email:    munna@spark-crm.com (Finance Manager)
Password: demo123
```

*Note: Login functionality will be available after Step 4 implementation*

---

## 📱 On Different Devices

### Same Computer
- Main: http://localhost:3000
- Database: http://localhost:5555

### Other Computer on Same Network
```
Replace localhost with your computer's IP:
http://192.168.1.XXX:3000

Find your IP:
# macOS/Linux
ifconfig | grep "inet "

# Windows
ipconfig | findstr "IPv4"
```

---

## 🛑 Stopping the Server

Press `Ctrl + C` in the terminal

The server stops gracefully:
```
^C
[TERMINATING]
```

---

## 🔄 Restarting

```bash
npm run dev
```

---

## 📁 Project Files Location

All files are in:
```
/Users/jewelrashedsarker/Munna/Project/CRM/
```

Important files:
- `ROADMAP.md` - Implementation plan
- `QUICK_START.md` - Fast reference
- `GETTING_STARTED.md` - Detailed guide
- `DATABASE_SETUP.md` - Database guide
- `.env.local` - Configuration
- `prisma/schema.prisma` - Database structure

---

## 🐛 Common Issues & Fixes

### "Port 3000 already in use"
```bash
# Use different port
npm run dev -- -p 3001
```

### "Cannot connect to database"
```bash
# Check PostgreSQL is running
brew services start postgresql

# Check .env.local has correct password
cat .env.local

# Test connection
psql -U postgres
```

### "Module not found" error
```bash
npm install
npm run dev
```

### "Tables don't exist"
```bash
npm run db:push
npm run db:seed
```

---

## 🎓 Learning Resources

While CRM is running:

1. **Check TypeScript types**: `lib/types/index.ts` - Understand data structure
2. **View components**: `components/ui/` - See reusable components
3. **Check utilities**: `lib/utils/` - Understand helper functions
4. **Permission system**: `lib/permissions.ts` - How access control works
5. **Database schema**: `prisma/schema.prisma` - Understand 15 tables

---

## 🚀 What's Working Now

✅ Frontend framework (Next.js + React)  
✅ Type safety (TypeScript)  
✅ Database connected (PostgreSQL)  
✅ Sample data seeded  
✅ UI foundation (Tailwind CSS)  
✅ Type definitions  
✅ Utility functions  
✅ Permission system  
✅ Component structure  

## 🔜 What's Next

🔜 Authentication (Step 4)  
🔜 Dashboard (Step 7)  
🔜 Lead Management (Step 8)  
🔜 Student Profiles (Step 10)  
🔜 Finance Module (Step 13)  
🔜 Reports (Step 16)  

---

## 📞 Support

Refer to:
- **GETTING_STARTED.md** - Detailed setup
- **DATABASE_SETUP.md** - Database issues
- **ROADMAP.md** - What's planned
- **TASKS.md** - Custom tasks

---

## ✨ You're Ready!

Your Spark CRM is set up and ready to view. Follow the 7 steps above to see it running! 🎉
