# Spark Education CRM - Implementation Roadmap

**Project**: Spark Education CRM for Educational Agency  
**Tech Stack**: Next.js 14 + TypeScript + PostgreSQL + Tailwind CSS  
**Team Size**: 5 members with 5 permission levels  
**Status**: Planning Phase  
**Timeline**: 7 weeks (one step at a time, tested before proceeding)

---

## 📊 PROGRESS TRACKING

### Phase Completion:
- [ ] **Phase 1: Foundation & Setup** (Steps 1-3) - Step 1 ✓
- [ ] **Phase 2: Authentication & Permissions** (Steps 4-5)
- [ ] **Phase 3: Database Schema** (Step 6)
- [ ] **Phase 4: Core Modules** (Steps 7-9)
- [ ] **Phase 5: Student & Applications** (Steps 10-11)
- [ ] **Phase 6: Follow-ups & Tasks** (Step 12)
- [ ] **Phase 7: Finance Management** (Steps 13-14)
- [ ] **Phase 8: Notifications & Communication** (Step 15)
- [ ] **Phase 9: Reporting & Analytics** (Step 16)
- [ ] **Phase 10: Advanced Features & Deployment** (Steps 17-19)

### Step-by-Step Progress:
- [x] Step 1: Project Setup & Environment Configuration
- [x] Step 2: Database Setup & Prisma Configuration
- [x] Step 3: Project Folder Structure & Utilities
- [ ] Step 4: User Authentication System
- [ ] Step 5: Role-Based Access Control (RBAC) System
- [ ] Step 6: Complete Database Schema Design
- [ ] Step 7: Dashboard Module (CEO/Founder View)
- [ ] Step 8: Lead Management Module
- [ ] Step 9: Lead Status & Pipeline System
- [ ] Step 10: Student Profile & Document Management
- [ ] Step 11: Application & University Management
- [ ] Step 12: Follow-up System & Task Management
- [ ] Step 13: Student Payment & Finance Tracking
- [ ] Step 14: Expense Management & Financial Reports
- [ ] Step 15: Notification & Communication History System
- [ ] Step 16: Comprehensive Reporting System
- [ ] Step 17: Team Management & User Administration
- [ ] Step 18: Data Export, Backup & System Settings
- [ ] Step 19: Testing, Optimization & Deployment

---

## PHASE 1: FOUNDATION & SETUP (Steps 1-3)

### Step 1: Project Setup & Environment Configuration
**Objective**: Initialize the Next.js project with TypeScript, Tailwind, and development environment

**Files to Create**:
- `package.json` - Project dependencies
- `.env.local` - Environment variables
- `tsconfig.json` - TypeScript configuration
- `tailwind.config.ts` - Tailwind setup
- `next.config.js` - Next.js configuration
- `.gitignore` - Git ignore rules
- `README.md` - Project documentation

**Testing**:
- Run `npm run dev` and verify app starts on localhost:3000
- Verify TypeScript compilation has no errors
- Confirm Tailwind CSS is working

**Deliverable**: Running Next.js app with TypeScript and Tailwind

---

### Step 2: Database Setup & Prisma Configuration
**Objective**: Set up PostgreSQL database and Prisma ORM

**Files to Create**:
- `prisma/schema.prisma` - Database schema definition
- `.env.local` (updated) - Database connection string
- `lib/db.ts` - Database client utility
- `migrations/` - Initial migration files

**Database Details**:
- PostgreSQL 15+
- Connection pooling with PgBouncer
- Support for 1000+ concurrent students

**Testing**:
- Successfully connect to PostgreSQL
- Run migrations without errors
- Verify Prisma Studio (`npx prisma studio`) loads

**Deliverable**: Connected PostgreSQL database with Prisma ORM

---

### Step 3: Project Folder Structure & Utilities
**Objective**: Create organized folder structure and common utilities

**Files to Create**:
```
src/
├── app/                    # Next.js app directory
├── components/             # Reusable React components
│   ├── dashboard/
│   ├── leads/
│   ├── ui/                # UI components (buttons, modals, etc.)
├── lib/                   # Utilities and helpers
│   ├── db.ts
│   ├── auth.ts
│   ├── permissions.ts
│   ├── constants.ts
├── hooks/                 # Custom React hooks
├── types/                 # TypeScript type definitions
├── styles/                # Global styles
```

