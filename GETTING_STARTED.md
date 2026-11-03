# Getting Started with Spark CRM

Complete guide to set up and run the CRM application on your local machine.

## ⚙️ Prerequisites

Before starting, make sure you have installed:

1. **Node.js 18+** - Download from https://nodejs.org/
   ```bash
   node --version  # Should show v18 or higher
   npm --version   # Should show 9 or higher
   ```

2. **PostgreSQL 15+** - Download from https://www.postgresql.org/download/
   ```bash
   psql --version  # Should show PostgreSQL 15+
   ```

3. **Git** (optional) - For version control
   ```bash
   git --version
   ```

---

## 🚀 Setup Instructions

### Step 1: Navigate to Project Directory

```bash
cd /Users/jewelrashedsarker/Munna/Project/CRM
```

### Step 2: Create PostgreSQL Database

**On macOS/Linux:**
```bash
# Start PostgreSQL service
brew services start postgresql

# Open PostgreSQL CLI
psql -U postgres

# Inside PostgreSQL CLI, run:
CREATE DATABASE spark_crm;
\l   # List databases to verify
\q   # Exit
```

**On Windows:**
- Open "pgAdmin" (installed with PostgreSQL)
- Right-click "Databases" → "Create" → "Database"
- Name: `spark_crm`
- Click "Save"

### Step 3: Install Dependencies

```bash
npm install
```

This installs:
- Next.js 14
- React 18
- Prisma ORM
- Tailwind CSS
- And all other dependencies

**Time**: ~2-5 minutes depending on internet speed

### Step 4: Configure Environment

Edit `.env.local` in your project root:

```bash
# Database Connection
DATABASE_URL="postgresql://postgres:YOUR_PASSWORD@localhost:5432/spark_crm"

# Replace YOUR_PASSWORD with your PostgreSQL password
```

**Example** (if your PostgreSQL password is "password123"):
```
DATABASE_URL="postgresql://postgres:password123@localhost:5432/spark_crm"
```

### Step 5: Set Up Database Schema

```bash
# Push Prisma schema to database
npm run db:push

# This creates all tables defined in prisma/schema.prisma
```

**Expected output:**
```
✓ Database successfully created
✓ Prisma schema pushed to database
```

### Step 6: Seed Sample Data

```bash
# Populate database with default users and sample data
npm run db:seed
```

**Creates these default users:**
- CEO: `ceo@spark-crm.com` | Password: `demo123`
- Co-Founder: `cofounder@spark-crm.com` | Password: `demo123`
- Director: `director@spark-crm.com` | Password: `demo123`
- Finance Manager: `munna@spark-crm.com` | Password: `demo123`
- Consultant 1: `consultant1@spark-crm.com` | Password: `demo123`
- Consultant 2: `consultant2@spark-crm.com` | Password: `demo123`

### Step 7: Start Development Server

```bash
npm run dev
```

**Expected output:**
```
> spark-education-crm@1.0.0 dev
> next dev

  ▲ Next.js 14.0.4
  - Local:        http://localhost:3000
```

### Step 8: Open in Browser

Visit: **http://localhost:3000**

---

## 🎨 What You'll See

### Home Page
- "Spark Education CRM" title
- Login and Register buttons
- Project setup status

### Current Features
- ✅ Landing page
- ✅ Database connected
- ✅ Type safety with TypeScript
- ✅ Styling with Tailwind CSS

### Coming Next
- 🔜 Login/Authentication page (Step 4)
- 🔜 Dashboard (Step 7)
- 🔜 Lead management (Step 8)
- 🔜 Student profiles (Step 10)
- 🔜 And much more...

---

## 📊 View Database (Prisma Studio)

To visually explore and manage your database:

```bash
npm run db:studio
```

This opens Prisma Studio at: http://localhost:5555

You can:
- ✅ View all database tables
- ✅ Create/Edit/Delete records
- ✅ Explore relationships
- ✅ Test data structure

---

## 🛑 Stop the Server

Press `Ctrl + C` in the terminal

---

## 🔧 Useful Commands

```bash
# Development
npm run dev              # Start dev server

# Database
npm run db:push         # Update database schema
npm run db:migrate      # Create a migration
npm run db:studio       # Open Prisma Studio (GUI)
npm run db:seed         # Populate sample data

# Code Quality
npm run type-check      # Check TypeScript errors
npm run lint            # Run ESLint
npm run build           # Build for production

# Cleanup
npm run clean           # Remove build files
```

---

## 🐛 Troubleshooting

### Error: "Could not find postgresql"
**Solution**: 
- Ensure PostgreSQL is installed
- On macOS: `brew install postgresql`
- Restart terminal after installation

### Error: "Connection refused on port 5432"
**Solution**:
- PostgreSQL service isn't running
- macOS: `brew services start postgresql`
- Windows: Start "PostgreSQL" from Services
- Linux: `sudo systemctl start postgresql`

### Error: "Database does not exist"
**Solution**:
```bash
psql -U postgres -c "CREATE DATABASE spark_crm;"
```

### Error: "password authentication failed"
**Solution**:
- Check PostgreSQL password in `.env.local`
- Default password might be empty (try just `postgres:@localhost`)
- Or reset PostgreSQL password if needed

### Error: "Port 3000 already in use"
**Solution**:
```bash
# Use different port
npm run dev -- -p 3001

# Or kill process on 3000
# macOS/Linux:
lsof -i :3000 | grep LISTEN | awk '{print $2}' | xargs kill -9

# Windows:
netstat -ano | findstr :3000
taskkill /PID <PID> /F
```

### Error: "Module not found"
**Solution**:
```bash
# Reinstall dependencies
rm -rf node_modules package-lock.json
npm install
```

---

## 📱 Development Tips

### Hot Reload
- Changes to `.tsx` and `.ts` files auto-reload
- Browser automatically refreshes
- No need to restart server

### TypeScript Errors
Check with:
```bash
npm run type-check
```

### Browser DevTools
Press `F12` or `Cmd+Option+I` to open DevTools
- Console tab for errors
- Network tab to see API calls
- Application tab to view local storage

### Database Debugging
```bash
npm run db:studio

# View all data in real-time
# Create test records
# Verify migrations worked
```

---

## 📚 Next Steps After Starting

1. **See the home page** - Visit http://localhost:3000
2. **Explore database** - Run `npm run db:studio`
3. **Check structure** - Look at `prisma/schema.prisma`
4. **Continue building** - Follow ROADMAP.md for next steps

---

## ✅ Success Checklist

After following these steps, you should have:

- [x] Node.js and npm installed
- [x] PostgreSQL installed and running
- [x] Project dependencies installed (`npm install`)
- [x] PostgreSQL database created (`spark_crm`)
- [x] `.env.local` configured with correct password
- [x] Database schema pushed (`npm run db:push`)
- [x] Sample data seeded (`npm run db:seed`)
- [x] Development server running (`npm run dev`)
- [x] Home page loads at http://localhost:3000
- [x] Prisma Studio accessible at http://localhost:5555 (optional)

---

## 🆘 Need Help?

1. Check **DATABASE_SETUP.md** for database-specific issues
2. Check **ROADMAP.md** for project structure
3. Review error messages in terminal carefully
4. Try stopping/restarting the development server
5. Delete `.next` folder and `node_modules` if issues persist:
   ```bash
   rm -rf .next node_modules
   npm install
   npm run dev
   ```

---

## 🎉 You're Ready!

Your Spark CRM is now running locally. Continue with the implementation roadmap to build more features!
