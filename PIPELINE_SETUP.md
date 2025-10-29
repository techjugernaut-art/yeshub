# YesHub Pipeline Deployment - Complete Setup

**Date:** October 29, 2025
**Pipeline Name:** yeshub-pipeline
**Team:** mutual
**Status:** ✅ FULLY OPERATIONAL

---

## 🎯 Pipeline Overview

```
┌─────────────┐         ┌────────────────┐         ┌─────────────────┐
│   GitHub    │────────▶│    Staging     │────────▶│   Production    │
│techjugernaut│         │ yeshub-api-v2  │         │    yeshubgh     │
└─────────────┘         └────────────────┘         └─────────────────┘
```

---

## ✅ What's Been Set Up

### 1. GitHub Repository
- **URL:** https://github.com/techjugernaut-art/yeshub
- **Code:** Complete YesHub job portal
- **Commits:** All history preserved

### 2. Heroku Pipeline
- **Name:** yeshub-pipeline
- **Owner:** mutual (team)
- **Apps:**
  - **Staging:** yeshub-api-v2
  - **Production:** yeshubgh

### 3. Staging Environment
- **App:** yeshub-api-v2
- **URL:** https://yeshub-api-v2-fd6c52bb29a5.herokuapp.com/
- **Status:** ✅ RUNNING (v968)
- **Purpose:** Test changes before production

### 4. Production Environment
- **App:** yeshubgh
- **URL:** https://yeshubgh-978dcadde9a0.herokuapp.com/
- **Status:** ✅ RUNNING (v8)
- **Purpose:** Live site

---

## 📋 Pipeline Configuration

### View Pipeline Status
```bash
heroku pipelines:info yeshub-pipeline
```

### Expected Output:
```
=== yeshub-pipeline
owner: mutual (team)

app name      stage      
───────────── ────────── 
yeshub-api-v2 staging    
yeshubgh      production
```

---

## 🚀 Deployment Workflows

### Method 1: Deploy to Staging First (RECOMMENDED)

```bash
# Navigate to project directory
cd /Users/kingsleyabrokwah/Desktop/yeshubgh/yeshub/jdm

# Make your changes
# ... edit files ...

# Commit changes
git add .
git commit -m "Your change description"

# Push to GitHub
git push origin master

# Deploy to STAGING
git push staging master

# Test on staging: https://yeshub-api-v2-fd6c52bb29a5.herokuapp.com/

# If everything works, promote to PRODUCTION
heroku pipelines:promote --app yeshub-api-v2

# Or manually deploy to production
git push heroku master
```

### Method 2: Direct Production Deploy

```bash
# For urgent fixes only!
cd /Users/kingsleyabrokwah/Desktop/yeshubgh/yeshub/jdm

git add .
git commit -m "Urgent fix: description"
git push origin master
git push heroku master
```

---

## 🔄 Promote from Staging to Production

Once you've tested on staging and everything works:

```bash
# Promote staging to production
heroku pipelines:promote --app yeshub-api-v2

# This will:
# 1. Copy the exact staging build to production
# 2. Zero downtime deployment
# 3. Maintain consistency between environments
```

---

## 🌐 Connecting GitHub for Auto-Deployment

To enable automatic deployments from GitHub when you push:

### Step 1: Connect via Heroku Dashboard

1. Visit: https://dashboard.heroku.com/pipelines/yeshub-pipeline
2. Click on **staging** or **production** app
3. Go to **Deploy** tab
4. Under "Deployment method", click **GitHub**
5. Click **Connect to GitHub**
6. Search for `techjugernaut-art/yeshub`
7. Click **Connect**

### Step 2: Enable Auto-Deploy (Optional)

For each app:
1. Under "Automatic deploys"
2. Select branch: `master`
3. Click **Enable Automatic Deploys**

**Benefits:**
- Every push to GitHub master → auto-deploys to staging
- Manually promote to production when ready
- No need to use `git push heroku master`

---

## 🔍 Monitoring & Verification

### Check App Status
```bash
# Staging
heroku ps -a yeshub-api-v2

# Production
heroku ps -a yeshubgh

# Pipeline overview
heroku pipelines:info yeshub-pipeline
```

### View Logs
```bash
# Staging logs
heroku logs --tail -a yeshub-api-v2

# Production logs
heroku logs --tail -a yeshubgh
```