**Testing**:
- All imports resolve correctly
- No TypeScript errors
- Directory structure matches design

**Deliverable**: Clean, organized project structure

---

## PHASE 2: AUTHENTICATION & PERMISSIONS (Steps 4-5)

### Step 4: User Authentication System
**Objective**: Implement JWT-based authentication with login/logout

**Files to Create**:
- `app/api/auth/login/route.ts` - Login API endpoint
- `app/api/auth/logout/route.ts` - Logout API endpoint
- `app/api/auth/register/route.ts` - User registration
- `lib/auth.ts` - JWT utilities
- `middleware.ts` - Authentication middleware
- `app/(auth)/login/page.tsx` - Login page UI
- `types/auth.ts` - Auth type definitions

**Testing**:
- Register new user - verify user created in DB
- Login with correct credentials - verify JWT token returned
- Login with wrong credentials - verify error message
- Access protected route without token - verify redirect to login
- Access protected route with valid token - verify access granted

**Deliverable**: Fully functional login/logout system

---

### Step 5: Role-Based Access Control (RBAC) System
**Objective**: Implement 5-level permission hierarchy with strict access rules

**Permission Levels**:
1. **Level 1 - Founder & CEO**: Full access to all modules
2. **Level 2 - Co-Founder**: Management access (Leads, Students, Applications, Universities, Reports, Finance View)
3. **Level 3 - Director & Finance Manager**: Operations + Finance (Students, Applications, Documents, Payments, Expenses, Finance Reports, Office Operations)
4. **Level 4 - Finance Manager (Munna Mama)**: Finance + Management (Finance, Payments, Expenses, Reports, Salary Sheet, Daily Reports)
5. **Level 5 - Consultant**: Limited access (Only own Leads, Students, Applications, Follow-ups, Documents, Tasks, Check-in)

**Files to Create**:
- `lib/permissions.ts` - Permission checking logic
- `types/roles.ts` - Role and permission type definitions
- `app/api/users/[id]/update-role/route.ts` - Update user role API
- `components/auth/ProtectedRoute.tsx` - Route protection component
- `hooks/useAuth.ts` - Auth hook with permission checking
- `lib/permissionMatrix.ts` - Centralized permission rules
- Database seed file for initial admin user

**Permission Matrix with Specific Rules**:

| Feature | CEO | Co-Founder | Director | Finance Mgr | Consultant |
|---------|-----|-----------|----------|-------------|-----------|
| **All Leads** | ✓ | ✓ | ✗ | ✗ | Own only |
| **All Students** | ✓ | ✓ | ✗ | ✗ | Own only |
| **Finance (View)** | ✓ | ✓ | ✗ | ✓ | ✗ |
| **Finance (Edit)** | ✓ | ✗ | ✗ | ✓ | ✗ |
| **Delete Records** | ✓ | ✗ | ✗ | ✗ | ✗ |
| **Team Management** | ✓ | Monitor | ✗ | ✗ | ✗ |
| **Reports** | ✓ | ✓ | ✓ | ✓ | Own only |

**Critical Permission Rules**:
1. ✅ **Consultants see ONLY their assigned students/leads**
   - API filters automatically by `assignedTo == currentUser.id`
   - Cannot access other consultant's data even with direct URL
2. ✅ **Finance access restricted to: CEO, Co-Founder, Finance Manager**
   - Finance routes completely hidden for others
   - API returns 403 Forbidden for unauthorized access
3. ✅ **Only CEO can delete records**
   - All delete endpoints check `role === 'CEO'`
   - Audit log records who attempted deletion
4. ✅ **Activity log on every action**
   - See Step 6 for activity log table details

**Testing**:
- Login as Consultant - verify only own data visible
- Login as Consultant - try accessing /finance route - verify 403
- Login as Finance Manager - verify can see/edit finance
- Try delete as Co-Founder - verify denied
- Verify activity log records permission denials
- Test API filters consultant-only queries

**Deliverable**: Complete role-based access control system with strict permission enforcement

---

## PHASE 3: DATABASE SCHEMA (Step 6)

### Step 6: Complete Database Schema Design
**Objective**: Design and validate database schema for all modules

**Core Tables** (based on PDF requirements):

#### User & Team Management
- `users` - All users (id, email, password, name, role, status)
- `teams` - Team structure (if needed)
- `user_profiles` - Extended user info (phone, avatar, address)

