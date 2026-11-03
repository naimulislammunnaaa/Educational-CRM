# Spark Education CRM

Complete Customer Relationship Management (CRM) system for Educational Agency.

## 🚀 Features

- **Lead Management** - Track and manage student leads through the complete pipeline
- **Student Profiles** - Comprehensive student information and document management
- **Applications** - Track applications to multiple universities
- **Finance Management** - Payment tracking and expense management
- **Team Management** - Role-based access control for 5 team levels
- **Follow-ups & Tasks** - Automated follow-up tracking and task management
- **Reporting & Analytics** - Comprehensive business reports and performance metrics
- **Activity Logging** - Complete audit trail of all system changes

## 📋 Tech Stack

- **Frontend**: Next.js 14 + React 18 + TypeScript
- **Styling**: Tailwind CSS
- **Backend**: Next.js API Routes
- **Database**: PostgreSQL (with Prisma ORM)
- **Authentication**: JWT

## 🛠️ Getting Started

### Prerequisites

- Node.js 18+ 
- npm or yarn
- PostgreSQL 15+

### Installation

1. Clone the repository
```bash
git clone <repository-url>
cd CRM
```

2. Install dependencies
```bash
npm install
```

3. Configure environment variables
```bash
cp .env.local.example .env.local
# Edit .env.local with your database credentials
```

4. Run development server
```bash
npm run dev
```

5. Open [http://localhost:3000](http://localhost:3000)

## 📚 Documentation

See [ROADMAP.md](./ROADMAP.md) for detailed implementation plan and progress tracking.

## 📊 Project Structure

```
├── app/                 # Next.js app directory
├── components/          # React components
├── lib/                # Utility functions
├── types/              # TypeScript type definitions
├── hooks/              # Custom React hooks
└── ROADMAP.md          # Implementation roadmap
```

## 🔐 Permission Levels

1. **CEO/Founder** - Full access
2. **Co-Founder** - Management access
3. **Director & Finance Manager** - Operations + Finance
4. **Finance Manager** - Finance + Management
5. **Consultant** - Limited to own assigned students

## 📝 License

Private project for internal use only.

## 👥 Team

- Developed for Spark Education Agency
