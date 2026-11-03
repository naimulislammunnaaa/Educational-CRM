# How to Push Spark CRM to GitHub

Complete guide to upload your CRM code to GitHub repository.

---

## ⚙️ Prerequisites

Before starting, ensure you have:

1. **Git Installed**
   ```bash
   git --version  # Should show version 2.0+
   ```
   
   If not installed:
   - macOS: `brew install git`
   - Windows: Download from https://git-scm.com/download/win
   - Linux: `sudo apt-get install git`

2. **GitHub Account**
   - Create free account at https://github.com/signup
   - Sign in at https://github.com

3. **Git Configured** (First time only)
   ```bash
   git config --global user.name "Your Name"
   git config --global user.email "your-email@example.com"
   ```

---

## 🚀 Step-by-Step Setup

### **Option A: Using HTTPS (Easier, Recommended)**

#### Step 1: Initialize Git Repository
```bash
cd /Users/jewelrashedsarker/Munna/Project/CRM

git init
```

#### Step 2: Create GitHub Repository

Go to: https://github.com/new

**Fill in:**
- Repository name: `spark-education-crm` (or your preferred name)
- Description: "Complete CRM for Educational Agency"
- Visibility: **Private** (if personal) or **Public** (if open source)
- **DO NOT** initialize with README (you already have one)
- **DO NOT** add .gitignore (you already have one)

**Click: Create Repository**

#### Step 3: Add Remote
Copy the HTTPS URL from GitHub repo and run:

```bash
# Replace USERNAME and REPO_NAME with your GitHub details
git remote add origin https://github.com/USERNAME/spark-education-crm.git

# Verify
git remote -v
```

**Expected output:**
```
origin  https://github.com/USERNAME/spark-education-crm.git (fetch)
origin  https://github.com/USERNAME/spark-education-crm.git (push)
```

#### Step 4: Add Files
```bash
git add .
```

#### Step 5: Create Initial Commit
```bash
git commit -m "Initial commit: Spark CRM foundation with database schema and utilities"
```

#### Step 6: Set Default Branch
```bash
git branch -M main
```

#### Step 7: Push to GitHub
```bash
git push -u origin main
```

**First time:** GitHub will ask for credentials
- Enter your GitHub username
- Enter your GitHub password (or personal access token)

---

### **Option B: Using SSH (More Secure)**

#### Step 1: Generate SSH Key (If not already done)

```bash
ssh-keygen -t ed25519 -C "your-email@example.com"

# Or for older systems:
ssh-keygen -t rsa -b 4096 -C "your-email@example.com"
```

Press Enter for all prompts (use defaults)

#### Step 2: Add SSH Key to GitHub

```bash
# Copy SSH key to clipboard
cat ~/.ssh/id_ed25519.pub | pbcopy

# (Or manually: cat ~/.ssh/id_ed25519.pub)
```

Go to: https://github.com/settings/keys

**Click:** "New SSH key"
- Title: "Spark CRM"
- Key: Paste the copied key
- Click: "Add SSH key"

#### Step 3: Initialize Repository
```bash
cd /Users/jewelrashedsarker/Munna/Project/CRM
git init
```

#### Step 4: Create GitHub Repository
Same as Option A, Step 2

#### Step 5: Add SSH Remote
```bash
# Replace USERNAME and REPO_NAME
git remote add origin git@github.com:USERNAME/spark-education-crm.git

git remote -v
```

#### Step 6-7: Commit and Push
```bash
git add .

git commit -m "Initial commit: Spark CRM foundation with database schema and utilities"

git branch -M main

git push -u origin main
```

---

## 📋 First Push Checklist

Before pushing, ensure:

- [x] `.env.local` in `.gitignore` (don't commit secrets)
- [x] `node_modules/` in `.gitignore` (don't commit dependencies)
- [x] `.next/` in `.gitignore` (don't commit build artifacts)
- [x] Git initialized: `git init`
- [x] Remote added: `git remote -v` shows origin
- [x] Files staged: `git add .`
- [x] Committed: `git commit -m "..."`
- [x] Branch renamed: `git branch -M main`

---

## 🔄 Ongoing Workflow

### After Initial Push

Every time you make changes:

```bash
# 1. See what changed
git status

# 2. Stage changes
git add .

# 3. Commit with message
git commit -m "Add feature X"

# 4. Push to GitHub
git push
```

### Good Commit Messages

```bash
# ✅ Good
git commit -m "Add authentication system with JWT tokens"
git commit -m "Create dashboard with KPI widgets"
git commit -m "Fix: Consultant permission filtering on leads list"

# ❌ Avoid
git commit -m "update"
git commit -m "fixed stuff"
git commit -m "work in progress"
```

### Branch Strategy (Optional)

For better collaboration:

```bash
# Create feature branch
git checkout -b feature/authentication

# Make changes and commit
git add .
git commit -m "Add login page"

# Push feature branch
git push -u origin feature/authentication

# Then create Pull Request on GitHub
```

---

## 🔒 Protecting Sensitive Data

### Already Protected (.gitignore)

These files are NOT committed:
```
.env.local          # Database password
.env.production.local
node_modules/       # Dependencies
.next/              # Build files
.DS_Store          # macOS files
*.swp              # Editor files
```

### If You Accidentally Committed Secrets

```bash
# Remove file from git (but keep locally)
git rm --cached .env.local

# Add to .gitignore
echo ".env.local" >> .gitignore

# Commit the fix
git add .gitignore
git commit -m "Remove .env.local from tracking"

# Push
git push

# ⚠️ Note: .env.local is still in git history
# For production: regenerate all secrets/passwords
```

---

## 📊 Repository Structure on GitHub

After pushing, your GitHub repo will contain:

```
spark-education-crm/
├── app/                    # Next.js app
├── components/             # React components
├── lib/                   # Utilities
├── prisma/                # Database schema
├── types/                 # TypeScript types
├── hooks/                 # Custom hooks
├── .env.example           # Template (not .env.local!)
├── .gitignore             # What to ignore
├── package.json           # Dependencies
├── tsconfig.json          # TypeScript config
├── ROADMAP.md             # Implementation plan
├── GETTING_STARTED.md     # Setup guide
├── QUICK_START.md         # Fast reference
├── HOW_TO_VIEW.md         # How to run
├── DATABASE_SETUP.md      # DB guide
├── GITHUB_SETUP.md        # This file
└── README.md              # Project description
```

---

## 🔗 Useful GitHub Links

After pushing:

- **View repo:** `https://github.com/USERNAME/spark-education-crm`
- **Clone repo:** `https://github.com/USERNAME/spark-education-crm.git`
- **Settings:** `https://github.com/USERNAME/spark-education-crm/settings`
- **Issues:** `https://github.com/USERNAME/spark-education-crm/issues`
- **Pull Requests:** `https://github.com/USERNAME/spark-education-crm/pulls`

---

## 📱 Clone on Another Machine

To get the code on another computer:

```bash
git clone https://github.com/USERNAME/spark-education-crm.git

cd spark-education-crm

npm install

# Create .env.local with your database credentials
cp .env.example .env.local

npm run dev
```

---

## 🐛 Common Issues

### Error: "fatal: not a git repository"

**Solution:**
```bash
cd /Users/jewelrashedsarker/Munna/Project/CRM
git init
```

### Error: "remote origin already exists"

**Solution:**
```bash
# Remove existing remote
git remote remove origin

# Add new remote
git remote add origin https://github.com/USERNAME/repo.git
```

### Error: "Permission denied (publickey)"

**Solution (SSH):**
```bash
# Check SSH connection
ssh -T git@github.com

# If fails, re-add SSH key to GitHub:
# https://github.com/settings/keys
```

### Error: "Please tell me who you are"

**Solution:**
```bash
git config --global user.name "Your Name"
git config --global user.email "your-email@example.com"
```

### Large File Upload Fails

**Solution:**
```bash
# Install Git LFS (Large File Storage)
brew install git-lfs

git lfs install

# Then commit and push normally
```

---

## 📈 GitHub Features to Use

### 1. **README.md**
Already created with project info

### 2. **Issues**
Create issues for bugs/tasks:
```
GitHub Repo → Issues → New Issue → Describe problem
```

### 3. **Projects**
Track tasks visually:
```
GitHub Repo → Projects → New project
```

### 4. **Wiki**
Add documentation:
```
GitHub Repo → Wiki → New Page
```

### 5. **Releases**
Tag versions:
```bash
git tag -a v1.0.0 -m "Version 1.0.0 - Foundation complete"
git push origin v1.0.0
```

---

## 🔐 Private vs Public Repository

### **Private** (Recommended for now)
- Only you can see code
- Good for development
- Change in Settings → Visibility if needed

### **Public**
- Anyone can see code
- Good for open source
- Add LICENSE file

### **Add License** (Optional)

If public, add license:

1. Go to: `GitHub Repo → Add file → Create new file`
2. Name: `LICENSE`
3. GitHub will suggest templates
4. Commit

---

## ✅ Success Checklist

After pushing:

- [x] GitHub account created
- [x] Git installed locally
- [x] Repository created on GitHub
- [x] Remote added to local repo
- [x] Code committed locally
- [x] Pushed to GitHub
- [x] Repo visible at github.com/USERNAME/spark-education-crm
- [x] All files uploaded (except .env.local, node_modules)
- [x] .gitignore preventing sensitive files

---

## 🎯 Next Steps

### **Immediate:**
1. Follow steps above to push code to GitHub
2. Verify files appear on GitHub.com

### **Regular Workflow:**
1. Make changes locally
2. Commit: `git commit -m "description"`
3. Push: `git push`

### **Share with Team:**
1. Go to Settings → Collaborators
2. Add team members' GitHub usernames
3. They can clone and contribute

---

## 📚 Learn More

- Git documentation: https://git-scm.com/docs
- GitHub guides: https://docs.github.com
- Branching strategy: https://git-flow.readthedocs.io

---

## 🎉 Done!

Your Spark CRM code is now backed up and shareable on GitHub! 🚀