#### Lead Management
- `leads` - Basic lead info (id, studentName, phone, email, leadSource, status, assignedTo, createdAt)
- `lead_education` - Education details (qualification, gpa, ielts, hsk, studyGap)
- `lead_preferences` - Study preferences (desiredCountry, preferredDegree, major, budget)
- `lead_source_enum` - Lead source types (Facebook, TikTok, Website, WhatsApp, Referral, etc.)
- `lead_status_enum` - Status pipeline (NEW_LEAD, CONTACTED, COUNSELLING, INTERESTED, etc.)

#### Student & Application Management
- `students` - Student records (when lead becomes serious)
- `applications` - Application to universities (studentId, universityId, programId, status, applicationDate)
- `application_status_enum` - (APPLIED, PRE_ADMISSION, ADMISSION, VISA_PROCESSING, VISA_APPROVED, COMPLETED)

#### Document Management
- `documents` - Student documents (id, studentId, documentType, filePath, status, uploadedAt)
- `document_type_enum` - Required documents (Passport, Certificate, Transcript, IELTS, etc.)
- `document_status_enum` - (RECEIVED, MISSING, NEED_CORRECTION, VERIFIED)

#### University & Program Management
- `universities` - University list (name, province, city, ranking, website, contactPerson, email)
- `university_programs` - Programs offered (universityId, degree, major, language, tuition, duration)
- `program_requirements` - Requirements for programs (universityId, ielts, hsk, age, etc.)

#### Finance Management
- `student_payments` - Payment tracking (studentId, totalFee, paid, due, paymentMethod, status)
- `payment_breakdowns` - Detailed fees (serviceFee, applicationFee, universityFee, visaFee, otherFee)
- `expenses` - Office expenses (amount, category, date, description, approvedBy)
- `expense_categories` - (OFFICE_RENT, SALARY, MARKETING, FACEBOOK_ADS, TIKTOK_ADS, TRANSPORTATION, etc.)

#### Tasks & Follow-ups
- `tasks` - Task management (id, studentId, taskType, assignedTo, deadline, priority, status)
- `task_types_enum` - (CALL_STUDENT, WHATSAPP, COLLECT_DOCUMENT, CHECK_APPLICATION, etc.)
- `follow_ups` - Follow-up records (id, leadId/studentId, date, time, type, note, result, nextFollowUp)

#### Communication & Activity (CRITICAL FOR AUDIT TRAIL)
- `activity_log` - **Complete audit history** (id, entityType, entityId, userId, action, oldValue, newValue, description, timestamp, ipAddress)
  - Records EVERY change: lead status, payment amount, document upload, student assigned, etc.
  - Old and new values for tracking exactly what changed
  - Who made the change and when
  - Used for compliance and troubleshooting
- `communication_history` - Communication records (id, studentId, type, date, notes, attachments)

#### Reports & Analytics (Support Tables)
- `lead_source_stats` - Cached stats (for performance)
- `conversion_rate_cache` - Performance optimization

**Data Relationships**:
```
users (1) ── (n) leads
leads (1) ── (1) students (when converted)
students (1) ── (n) applications
students (1) ── (n) documents
students (1) ── (1) student_payments
applications (n) ── (1) universities
applications (n) ── (1) university_programs
students (1) ── (n) follow_ups
students (1) ── (n) tasks
students (1) ── (n) activity_log
expenses (n) ── (1) expense_categories
```

**Testing**:
- Validate schema with Prisma
- Run migrations successfully
- Create sample records for each table
- Test relationships and foreign keys
- Performance: Query 1000 leads with filters - should return < 500ms

**Deliverable**: Validated PostgreSQL schema with all relationships

---

## PHASE 4: CORE MODULES (Steps 7-9)

### Step 7: Dashboard Module (CEO/Founder View)
**Objective**: Build comprehensive dashboard with KPIs and overview

**Components to Create**:
- `app/dashboard/page.tsx` - Main dashboard
- `components/dashboard/LeadOverview.tsx` - Lead KPIs
- `components/dashboard/ApplicationOverview.tsx` - Application KPIs
- `components/dashboard/FinanceOverview.tsx` - Finance KPIs
- `components/dashboard/TeamPerformance.tsx` - Team metrics
- `components/dashboard/Charts.tsx` - Chart components

