# Complete Guide: GitHub Pages Setup, Build, Deploy & Go Live

This guide walks you through every step needed to create a GitHub Pages site, push to GitHub, build, and deploy it live.

---

## PHASE 1: Setup & Repository Configuration

### Step 1: Clone Your Repository Locally
```bash
git clone https://github.com/saaysalim/TestRepo.git
cd TestRepo
```

### Step 2: Verify Git Configuration
```bash
git config user.name "Your Name"
git config user.email "your.email@github.com"
```

### Step 3: Create Initial Content Structure
Create this directory structure:
```
TestRepo/
├── docs/
│   ├── index.md
│   ├── getting-started.md
│   ├── cicd.md
│   └── api-reference.md
├── src/
│   └── pages/
├── .github/
│   └── workflows/
├── package.json
├── README.md
└── _config.yml (GitHub Pages config)
```

### Step 4: Create _config.yml for GitHub Pages
In root directory, create `_config.yml`:
```yaml
# GitHub Pages Configuration
title: TestRepo
description: A modern CI/CD pipeline project with GitHub Pages
theme: jekyll-theme-minimal
baseurl: "/TestRepo"
url: "https://saaysalim.github.io/TestRepo"

# Jekyll settings
markdown: kramdown
sass:
  sass_dir: _sass
permalink: /:year/:month/:day/:title/

# Collections
collections:
  docs:
    output: true
    permalink: /docs/:path/

# Exclude from build
exclude:
  - node_modules/
  - dist/
  - .env
  - package-lock.json
```

---

## PHASE 2: Create Initial Pages & Content

### Step 5: Create Landing Page (docs/index.md)
```markdown
# Welcome to TestRepo

**A modern project with CI/CD pipeline and GitHub Pages**

## Quick Links
- [Getting Started](./getting-started.md)
- [CI/CD Pipeline](./cicd.md)
- [API Reference](./api-reference.md)
- [GitHub Repository](https://github.com/saaysalim/TestRepo)

## Features
- ✅ Automated CI/CD Pipeline
- 📄 GitHub Pages Documentation
- 🚀 One-Click Deployment
- 📊 Comprehensive Documentation

---
*Last Updated: November 16, 2026*
```

### Step 6: Verify Existing Documentation Pages
Check these files exist in `docs/`:
- `getting-started.md` ✓
- `cicd.md` ✓
- `api-reference.md` ✓

### Step 7: Create CONTRIBUTING.md
```markdown
# Contributing Guidelines

Thank you for your interest in contributing!

## How to Contribute

1. Fork the repository
2. Create a feature branch: `git checkout -b feature/my-feature`
3. Make your changes
4. Push to your fork: `git push origin feature/my-feature`
5. Submit a Pull Request

## Code Standards
- Use TypeScript
- Write tests for new features
- Follow ESLint rules
- Update documentation

## Questions?
Open an issue or discussion!
```

### Step 8: Create LICENSE File
```
MIT License

Copyright (c) 2026 Salim Saay

Permission is hereby granted, free of charge...
```

---

## PHASE 3: Push Content to GitHub

### Step 9: Stage All Files
```bash
# Navigate to repo
cd C:\temp\TestRepo

# Stage all files
git add .

# Verify staged files
git status
```

### Step 10: Create Initial Commit
```bash
git commit -m "Initial commit: Add documentation and CI/CD pipeline

- Add comprehensive documentation
- Add GitHub Actions CI/CD workflow
- Add GitHub Pages configuration
- Add contributing guidelines
- Add project structure

Co-authored-by: Copilot <223556219+Copilot@users.noreply.github.com>"
```

### Step 11: Push to GitHub
```bash
# Push to main branch
git push origin main

# Verify push
git log --oneline -5
```

**Expected Output:**
```
✓ All changes pushed to GitHub
✓ Files visible on github.com/saaysalim/TestRepo
```

---

## PHASE 4: Configure GitHub Pages

### Step 12: Enable GitHub Pages in Repository Settings

**On GitHub.com:**

1. Go to: `https://github.com/saaysalim/TestRepo/settings`
2. Find: **"Pages"** in left sidebar (under Code and automation)
3. Under **"Build and deployment"**:
   - **Source**: Select `Deploy from a branch`
   - **Branch**: Select `main`
   - **Folder**: Select `/ (root)` or `/docs`
   - Click **Save**

4. GitHub will show:
   ```
   Your site is live at: https://saaysalim.github.io/TestRepo
   ```

### Step 13: Wait for Deployment
- GitHub automatically builds your site (1-2 minutes)
- Check the **Deployments** tab on GitHub
- You should see a successful deployment

---

## PHASE 5: Setup GitHub Actions Workflow

### Step 14: Create GitHub Pages Build Workflow

Create: `.github/workflows/pages.yml`

