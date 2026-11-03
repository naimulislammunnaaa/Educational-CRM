# Database Setup Guide for Spark CRM

## Prerequisites

- PostgreSQL 15+ installed
- Node.js 18+ installed
- npm or yarn package manager

## Step 1: Install PostgreSQL

### macOS (using Homebrew)
```bash
brew install postgresql
brew services start postgresql
```

### Windows
Download from: https://www.postgresql.org/download/windows/

### Linux (Ubuntu/Debian)
```bash
sudo apt-get install postgresql postgresql-contrib
sudo systemctl start postgresql
```

## Step 2: Create Database

Open PostgreSQL CLI:

```bash
psql -U postgres
```

Create the database:

```sql
CREATE DATABASE spark_crm;
```

Check the database was created:

```sql
\l
```

Exit PostgreSQL:

```sql
\q
```

## Step 3: Configure Environment Variables

Update `.env.local` with your database connection string:

```
DATABASE_URL="postgresql://postgres:YOUR_PASSWORD@localhost:5432/spark_crm"
```

Replace `YOUR_PASSWORD` with your PostgreSQL password.

## Step 4: Install Dependencies

```bash
npm install
```

This installs:
- `@prisma/client` - Prisma database client
- `prisma` - Prisma CLI
- `bcryptjs` - Password hashing
- All other project dependencies

## Step 5: Push Database Schema

Run migrations to create all tables:

```bash
npm run db:push
```

Or to create a named migration:

```bash
npm run db:migrate
```

## Step 6: Seed Initial Data

Populate database with sample data and default users:

```bash
npm run db:seed
```

This creates:
- 5 default users (CEO, Co-Founder, Director, Finance Manager, 2 Consultants)
- Sample universities and programs

### Default Login Credentials

After seeding, you can login with:

| Email | Password | Role |
|-------|----------|------|
| `ceo@spark-crm.com` | `demo123` | CEO/Founder |
| `cofounder@spark-crm.com` | `demo123` | Co-Founder |
| `director@spark-crm.com` | `demo123` | Director |
| `munna@spark-crm.com` | `demo123` | Finance Manager |
| `consultant1@spark-crm.com` | `demo123` | Consultant |
| `consultant2@spark-crm.com` | `demo123` | Consultant |

## Step 7: Start Development Server

```bash
npm run dev
```

Visit: http://localhost:3000

## Useful Prisma Commands

### View Database in Prisma Studio
Interactive GUI to view and manage database:
```bash
npm run db:studio
```

### Create New Migration
After modifying `prisma/schema.prisma`:
```bash
npm run db:migrate
```

### Reset Database (WARNING: Deletes all data)
```bash
npx prisma migrate reset
```

### Generate Prisma Client
After schema changes:
```bash
npx prisma generate
```

## Database Schema Overview

### Core Tables

**Users**
- id, email, password, name, phone, role, status, createdAt, lastLogin

**Leads**
- Complete lead information with status pipeline
- Assignable to consultants
- Supports multiple contact methods (phone, WhatsApp, email, WeChat, Facebook)

**Students**
- Converted from leads
- Linked to lead for history
- Documents tracking

**Applications**
- Student applications to universities
- Status tracking (Applied → Pre-admission → Admission → Visa Processing → Completed)

**Universities & Programs**
- University database with contact info and requirements
- Programs within universities
- Requirements (IELTS, HSK, age, etc.)

**Finance**
- Student payments tracking
- Office expense tracking

**Tasks & Follow-ups**
- Task management with priorities
- Follow-up scheduling

**ActivityLog**
- Complete audit trail
- Records who changed what and when
- For compliance and troubleshooting

## Troubleshooting

### Connection Error: "ECONNREFUSED"
- PostgreSQL not running
- Wrong connection string in .env.local
- Wrong port (default: 5432)

**Fix:**
```bash
# macOS
brew services start postgresql

# Linux
sudo systemctl start postgresql
```

### Error: "Database does not exist"
Create the database first:
```bash
psql -U postgres -c "CREATE DATABASE spark_crm;"
```

### Error: "password authentication failed"
Check your PostgreSQL password in .env.local:
```
DATABASE_URL="postgresql://postgres:YOUR_PASSWORD@localhost:5432/spark_crm"
```

### Error: "relation does not exist"
Run migrations:
```bash
npm run db:push
```

## Production Deployment

For production deployment:

1. Use environment-specific .env files (.env.production)
2. Set strong JWT_SECRET
3. Use managed database services (AWS RDS, DigitalOcean, etc.)
4. Enable SSL for database connections
5. Set up automated backups
6. Use connection pooling (PgBouncer)

## Need Help?

- Prisma Docs: https://www.prisma.io/docs
- PostgreSQL Docs: https://www.postgresql.org/docs
- Create an issue in the repository
