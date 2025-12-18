# Git Setup Instructions

Follow these steps to push your WASP-39b project to GitHub.

## Prerequisites

1. **Install Git** (if not already installed):
   - Windows: Download from https://git-scm.com/download/win
   - Mac: `brew install git` or download from https://git-scm.com/download/mac
   - Linux: `sudo apt-get install git` (Ubuntu/Debian) or `sudo yum install git` (RedHat/CentOS)

2. **Create a GitHub account** (if you don't have one):
   - Go to https://github.com
   - Sign up for free

3. **Configure Git** (first time only):
   ```bash
   git config --global user.name "Your Name"
   git config --global user.email "your.email@example.com"
   ```

## Step-by-Step Guide

### Step 1: Create a New Repository on GitHub

1. Go to https://github.com
2. Click the **"+"** icon (top right) → **"New repository"**
3. Fill in:
   - **Repository name**: `wasp39b-atmospheric-analysis`
   - **Description**: "Spectroscopic analysis of WASP-39b exoplanet using JWST data with MCMC parameter estimation"
   - **Public** or **Private**: Choose based on preference (Public recommended for portfolio)
   - **DO NOT** initialize with README, .gitignore, or license (we already have these)
4. Click **"Create repository"**

### Step 2: Initialize Local Git Repository

Open your terminal/command prompt and navigate to your project directory:

```bash
# Navigate to the project folder
cd path/to/wasp39b-atmospheric-analysis

# Initialize git repository
git init

# Add all files to staging
git add .

# Commit the files
git commit -m "Initial commit: WASP-39b atmospheric analysis project"
```

### Step 3: Connect to GitHub and Push

Replace `YOUR_USERNAME` with your actual GitHub username:

```bash
# Add the remote repository
git remote add origin https://github.com/YOUR_USERNAME/wasp39b-atmospheric-analysis.git

# Verify the remote was added
git remote -v

# Push to GitHub (first time)
git push -u origin main
```

**Note:** If you get an error about "master" vs "main" branch, try:
```bash
git branch -M main
git push -u origin main
```

### Step 4: Verify on GitHub

1. Go to your GitHub repository: `https://github.com/YOUR_USERNAME/wasp39b-atmospheric-analysis`
2. Verify all files are present (except .fits files, which are ignored)

## Updating Your Repository Later

After making changes to your code:

```bash
# Check what changed
git status

# Add changed files
git add .

# Commit with a descriptive message
git commit -m "Description of what you changed"

# Push to GitHub
git push
```

## Common Git Commands

```bash
# Check repository status
git status

# View commit history
git log

# Create a new branch
git checkout -b feature-name

# Switch between branches
git checkout branch-name

# Pull latest changes from GitHub
git pull

# See differences in files
git diff
```

## Troubleshooting

### Problem: "Permission denied (publickey)"

**Solution:** Set up SSH keys or use HTTPS with personal access token.

For HTTPS with token:
1. Go to GitHub → Settings → Developer settings → Personal access tokens
2. Generate new token (classic)
3. Copy the token
4. When pushing, use: `https://YOUR_TOKEN@github.com/YOUR_USERNAME/repo.git`

### Problem: "! [rejected] master -> master (fetch first)"

**Solution:** Someone else pushed changes. Pull first:
```bash
git pull origin main --rebase
git push
```

### Problem: Large files won't push

**Solution:** FITS files are already in .gitignore. If you accidentally added them:
```bash
git rm --cached data/*.fits
git commit -m "Remove large FITS files"
git push
```

## Best Practices

1. **Commit often** with clear messages
2. **Never commit large data files** (already handled by .gitignore)
3. **Write meaningful commit messages**: "Fixed MCMC convergence issue" not "Fixed stuff"
4. **Keep README updated** as you improve the project
5. **Use branches** for experimental features

## Making Your Repository Stand Out

After pushing, enhance your GitHub repo:

1. **Add Topics/Tags**: 
   - Go to repo → About (right side) → Settings icon
   - Add: `exoplanets`, `jwst`, `astropy`, `mcmc`, `bayesian-inference`, `spectroscopy`

2. **Pin the Repository**:
   - Go to your GitHub profile
   - Click "Customize your pins"
   - Select this repository

3. **Add a License** (optional):
   - Create a new file: LICENSE
   - Choose MIT, Apache 2.0, or GPL v3

4. **Enable GitHub Pages** (if you want to showcase visualizations)

## Next Steps

After pushing to GitHub:

1. ✅ Add your GitHub repo link to your resume
2. ✅ Include it in your LinkedIn projects section
3. ✅ Consider writing a blog post about the analysis
4. ✅ Add sample output plots to the README

## Resources

- [Git Documentation](https://git-scm.com/doc)
- [GitHub Guides](https://guides.github.com/)
- [Git Cheat Sheet](https://education.github.com/git-cheat-sheet-education.pdf)

---

**Quick Reference Card:**

```bash
# First time setup
git init
git add .
git commit -m "Initial commit"
git remote add origin https://github.com/USERNAME/REPO.git
git push -u origin main

# Regular updates
git add .
git commit -m "Your message"
git push
```

Good luck with your portfolio! 🚀
