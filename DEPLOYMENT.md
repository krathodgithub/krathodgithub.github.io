# Deployment Guide for kaushikrathod.com

This guide will help you deploy your portfolio to your custom domain using GitHub Actions and GitHub Pages.

## 📋 Prerequisites

- GitHub account
- Access to your domain registrar (where you bought kaushikrathod.com)
- EmailJS account credentials

## 🚀 Step 1: Push to GitHub

1. **Create a new repository on GitHub**:
   - Go to https://github.com/new
   - Repository name: `portfolio` (or any name you prefer)
   - Visibility: Public (required for free GitHub Pages)
   - Don't initialize with README, .gitignore, or license
   - Click "Create repository"

2. **Push your code** (run these commands):
   ```bash
   git remote add origin https://github.com/krathodgithub/portfolio.git
   git branch -M main
   git push -u origin main
   ```

## ⚙️ Step 2: Configure GitHub Repository

### Enable GitHub Pages

1. Go to your repository on GitHub
2. Click **Settings** (top right)
3. In the left sidebar, click **Pages**
4. Under "Build and deployment":
   - **Source**: Select "GitHub Actions"
5. Leave the page open - you'll come back to it

### Add EmailJS Secrets

1. In your repository settings, click **Secrets and variables** → **Actions**
2. Click **New repository secret**
3. Add these three secrets:

   **Secret 1:**
   - Name: `VITE_EMAILJS_SERVICE_ID`
   - Value: Your EmailJS service ID (from EmailJS dashboard)

   **Secret 2:**
   - Name: `VITE_EMAILJS_TEMPLATE_ID`
   - Value: Your EmailJS template ID

   **Secret 3:**
   - Name: `VITE_EMAILJS_PUBLIC_KEY`
   - Value: Your EmailJS public key

   Click "Add secret" for each one.

## 🌐 Step 3: Configure Your Domain (kaushikrathod.com)

### A. Add DNS Records

Log in to your domain registrar (GoDaddy, Namecheap, Cloudflare, etc.) and add these DNS records:

**For Apex Domain (kaushikrathod.com):**

Add these 4 **A records**:
```
Type: A
Name: @ (or leave blank for root domain)
Value: 185.199.108.153

Type: A
Name: @
Value: 185.199.109.153

Type: A
Name: @
Value: 185.199.110.153

Type: A
Name: @
Value: 185.199.111.153
```

**For WWW subdomain (optional but recommended):**

Add a **CNAME record**:
```
Type: CNAME
Name: www
Value: krathodgithub.github.io
```

**Important:** DNS changes can take 24-48 hours to propagate, but usually happen within 1-2 hours.

### B. Verify Custom Domain in GitHub

1. Go back to your repository **Settings** → **Pages**
2. Under "Custom domain", enter: `kaushikrathod.com`
3. Click **Save**
4. Wait for DNS check to complete (green checkmark)
5. Once verified, check **Enforce HTTPS** (wait a few minutes if it's not available yet)

## 🔄 Step 4: Deploy

Your site will automatically deploy when you push to the main branch!

**To trigger the first deployment:**
```bash
git push origin main
```

**To check deployment status:**
1. Go to your repository on GitHub
2. Click the **Actions** tab
3. You'll see the "Deploy to GitHub Pages" workflow running
4. Wait for it to complete (green checkmark)

## ✅ Step 5: Verify Deployment

1. **Wait for DNS propagation** (can take 1-2 hours)
2. Visit: https://kaushikrathod.com
3. Your portfolio should be live!

## 🔧 Troubleshooting

### DNS Not Working Yet
- DNS changes take time (up to 48 hours, usually 1-2 hours)
- Check DNS propagation: https://www.whatsmydns.net/#A/kaushikrathod.com
- Make sure all 4 A records are added correctly

### GitHub Pages Not Deploying
- Check **Actions** tab for error messages
- Make sure repository is **Public** (required for free GitHub Pages)
- Verify GitHub Pages is set to "GitHub Actions" as source

### HTTPS Certificate Pending
- Wait 10-15 minutes after DNS verification
- GitHub automatically provisions HTTPS certificate
- Don't check "Enforce HTTPS" until certificate is ready

### Contact Form Not Working
- Make sure you added all 3 EmailJS secrets in repository settings
- Check secret names match exactly (case-sensitive)
- Verify EmailJS service is configured and active

### Build Failing
- Check the Actions tab for specific error messages
- Most common: Missing EmailJS secrets
- Solution: Add the secrets as described in Step 2

## 📝 Future Updates

Every time you push to the main branch, GitHub Actions will automatically:
1. Build your portfolio
2. Deploy to GitHub Pages
3. Update kaushikrathod.com

To update your portfolio:
```bash
# Make your changes
git add .
git commit -m "Your commit message"
git push origin main
```

## 🎉 Success!

Your portfolio should now be live at:
- 🌐 **https://kaushikrathod.com**
- 🌐 **https://www.kaushikrathod.com** (if you added CNAME)

---

## Quick Reference

**Your GitHub Repo:** https://github.com/krathodgithub/portfolio

**GitHub Pages Settings:** https://github.com/krathodgithub/portfolio/settings/pages

**GitHub Actions:** https://github.com/krathodgithub/portfolio/actions

**DNS Check Tool:** https://www.whatsmydns.net

---

Need help? Check the GitHub Actions logs in the Actions tab for detailed error messages.