**Dashboard Metrics**:
- **Lead Overview**: Total Leads, New Leads Today, Hot Leads, Follow-ups Due, Converted, Lost
- **Application Overview**: Files Opened, Docs Pending, Applied, Pre-Admission, Admission, Visa Processing, Visa Approved, Completed
- **Finance**: Total Revenue, Received, Pending, Expenses, Net Profit
- **Team**: Consultant-wise Leads, Files, Conversion Rate, Follow-up Performance

**API Endpoints**:
- `GET /api/dashboard/stats` - Get all dashboard stats
- `GET /api/dashboard/lead-stats` - Lead breakdown
- `GET /api/dashboard/finance-stats` - Finance overview

**Testing**:
- Verify all metrics calculate correctly
- Test with different date ranges
- Performance: Dashboard loads in < 2 seconds
- Role-based visibility (Co-Founder sees limited data)

**Deliverable**: Functional dashboard with live KPIs

---

### Step 8: Lead Management Module
**Objective**: Create comprehensive lead management system with full CRUD operations

**Pages & Components**:
- `app/leads/page.tsx` - Lead list view
- `app/leads/[id]/page.tsx` - Lead detail view
- `app/leads/new/page.tsx` - New lead form
- `components/leads/LeadForm.tsx` - Form component
- `components/leads/LeadTable.tsx` - List table
- `components/leads/LeadCard.tsx` - Lead card view
- `components/leads/LeadFilters.tsx` - Filter component
- `components/leads/LeadPipeline.tsx` - Pipeline view (drag-drop status)

**Form Fields**:
- Basic Info: Name, Phone, WhatsApp, Email, Gender, DOB, Nationality, Country, City
- Education: Qualification, GPA, IELTS, HSK, Study Gap, Graduation Year
- Preferences: Desired Country, Degree, Major, Medium, Intake, Scholarship, Budget
- Lead Source: Dropdown (Facebook, TikTok, Website, WhatsApp, Referral, etc.)

**API Endpoints**:
- `GET /api/leads` - List leads (with filters, pagination)
- `GET /api/leads/[id]` - Get lead details
- `POST /api/leads` - Create lead
- `PUT /api/leads/[id]` - Update lead
- `DELETE /api/leads/[id]` - Delete lead
- `PUT /api/leads/[id]/status` - Update lead status
- `PUT /api/leads/[id]/assign` - Assign to consultant

**Testing**:
- Create new lead - verify all fields saved
- Update lead - verify changes in DB
- Filter leads by source - verify correct results
- Assign lead to consultant - verify permissions
- Pagination: 10, 20, 50 per page

**Deliverable**: Full lead management CRUD system

---

### Step 9: Lead Status & Pipeline System
**Objective**: Implement lead status workflow with pipeline visualization

**Components**:
- `components/leads/Pipeline.tsx` - Kanban pipeline view
- `components/leads/StatusTransition.tsx` - Status change logic
- `lib/leadWorkflow.ts` - Pipeline workflow rules

**Pipeline Statuses** (from PDF):
```
NEW_LEAD
    ↓
CONTACTED
    ↓
COUNSELLING
    ↓
INTERESTED
    ↓
DOCUMENT_COLLECTION
    ↓
FILE_OPENED
    ↓
UNIVERSITY_SHORTLIST
    ↓
APPLICATION_SUBMITTED
    ↓
PRE_ADMISSION
    ↓
ADMISSION
    ↓
VISA_PROCESSING

Exit Statuses:
├─ NOT_INTERESTED
├─ NO_RESPONSE
├─ NOT_ELIGIBLE
└─ LOST
```