```yaml
name: Build and Deploy GitHub Pages

on:
  push:
    branches: [ main, develop ]
  pull_request:
    branches: [ main ]
  workflow_dispatch:

permissions:
  contents: read
  pages: write
  id-token: write

concurrency:
  group: "pages"
  cancel-in-progress: false

jobs:
  build:
    runs-on: ubuntu-latest
    
    steps:
      - name: Checkout code
        uses: actions/checkout@v3
      
      - name: Setup Ruby
        uses: ruby/setup-ruby@v1
        with:
          ruby-version: '3.1'
          bundler-cache: true
      
      - name: Setup Pages
        uses: actions/configure-pages@v3
      
      - name: Build with Jekyll
        uses: actions/jekyll-build-pages@v1
        with:
          source: ./
          destination: ./_site
      
      - name: Upload artifact
        uses: actions/upload-pages-artifact@v1
        with:
          path: './_site'

  deploy:
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    
    runs-on: ubuntu-latest
    needs: build
    
    steps:
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v2
      
      - name: Deployment Success
        run: echo "✅ GitHub Pages deployed successfully!"
```

### Step 15: Commit and Push Workflow File
```bash
git add .github/workflows/pages.yml
git commit -m "ci: Add GitHub Pages build and deploy workflow"
git push origin main
```

---

## PHASE 6: Verification & Testing

### Step 16: Verify Workflow Execution

**On GitHub.com:**

1. Go to: **Actions** tab
2. Find: `Build and Deploy GitHub Pages` workflow
3. Watch it run (should take 1-3 minutes)
4. Check for ✅ **All green checkmarks**

**Expected workflow status:**
```
✅ build — Build with Jekyll
✅ deploy — Deploy to GitHub Pages
```

### Step 17: Check Deployment Details

1. Go to: **Deployments** (in repo main page)
2. Find latest deployment
3. Click: **View deployment**
4. Should open: `https://saaysalim.github.io/TestRepo`

### Step 18: Test the Live Site

**Visit your site:**
```
https://saaysalim.github.io/TestRepo
```

**You should see:**
- ✅ Homepage (Welcome to TestRepo)
- ✅ Getting Started page
- ✅ CI/CD Documentation
- ✅ API Reference
- ✅ Navigation links work

---

## PHASE 7: Custom Domain (Optional)

### Step 19: Add Custom Domain (If Available)

**To use custom domain like `testrepo.com`:**

1. Go to **Settings → Pages**
2. Under **Custom domain**, enter: `testrepo.com`
3. Add DNS records to your domain registrar:
   ```
   A record: 185.199.108.153
   A record: 185.199.109.153
   A record: 185.199.110.153
   A record: 185.199.111.153
   
   CNAME record: saaysalim.github.io
   ```
4. Wait 24 hours for DNS propagation
5. Click **Enforce HTTPS** checkbox

---

## PHASE 8: Continuous Updates

### Step 20: Making Changes to Your Site

**To update content:**

1. Edit files in `/docs` or `/src`
2. Test locally (if needed)
3. Commit and push:
   ```bash
   git add .
   git commit -m "docs: Update documentation"
   git push origin main
   ```
4. GitHub Actions automatically:
   - Rebuilds your site
   - Deploys to GitHub Pages
   - Updates live site (1-2 minutes)

### Step 21: Monitor Build Status

**Always check:**
1. **Actions** tab for build status
2. **Deployments** for deployment history
3. Live site for changes

---

## TROUBLESHOOTING

### Issue: GitHub Pages Not Building

**Solution:**
```bash
# 1. Check workflow file syntax
# 2. Verify branch protection rules
# 3. Check GitHub Pages settings
# 4. Look at workflow logs

# View logs on: Actions → Workflow name → Latest run
```

### Issue: Site Not Live After Push

**Solutions:**
1. Wait 2-3 minutes for GitHub Actions
2. Clear browser cache: `Ctrl+Shift+Delete`
3. Check **Actions** tab for failures
4. Verify **Pages** settings show build successful

### Issue: 404 on GitHub Pages

**Check:**
1. Files exist in `/docs` or root
2. `_config.yml` has correct `baseurl`
3. Filenames are correct (case-sensitive)
4. Jekyll rebuilt successfully

### Issue: Links Not Working

**Fix:**
1. Use relative paths: `./file.md`
2. Update baseurl in `_config.yml`
3. Use `{{ site.baseurl }}/path` in templates

---

## QUICK REFERENCE CHECKLIST

- [ ] Step 1: Clone repository
- [ ] Step 2: Configure git
- [ ] Step 3-4: Create structure & _config.yml
- [ ] Step 5-8: Create content pages
- [ ] Step 9-11: Commit & push to GitHub
- [ ] Step 12-13: Enable GitHub Pages
- [ ] Step 14-15: Setup workflow
- [ ] Step 16-18: Verify & test
- [ ] Step 19: (Optional) Add custom domain
- [ ] Step 20-21: Setup continuous updates

---

## FINAL VERIFICATION

✅ **Your site is LIVE when:**
1. `https://saaysalim.github.io/TestRepo` loads
2. Navigation works
3. All pages display correctly
4. Workflow shows green checkmarks
5. No 404 errors

---

**Congratulations! Your GitHub Pages site is live! 🎉**

For questions, see: [GitHub Pages Documentation](https://pages.github.com/)