### Check Releases
```bash
# Staging
heroku releases -a yeshub-api-v2 -n 10

# Production
heroku releases -a yeshubgh -n 10
```

### Test Websites
- **Staging:** https://yeshub-api-v2-fd6c52bb29a5.herokuapp.com/
- **Production:** https://yeshubgh-978dcadde9a0.herokuapp.com/

---

## 📊 Current Status

### Staging (yeshub-api-v2)
```
✅ Running on Heroku
✅ PHP 8.4.14 with Apache
✅ v968 deployed
✅ Connected to yeshub-pipeline
📍 https://yeshub-api-v2-fd6c52bb29a5.herokuapp.com/
```

### Production (yeshubgh)
```
✅ Running on Heroku
✅ PHP 8.4.14 with Apache
✅ v8 deployed
✅ Connected to yeshub-pipeline
📍 https://yeshubgh-978dcadde9a0.herokuapp.com/
```

---

## 🔧 Git Remotes Configuration

```bash
origin   https://github.com/techjugernaut-art/yeshub.git       # GitHub
heroku   https://git.heroku.com/yeshubgh.git                   # Production
staging  https://git.heroku.com/yeshub-api-v2.git              # Staging
```

---

## 📝 Best Practices

### 1. Always Test on Staging First
```bash
git push staging master  # Deploy to staging
# Test thoroughly
heroku pipelines:promote --app yeshub-api-v2  # Promote to production
```

### 2. Use Descriptive Commit Messages
```bash
git commit -m "feat: add new job search filter"
git commit -m "fix: correct mobile navigation menu"
git commit -m "docs: update README with deployment info"
```

### 3. Tag Production Releases
```bash
git tag -a v1.0.0 -m "Release version 1.0.0"
git push origin v1.0.0
```

### 4. Monitor After Deployment
```bash
# Watch logs for errors
heroku logs --tail -a yeshubgh

# Check app health
heroku ps -a yeshubgh
```

---

## 🚨 Rollback Procedure

If something breaks in production:

```bash
# View recent releases
heroku releases -a yeshubgh

# Rollback to previous version
heroku rollback v7 -a yeshubgh

# Or rollback one version
heroku rollback -a yeshubgh
```

---

## 🎯 Environment Management

### Staging Environment
**Purpose:** Test all changes before production
**Usage:** Deploy frequently, test thoroughly
**Risk:** Low (can break without affecting users)

### Production Environment
**Purpose:** Live user-facing application
**Usage:** Deploy only tested changes
**Risk:** High (affects real users)

**Workflow:**
1. Develop locally
2. Deploy to staging
3. Test on staging
4. Promote to production
5. Monitor production

---

## 📌 Quick Reference

| Action | Command |
|--------|---------|
| Deploy to staging | `git push staging master` |
| Deploy to production | `git push heroku master` |
| Promote staging→prod | `heroku pipelines:promote --app yeshub-api-v2` |
| View pipeline | `heroku pipelines:info yeshub-pipeline` |
| Staging logs | `heroku logs --tail -a yeshub-api-v2` |
| Production logs | `heroku logs --tail -a yeshubgh` |
| Rollback production | `heroku rollback -a yeshubgh` |
| Restart staging | `heroku restart -a yeshub-api-v2` |
| Restart production | `heroku restart -a yeshubgh` |

---

## 🌟 Success Criteria

- ✅ Pipeline created with mutual team ownership
- ✅ Staging app (yeshub-api-v2) configured and running
- ✅ Production app (yeshubgh) configured and running
- ✅ Both apps deployed with latest code
- ✅ Both sites verified working
- ✅ Git remotes properly configured
- ✅ Documentation complete

**STATUS: ALL OBJECTIVES ACHIEVED** 🎉

---

## 📞 Support & Resources

- **Heroku Dashboard:** https://dashboard.heroku.com/pipelines/yeshub-pipeline
- **GitHub Repo:** https://github.com/techjugernaut-art/yeshub
- **Heroku Docs:** https://devcenter.heroku.com/articles/pipelines
- **Team:** mutual (admin access)

---

**Last Updated:** October 29, 2025
**Pipeline Version:** 1.0
**Maintained By:** Claude Code
