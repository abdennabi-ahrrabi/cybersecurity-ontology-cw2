# Git Setup Guide for CW2 Cybersecurity Ontology Project

## Prerequisites
- Git installed on your system
- GitHub account created
- GitHub repository created (e.g., `cybersecurity-ontology-cw2`)

---

## Step 1: Initialize Git Repository

Open terminal in the CW2 directory and run:

```bash
cd /c/src/Ulster/kG/CW2
git init
```

**Expected output:**
```
Initialized empty Git repository in C:/src/Ulster/kG/CW2/.git/
```

---

## Step 2: Configure Git (First Time Only)

Set your name and email (use your university email):

```bash
git config --global user.name "Your Name"
git config --global user.email "your.email@ulster.ac.uk"
```

---

## Step 3: Add Files to Git

### Option A: Add Essential Files Only (Recommended)

```bash
# Add the main ontology files
git add CybersecurityOntology_ENHANCED.owl
git add CybersecurityOntology_SWRL_Rules.swrl

# Add documentation
git add TECHNICAL_REPORT_Ontology_Enhancement.md
git add SWRL_REASONING_GUIDE.md
git add PRODUCTION_SYSTEM_FEATURES.md
git add README.md
git add INDEX.md

# Add .gitignore
git add .gitignore
```

### Option B: Add All Files (Including Development History)

```bash
# Add everything except what's in .gitignore
git add .
```

### Check What Will Be Committed

```bash
git status
```

**You should see:**
```
On branch main

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   .gitignore
        new file:   CybersecurityOntology_ENHANCED.owl
        new file:   CybersecurityOntology_SWRL_Rules.swrl
        new file:   PRODUCTION_SYSTEM_FEATURES.md
        new file:   README.md
        new file:   SWRL_REASONING_GUIDE.md
        new file:   TECHNICAL_REPORT_Ontology_Enhancement.md
        ...
```

---

## Step 4: Create Initial Commit

```bash
git commit -m "Initial commit: Enhanced Cybersecurity Ontology v2.0 with SWRL production rules"
```

**Expected output:**
```
[main (root-commit) a1b2c3d] Initial commit: Enhanced Cybersecurity Ontology v2.0 with SWRL production rules
 7 files changed, 5000+ insertions(+)
 create mode 100644 .gitignore
 create mode 100644 CybersecurityOntology_ENHANCED.owl
 ...
```

---

## Step 5: Connect to GitHub

### Create Repository on GitHub:
1. Go to https://github.com
2. Click "+" → "New repository"
3. Name: `cybersecurity-ontology-cw2` (or your choice)
4. Description: "Enhanced Cybersecurity Ontology with SWRL Production Rules - Ulster University CW2"
5. Choose "Public" or "Private"
6. **DO NOT** initialize with README (you already have one)
7. Click "Create repository"

### Link Local Repository to GitHub:

Replace `YOUR_USERNAME` with your GitHub username:

```bash
git remote add origin https://github.com/YOUR_USERNAME/cybersecurity-ontology-cw2.git
```

### Verify Remote Connection:

```bash
git remote -v
```

**Expected output:**
```
origin  https://github.com/YOUR_USERNAME/cybersecurity-ontology-cw2.git (fetch)
origin  https://github.com/YOUR_USERNAME/cybersecurity-ontology-cw2.git (push)
```

---

## Step 6: Push to GitHub

### First Push:

```bash
git branch -M main
git push -u origin main
```

**You may be prompted for credentials:**
- Username: Your GitHub username
- Password: Use a **Personal Access Token** (not your GitHub password)

### How to Create GitHub Personal Access Token:
1. GitHub → Settings → Developer settings → Personal access tokens → Tokens (classic)
2. Click "Generate new token" → "Generate new token (classic)"
3. Name: `Ulster CW2 Project`
4. Expiration: Select appropriate duration
5. Scopes: Check `repo` (full control of private repositories)
6. Click "Generate token"
7. **COPY THE TOKEN** (you won't see it again!)
8. Use this token as your password when pushing

---

## Step 7: Verify on GitHub

1. Go to your GitHub repository URL
2. Refresh the page
3. You should see all your files uploaded

---

## Daily Workflow (After Initial Setup)

### When You Make Changes:

```bash
# Check what changed
git status

# Add specific files
git add filename.md

# Or add all changes
git add .

# Commit with descriptive message
git commit -m "Updated SWRL rules documentation"

# Push to GitHub
git push
```

---

## Common Git Commands

### View Commit History:
```bash
git log --oneline
```

### Undo Last Commit (Keep Changes):
```bash
git reset --soft HEAD~1
```

### Discard Changes in a File:
```bash
git checkout -- filename.txt
```

### Create a New Branch:
```bash
git checkout -b feature-branch-name
```

### Switch Branches:
```bash
git checkout main
```

### View Differences:
```bash
git diff filename.txt
```

---

## Recommended Commit Messages

Use clear, descriptive messages:

✅ **Good Examples:**
- `"Added 10 SWRL production rules for threat detection"`
- `"Enhanced ontology with Dublin Core metadata and inverse properties"`
- `"Updated technical report with testing results"`
- `"Fixed cardinality constraints in SecurityEvent class"`

❌ **Bad Examples:**
- `"Update"`
- `"Fix stuff"`
- `"asdf"`
- `"Final version 3 final FINAL"`

---

## File Structure on GitHub

Your repository will look like this:

```
cybersecurity-ontology-cw2/
├── .gitignore
├── README.md
├── INDEX.md
├── CybersecurityOntology_ENHANCED.owl
├── CybersecurityOntology_SWRL_Rules.swrl
├── TECHNICAL_REPORT_Ontology_Enhancement.md
├── SWRL_REASONING_GUIDE.md
├── PRODUCTION_SYSTEM_FEATURES.md
└── [optional development files]
```

---

## Tips for Academic Projects

1. **Commit Often**: Make commits after completing each major task
2. **Descriptive Messages**: Explain what changed and why
3. **Branch Strategy**: Consider creating branches for experiments
4. **Tag Releases**: Tag your final submission version:
   ```bash
   git tag -a v2.0 -m "Final submission version"
   git push origin v2.0
   ```

---

## Troubleshooting

### Problem: "remote origin already exists"
```bash
git remote remove origin
git remote add origin https://github.com/YOUR_USERNAME/repo.git
```

### Problem: "failed to push some refs"
```bash
# Pull first, then push
git pull origin main --rebase
git push
```

### Problem: "Authentication failed"
- Ensure you're using a Personal Access Token, not your password
- Check token hasn't expired
- Verify token has `repo` scope

### Problem: "Large file warning"
- GitHub has 100MB file size limit
- Your .owl file (533KB) is fine
- If you have larger files, consider Git LFS

---

## Next Steps

After pushing to GitHub:
1. ✅ Verify all files are visible on GitHub
2. ✅ Check README.md displays correctly
3. ✅ Add repository URL to your coursework submission
4. ✅ Consider making repository public if sharing with instructor
5. ✅ Add collaborators if working in a team

---

## Support Resources

- **Git Documentation**: https://git-scm.com/doc
- **GitHub Guides**: https://guides.github.com/
- **Git Cheat Sheet**: https://education.github.com/git-cheat-sheet-education.pdf

---

**Good luck with your submission! 🎓**