**Features**:
- Drag-drop status change
- Automatic timestamp on status change
- Activity log entry for each transition
- Validation rules (can't skip stages)
- View stats by stage

**API Endpoints**:
- `PUT /api/leads/[id]/status` - Change status (with validation)
- `GET /api/leads/stats/by-status` - Count by status

**Testing**:
- Move lead through complete pipeline
- Try invalid transitions - verify rejection
- Verify activity log created for each transition
- Test bulk status updates
- Performance: Load 100 leads in pipeline view < 1 second

**Deliverable**: Full pipeline workflow system

---

## PHASE 5: STUDENT & APPLICATION MANAGEMENT (Steps 10-11)

### Step 10: Student Profile & Document Management
**Objective**: Convert leads to students and manage documents

**Pages & Components**:
- `app/students/page.tsx` - Student list
- `app/students/[id]/page.tsx` - Student detail (complete profile)
- `components/students/StudentForm.tsx` - Student form
- `components/students/DocumentUpload.tsx` - Document upload
- `components/students/DocumentChecklist.tsx` - Document status tracker

**Tabs in Student Profile**:
1. **Personal Information** - All basic info from lead
2. **Education** - Education background
3. **Passport** - Passport details
4. **Documents** - Document management
5. **University** - Applied universities
6. **Program** - Selected programs
7. **Scholarship** - Scholarship info
8. **Application** - Application status
9. **Payment** - Payment tracking
10. **Visa** - Visa application status
11. **Travel** - Travel dates
12. **Communication History** - Activity timeline

**Documents to Track**:
- Passport, Passport Photo, SSC/High School Certificates & Transcripts
- Bachelor Certificate & Transcript, IELTS/HSK scores
- CV, Study Plan, Recommendation Letters, Bank Statements
- Police Clearance, Medical, Other

**Document Statuses**: Received, Missing, Need Correction, Verified

**API Endpoints**:
- `GET /api/students` - List students
- `GET /api/students/[id]` - Student details
- `POST /api/students` - Create student (from lead)
- `PUT /api/students/[id]` - Update student
- `POST /api/students/[id]/documents` - Upload document
- `PUT /api/students/[id]/documents/[docId]` - Update document status
- `GET /api/students/[id]/documents` - Get student documents

**Testing**:
- Convert lead to student - verify data transfer
- Upload document - verify file saved and metadata stored
- Update document status - verify activity log
- View student profile - verify all tabs load correctly
- File upload: Test different file types and sizes

**Deliverable**: Complete student management with document tracking

---

### Step 11: Application & University Management
**Objective**: Track student applications to multiple universities

**Pages & Components**:
- `app/applications/page.tsx` - Applications list
- `app/applications/[id]/page.tsx` - Application detail
- `components/applications/ApplicationForm.tsx` - Application creation
- `components/applications/UniversitySearch.tsx` - University selector
- `components/universities/UniversityList.tsx` - University catalog

**University Database Fields**:
- Name, Province, City, Ranking
- Website, Contact Person, WeChat, Email
- Agent Contact, Portal Available?, Intake, Deadline
- Programs offered, Requirements (IELTS, CSCA, Age, etc.)
- Fees (Application, Tuition, Hostel, Scholarship available)

**Application Status Pipeline**:
- APPLIED → PRE_ADMISSION → ADMISSION → VISA_PROCESSING → VISA_APPROVED → COMPLETED

**API Endpoints**:
- `GET /api/applications` - List applications
- `POST /api/applications` - Create application
- `PUT /api/applications/[id]` - Update application
- `PUT /api/applications/[id]/status` - Change status
- `GET /api/universities` - List universities (with search/filter)
- `GET /api/universities/[id]` - University details with programs
- `POST /api/universities` - Add university (Admin only)
- `GET /api/programs` - List programs (with filters)

**Testing**:
- Create application - verify lead/student/university linked
- Search universities by country/name - verify correct results
- Change application status - verify workflow validation
- View student's multiple applications - verify correct data

**Deliverable**: Complete application management system

---

## PHASE 6: FOLLOW-UPS & TASKS (Step 12)

### Step 12: Follow-up System & Task Management
**Objective**: Implement critical follow-up and task tracking

**Components**:
- `components/followups/FollowUpForm.tsx` - Create follow-up
- `components/followups/FollowUpList.tsx` - Upcoming follow-ups
- `components/tasks/TaskBoard.tsx` - Task management
- `components/tasks/TaskCard.tsx` - Individual task

**Follow-up Fields**:
- Date, Time, Type (Call, WhatsApp, Email, Meeting, etc.)
- Notes, Result, Next Follow-up date
- Assigned consultant
- Linked to Lead/Student/Application

**Task Types**:
- CALL_STUDENT
- WHATSAPP_STUDENT
- COLLECT_DOCUMENT
- CHECK_APPLICATION
- CONTACT_UNIVERSITY
- PAYMENT_FOLLOW_UP
- VISA_FOLLOW_UP
- INTERNAL_TASK

**Features**:
- Dashboard widget: "Today's Follow-ups" (for consultants)
- Automatic notifications when follow-up due
- Follow-up history timeline
- Task priority levels (Low, Medium, High)
- Task status (Pending, In Progress, Completed)

**API Endpoints**:
- `GET /api/follow-ups` - List follow-ups (with filters)
- `GET /api/follow-ups/today` - Today's follow-ups
- `POST /api/follow-ups` - Create follow-up
- `PUT /api/follow-ups/[id]` - Update follow-up
- `GET /api/tasks` - List tasks
- `POST /api/tasks` - Create task
- `PUT /api/tasks/[id]/status` - Update task status

**Testing**:
- Create follow-up for future date
- Verify "Today's Follow-ups" dashboard widget shows correct count
- Complete follow-up and log result
- Create tasks with different priorities
- View follow-up history on student profile

**Deliverable**: Complete follow-up and task system

---

## PHASE 7: FINANCE MANAGEMENT (Steps 13-14)

### Step 13: Student Payment & Finance Tracking
**Objective**: Track student payments and financial data

**Pages & Components**:
- `app/finance/payments/page.tsx` - Payment list
- `app/finance/payments/[id]/page.tsx` - Payment detail
- `components/finance/PaymentForm.tsx` - Record payment
- `components/finance/PaymentStatus.tsx` - Payment status tracker

**Payment Fields** (per student):
- Total Service Fee
- Application Fee, University Fee, Visa Fee, Other Fees
- Paid amount, Due amount
- Payment Date, Payment Method (Bank Transfer, Cash, Cheque, etc.)
- Payment Status (PENDING, PARTIAL, PAID)

**Payment Tracking Features**:
- Payment schedule/installments
- Payment receipt generation
- Reminder for due payments
- Invoice generation

**API Endpoints**:
- `GET /api/finance/payments` - List payments (with filters)
- `GET /api/finance/payments/[id]` - Payment details
- `POST /api/finance/payments` - Record payment
- `PUT /api/finance/payments/[id]` - Update payment
- `GET /api/finance/reports/outstanding` - Outstanding payments

**Testing**:
- Record payment - verify balance updated
- Create partial payment - verify remaining calculated
- Generate receipt - verify PDF download
- Filter by status (Pending, Partial, Paid)

**Deliverable**: Complete payment tracking system

---

### Step 14: Expense Management & Financial Reports
**Objective**: Track office expenses and generate financial reports

**Pages & Components**:
- `app/finance/expenses/page.tsx` - Expense list
- `app/finance/expenses/new/page.tsx` - New expense form
- `app/finance/reports/page.tsx` - Financial reports

**Expense Categories**:
- OFFICE_RENT
- SALARY
- MARKETING
- FACEBOOK_ADS
- TIKTOK_ADS
- TRANSPORTATION
- UNIVERSITY_PAYMENT
- VISA_RELATED
- REFUND
- OTHER

**Finance Reports**:
1. **Profit & Loss** - Revenue, Expenses, Net Profit
2. **Payment Summary** - Total Collected, Pending, Outstanding
3. **Consultant-wise Collection** - Who collected how much
4. **Expense Breakdown** - By category
5. **University Report** - Applications and admissions per university

**API Endpoints**:
- `GET /api/finance/expenses` - List expenses
- `POST /api/finance/expenses` - Record expense
- `GET /api/finance/reports/summary` - Financial summary
- `GET /api/finance/reports/profit-loss` - P&L report
- `GET /api/finance/reports/consultant-collection` - Consultant performance

**Testing**:
- Record expenses in different categories
- Generate P&L report - verify calculations
- Filter reports by date range
- Export reports to Excel/PDF

**Deliverable**: Complete finance management and reporting

---

## PHASE 8: NOTIFICATIONS & COMMUNICATION (Step 15)

### Step 15: Notification & Communication History System
**Objective**: Automatic notifications and communication tracking

**Components**:
- `components/notifications/NotificationBell.tsx` - Notification UI
- `components/notifications/NotificationCenter.tsx` - Notification list
- `components/communication/ActivityTimeline.tsx` - Communication history

**Automatic Notifications**:
- **For Consultants**: Follow-up due, New lead assigned, Document missing, Task deadline, Student reply
- **For Finance**: Payment due, Payment received, Refund request
- **For Founder**: New high-value lead, File opened, Admission received, Visa approved, Payment received, Lost lead, Team performance alert

**Communication History Features**:
- Activity timeline on student profile
- All actions logged (lead creation, status changes, payments, documents, etc.)
- Who did what and when
- Timestamp for every action

**API Endpoints**:
- `GET /api/notifications` - Get user notifications
- `GET /api/notifications/unread` - Unread count
- `PUT /api/notifications/[id]/read` - Mark as read
- `GET /api/students/[id]/activity` - Student activity timeline

**Testing**:
- Create follow-up and verify notification sent
- Receive payment and verify notification
- View activity timeline on student
- Mark notification as read
- Filter notifications by type

**Deliverable**: Complete notification and communication system

---

## PHASE 9: REPORTING & ANALYTICS (Step 16)

### Step 16: Comprehensive Reporting System
**Objective**: Create all business reports for data-driven decisions

**Report Types**:

1. **Lead Reports**:
   - Total leads by status
   - Source-wise leads
   - Country-wise leads
   - Consultant-wise leads
   - Conversion rate

2. **Application Reports**:
   - Files opened
   - Applications submitted
   - Pre-admissions
   - Admissions
   - Visa applications
   - Visa approvals

3. **Financial Reports**:
   - Revenue vs Expenses
   - Net profit
   - Outstanding payments
   - Consultant-wise collection
   - Payment method breakdown

4. **University Reports**:
   - Applications per university
   - Admissions per university
   - Success rate per university

5. **Team Reports**:
   - Consultant performance
   - Leads per consultant
   - Conversion rate per consultant
   - Collection per consultant
   - Follow-up performance

**Pages & Components**:
- `app/reports/page.tsx` - Report dashboard
- `components/reports/LeadReport.tsx` - Lead analysis
- `components/reports/FinanceReport.tsx` - Finance analysis
- `components/reports/UniversityReport.tsx` - University performance

**Export Formats**: PDF, Excel, CSV

**API Endpoints**:
- `GET /api/reports/leads` - Lead report data
- `GET /api/reports/applications` - Application report
- `GET /api/reports/finance` - Finance report
- `GET /api/reports/university` - University report
- `GET /api/reports/team` - Team performance

**Testing**:
- Generate each report type
- Verify calculations are correct
- Test date range filtering
- Export to different formats
- Performance: Large reports (10k records) load in < 5 seconds

**Deliverable**: Complete reporting dashboard

---

## PHASE 10: ADVANCED FEATURES (Steps 17-18)

### Step 17: Team Management & User Administration
**Objective**: Manage team members and their permissions

**Pages & Components**:
- `app/team/page.tsx` - Team member list
- `app/team/new/page.tsx` - Add team member
- `components/team/UserTable.tsx` - User management table
- `components/team/RoleAssignment.tsx` - Assign roles

**Features**:
- Add/remove team members
- Assign roles (CEO, Co-Founder, Director, Finance Manager, Consultant)
- View member activity (who logged in when, what actions)
- Manage permissions per role
- Salary sheet management (for Finance Manager)
- Daily check-in reports

**User Information**:
- Name, Email, Phone
- Role, Status (Active/Inactive)
- Date Joined, Last Login
- Assigned Leads/Students (for Consultants)

**API Endpoints**:
- `GET /api/users` - List users (Admin only)
- `POST /api/users` - Create user
- `PUT /api/users/[id]` - Update user
- `PUT /api/users/[id]/role` - Change role
- `GET /api/users/activity` - User activity logs

**Testing**:
- Create new user with specific role
- Verify role-based access works
- Change user role - verify permissions update
- View user activity logs

**Deliverable**: Complete team management system

---

### Step 18: Data Export, Backup & System Settings
**Objective**: System administration features

**Pages & Components**:
- `app/settings/page.tsx` - System settings
- `app/settings/backup/page.tsx` - Backup management
- `components/admin/DataExport.tsx` - Export data

**Features**:
1. **Data Export**:
   - Export all students to Excel
   - Export all leads to CSV
   - Export financial data
   - Bulk import data

2. **Backup & Recovery**:
   - Automatic daily backups
   - Manual backup download
   - Backup restore (Admin only)
   - Backup schedule configuration

3. **System Settings**:
   - Company information
   - Currency and timezone
   - Email templates
   - Notification preferences
   - Custom fields (if needed)

4. **Audit Logs**:
   - All user actions logged
   - Login history
   - Data modification history
   - Admin actions

**API Endpoints**:
- `POST /api/export/students` - Export students
- `POST /api/export/leads` - Export leads
- `POST /api/export/financial` - Export finance data
- `GET /api/admin/backup` - List backups
- `POST /api/admin/backup` - Create backup
- `GET /api/admin/audit-logs` - Audit logs

**Testing**:
- Export data in multiple formats
- Verify exported data integrity
- Test bulk import
- Create and verify backups

**Deliverable**: Complete admin and backup system

---

## DEPLOYMENT PREPARATION (Step 19)

### Step 19: Testing, Optimization & Deployment
**Objective**: Ensure CRM is production-ready

**Tasks**:
1. **Testing**:
   - Unit tests for utilities
   - Integration tests for APIs
   - E2E tests for critical workflows
   - Performance testing

2. **Optimization**:
   - Database query optimization
   - API response time < 500ms
   - Frontend bundle optimization
   - Image compression
   - Caching strategy

3. **Security**:
   - HTTPS everywhere
   - SQL injection prevention
   - XSS prevention
   - CSRF tokens
   - Rate limiting on APIs
   - Input validation

4. **Deployment**:
   - Choose hosting (Vercel, AWS, DigitalOcean)
   - Environment configuration
   - Database backups
   - Monitoring setup
   - Error tracking (Sentry)

5. **Documentation**:
   - API documentation
   - User manual
   - Admin guide
   - Developer guide

---

## IMPLEMENTATION ORDER

**Week 1-2**: Steps 1-6 (Foundation + Schema)  
**Week 2-3**: Steps 7-9 (Dashboard + Leads)  
**Week 3-4**: Steps 10-11 (Students + Applications)  
**Week 4-5**: Steps 12-14 (Follow-ups + Finance)  
**Week 5-6**: Steps 15-16 (Notifications + Reports)  
**Week 6-7**: Steps 17-18 (Team + Admin)  
**Week 7**: Step 19 (Testing + Deploy)  

---

## TESTING STRATEGY

Each step includes:
- ✅ Unit tests (utilities, calculations)
- ✅ Integration tests (API endpoints)
- ✅ E2E tests (critical workflows)
- ✅ Performance tests (load times, query performance)
- ✅ Security tests (permission checks, data validation)

---

## TECH STACK DETAILS

**Frontend**:
- Next.js 14+ (React 18+)
- TypeScript
- Tailwind CSS
- React Hook Form
- Zustand (state management)
- TanStack Query (data fetching)
- Shadcn/ui components

**Backend**:
- Next.js API Routes
- Prisma ORM
- PostgreSQL
- JWT authentication

**Tools**:
- ESLint + Prettier
- Jest (testing)
- Playwright (E2E)
- Docker (containerization)

---

## APPROVED REQUIREMENTS (From User Feedback)

✅ **Permission Rules**:
- Consultants see ONLY their assigned students (filtered at API & UI level)
- Finance visible ONLY to: CEO, Co-Founder, Finance Manager
- Only CEO can delete records
- All denials logged in activity_log

✅ **Schema Requirements**:
- Activity log table with detailed audit trail (who changed what, when, old/new values)
- Recorded for every action (lead status, payment, document, assignment, etc.)

✅ **Timeline & Process**:
- 7 weeks is acceptable
- Go one step at a time
- Test each step before moving to next
- Mark steps complete as we finish

✅ **Documentation**:
- ROADMAP.md saved in project (tracking checklist above)
- Each step tested before proceeding
- Activity log provides full audit trail for compliance

---

## NEXT STEPS

### How We'll Work:
1. **Start Step 1** - Project Setup
2. I'll create all necessary files
3. You test it works (run `npm run dev`, verify setup)
4. When confirmed working → **Update ROADMAP.md** (check off completed step)
5. Move to Step 2, repeat process

### What To Test:
- Run the development server
- Verify no errors in console/terminal
- Check that all dependencies install correctly
- Confirm TypeScript compiles without errors

---

## ✅ READY TO START?

**Type "START STEP 1" when you're ready to begin the implementation!**

The roadmap is complete, requirements are documented, and we're ready to build Spark CRM step by step. 🚀
