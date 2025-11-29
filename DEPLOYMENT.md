# Deploying Trysti.com to GitHub Pages with Custom Domain and HTTPS

This guide will walk you through deploying your website to GitHub Pages with a custom domain and free HTTPS.

## Step 1: Create GitHub Repository

1. Go to [GitHub](https://github.com) and sign in
2. Click the "+" icon in the top right and select "New repository"
3. Name your repository (e.g., `trysti-website` or `trysti.com`)
4. Make it **Public** (required for free GitHub Pages)
5. Click "Create repository"

## Step 2: Push Your Code to GitHub

Open a terminal in your project folder and run:

```bash
# Initialize git repository
git init

# Add all files
git add .

# Commit your files
git commit -m "Initial commit - Trysti website"

# Add your GitHub repository as remote (replace with your repository URL)
git remote add origin https://github.com/YOUR-USERNAME/YOUR-REPO-NAME.git

# Push to GitHub
git branch -M main
git push -u origin main
```

## Step 3: Enable GitHub Pages

1. Go to your repository on GitHub
2. Click **Settings** (top right)
3. In the left sidebar, click **Pages**
4. Under "Source", select **main** branch and **/ (root)** folder
5. Click **Save**
6. GitHub will provide a URL like `https://YOUR-USERNAME.github.io/YOUR-REPO-NAME/`

## Step 4: Configure Custom Domain (trysti.com)

### A. Add CNAME file to your repository

Create a file named `CNAME` (no extension) in your project root with just your domain:

```
trysti.com
```

Then push it to GitHub:

```bash
git add CNAME
git commit -m "Add CNAME for custom domain"
git push
```

### B. Configure DNS Settings

Go to your domain registrar where you bought trysti.com and add these DNS records:

**For root domain (trysti.com):**

Add these **A records** pointing to GitHub's IP addresses:
```
Type: A
Name: @
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

**For www subdomain (www.trysti.com):**

Add a **CNAME record**:
```
Type: CNAME
Name: www
Value: YOUR-USERNAME.github.io
```

**Note:** DNS changes can take up to 48 hours to propagate, but usually take 15-30 minutes.

### C. Configure Custom Domain in GitHub

1. Go to your repository **Settings** → **Pages**
2. Under "Custom domain", enter: `trysti.com`
3. Click **Save**
4. GitHub will check your DNS configuration

## Step 5: Enable HTTPS (FREE!)

**YES, HTTPS is completely FREE with GitHub Pages!**

1. In **Settings** → **Pages**, wait for DNS check to complete (may take a few minutes)
2. Once DNS is verified, you'll see a checkbox: **"Enforce HTTPS"**
3. Check this box to enable HTTPS
4. GitHub automatically provisions a free SSL certificate through Let's Encrypt
5. Your site will now be accessible via `https://trysti.com`

**Important:** 
- The HTTPS option may take up to 24 hours to become available after DNS configuration
- Once enabled, GitHub automatically renews the SSL certificate

## Step 6: Verify Your Website

After DNS propagates and HTTPS is enabled, visit:
- https://trysti.com
- https://www.trysti.com

Both should work with a valid SSL certificate (padlock icon in browser)!

## Updating Your Website

Whenever you make changes:

```bash
# Make your changes to HTML, CSS, or JS files

# Stage changes
git add .

# Commit changes
git commit -m "Description of your changes"

# Push to GitHub
git push

# GitHub Pages will automatically rebuild and deploy (takes 1-2 minutes)
```

## Troubleshooting

### DNS not working
- Check DNS propagation: https://dnschecker.org
- Verify A records are correct
- Some registrars may take longer to update

### HTTPS not available
- Wait 24 hours after DNS configuration
- Ensure DNS is fully propagated
- Uncheck and re-check "Enforce HTTPS" in GitHub settings

### 404 Error
- Ensure your main file is named `index.html` (lowercase)
- Verify CNAME file contains only your domain (no http:// or trailing slash)
- Check that GitHub Pages is enabled and building from the correct branch

### Page not updating
- Clear browser cache (Ctrl+Shift+R or Cmd+Shift+R)
- Wait 1-2 minutes for GitHub Pages to rebuild
- Check the Actions tab in GitHub to see build status

## Additional Configuration

### Redirect www to root domain (optional)
Your DNS CNAME for www already handles this. GitHub Pages will serve content at both.

### Custom 404 page
Create a `404.html` file in your root directory with custom error page styling.

### Analytics
Add Google Analytics or other analytics by inserting the tracking code in the `<head>` section of `index.html`.

## Cost Breakdown

✅ **GitHub Pages hosting**: FREE
✅ **HTTPS/SSL Certificate**: FREE (auto-renewed)
✅ **Bandwidth**: FREE (unlimited for normal traffic)
✅ **Build/Deploy**: FREE (automatic)

💰 **Domain name (trysti.com)**: $10-15/year (your only cost!)

## Support

For GitHub Pages issues, check:
- [GitHub Pages Documentation](https://docs.github.com/en/pages)
- [GitHub Pages Status](https://www.githubstatus.com/)

---

**Your website is now live with free HTTPS! 🎉**
