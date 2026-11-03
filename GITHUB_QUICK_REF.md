# GitHub Quick Reference

## 🚀 First Time Setup (Copy & Paste)

### 1️⃣ Open Terminal
```bash
cd /Users/jewelrashedsarker/Munna/Project/CRM
```

### 2️⃣ Initialize Git
```bash
git init
```

### 3️⃣ Create Repo on GitHub
Go to: https://github.com/new
- Name: `spark-education-crm`
- Visibility: Private
- Don't initialize anything
- Create Repository

### 4️⃣ Add Remote (Replace USERNAME)
```bash
git remote add origin https://github.com/USERNAME/spark-education-crm.git
```

### 5️⃣ First Commit & Push
```bash
git add .
git commit -m "Initial commit: Spark CRM foundation with database schema and utilities"
git branch -M main
git push -u origin main
```

**Done!** Your code is on GitHub 🎉

---

## 📝 Daily Workflow

### Make Changes → Commit → Push

```bash
# 1. See what changed
git status

# 2. Stage all changes
git add .

# 3. Commit with message
git commit -m "Your message here"

# 4. Push to GitHub
git push
```

---

## 💾 Good Commit Messages

```bash
# Feature
git commit -m "Add login authentication system"

# Bug Fix
git commit -m "Fix: Consultant permission filtering"

# Update
git commit -m "Update dashboard KPI calculations"

# Docs
git commit -m "Add database setup documentation"
```

---

## 🔍 View Status

```bash
git status           # What's changed?
git log --oneline    # Commit history
git remote -v        # Which GitHub repo?
git branch           # Current branch?
```

---

## 🌿 Branches (Optional)

```bash
# Create feature branch
git checkout -b feature/authentication

# Switch branches
git checkout main

# List branches
git branch -a

# Delete branch
git branch -d feature/authentication
```

---

## 🔄 Update from GitHub

```bash
# Pull latest changes
git pull

# Fetch without merging
git fetch
```

---

## ⚠️ Undo Changes

```bash
# Undo uncommitted changes
git restore .

# Undo last commit (keep changes)
git reset --soft HEAD~1

# Undo last commit (discard changes)
git reset --hard HEAD~1
```

---

## 🏷️ Create Release

```bash
# Tag current commit
git tag -a v1.0.0 -m "Version 1.0.0 - Foundation complete"

# Push tag to GitHub
git push origin v1.0.0

# All tags
git push origin --tags
```

---

## 📊 See Commits

```bash
git log                    # All commits
git log --oneline         # Short format
git log --graph           # Visual tree
git show COMMIT_ID        # Details of one commit
```

---

## 🚨 Secrets Leaked?

```bash
# Remove from tracking (keep locally)
git rm --cached .env.local

# Commit the fix
git add .gitignore
git commit -m "Remove .env.local from tracking"

# Push
git push

# ⚠️ Still in history - regenerate passwords if production
```

---

## 🔑 Setup SSH (Optional, More Secure)

```bash
# Generate SSH key
ssh-keygen -t ed25519 -C "your-email@example.com"

# Copy public key
cat ~/.ssh/id_ed25519.pub | pbcopy

# Add to GitHub: https://github.com/settings/keys

# Update remote to SSH
git remote set-url origin git@github.com:USERNAME/repo.git
```

---

## 📱 Clone on Another Machine

```bash
git clone https://github.com/USERNAME/spark-education-crm.git
cd spark-education-crm
npm install
cp .env.example .env.local
npm run dev
```

---

## ✅ Common Commands

| Action | Command |
|--------|---------|
| Initialize | `git init` |
| Add all | `git add .` |
| Commit | `git commit -m "msg"` |
| Push | `git push` |
| Pull | `git pull` |
| Status | `git status` |
| Log | `git log --oneline` |
| Undo | `git restore .` |
| Branch | `git checkout -b name` |

---

## 🔗 Useful Links

```
Repository:  https://github.com/USERNAME/spark-education-crm
Clone:       git clone https://github.com/USERNAME/spark-education-crm.git
Settings:    https://github.com/USERNAME/spark-education-crm/settings
Issues:      https://github.com/USERNAME/spark-education-crm/issues
```

---

## 🆘 Troubleshooting

| Issue | Fix |
|-------|-----|
| Not a git repo | `git init` |
| Remote exists | `git remote remove origin` then add new |
| Can't push | `git pull` first, then `git push` |
| Permission denied | Check SSH key or use HTTPS |
| Wrong message | `git commit --amend -m "new message"` |

---

**Full guide:** See `GITHUB_SETUP.md` for detailed instructions
