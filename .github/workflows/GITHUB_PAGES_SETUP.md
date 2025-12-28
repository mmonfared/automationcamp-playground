# GitHub Pages Deployment Setup Guide

This guide will help you deploy your Angular app to GitHub Pages using the automated workflow.

## 📋 Prerequisites

Before the workflow can deploy your app, you need to configure GitHub Pages in your repository settings.

## 🔧 Setup Steps

### 1. Enable GitHub Pages

1. Go to your GitHub repository
2. Click on **Settings** tab
3. In the left sidebar, click on **Pages**
4. Under **Build and deployment**, set:
   - **Source**: `GitHub Actions` (not "Deploy from a branch")

### 2. Push Your Code

Once you've committed the workflow file, push it to your repository:

```bash
git add .github/workflows/deploy-to-github-pages.yml
git commit -m "Add GitHub Pages deployment workflow"
git push origin main
```

### 3. Monitor the Deployment

1. Go to the **Actions** tab in your GitHub repository
2. You should see the "Deploy to GitHub Pages" workflow running
3. Once it completes successfully (green checkmark), your site will be live!

### 4. Access Your Site

Your site will be available at:
```
https://<your-username>.github.io/<repository-name>/
```

For example: `https://johndoe.github.io/my-angular-app/`

## 🚀 Workflow Features

The workflow includes:

- ✅ **Automatic deployment** on push to `main` branch
- ✅ **Manual deployment** option via workflow_dispatch
- ✅ **Concurrent deployment protection** to prevent conflicts
- ✅ **Optimized builds** using Angular production configuration
- ✅ **Caching** for faster builds using npm cache

## 🔄 Triggering Deployments

### Automatic Trigger
Push any changes to the `main` branch:
```bash
git push origin main
```

### Manual Trigger
1. Go to **Actions** tab
2. Select "Deploy to GitHub Pages" workflow
3. Click **Run workflow** button
4. Select the branch and click **Run workflow**

## ⚙️ Configuration Options

### Change Target Branch

To deploy from a different branch, edit `.github/workflows/deploy-to-github-pages.yml`:

```yaml
on:
  push:
    branches:
      - develop  # Change 'main' to your preferred branch
```

### Change Node.js Version

To use a different Node.js version, update the workflow:

```yaml
- name: Setup Node.js
  uses: actions/setup-node@v4
  with:
    node-version: '20'  # Change to desired version
```

### Custom Build Output Path

If your Angular build outputs to a different directory, update:

```yaml
- name: Upload artifact
  uses: actions/upload-pages-artifact@v3
  with:
    path: './dist/my-custom-path'  # Update path here
```

## 🐛 Troubleshooting

### Workflow Fails on Build Step
- Check that all dependencies are listed in `package.json`
- Ensure `build:prod` script exists and works locally
- Review the workflow logs in the Actions tab

### Site Shows 404 Errors
- Make sure GitHub Pages is configured to use "GitHub Actions" as source
- Check that the build output path is correct in the workflow
- Wait a few minutes for DNS propagation

### Assets Not Loading
- Verify that Angular base href is configured correctly
- You may need to add `--base-href=/repository-name/` to your build command

## 📚 Additional Resources

- [GitHub Pages Documentation](https://docs.github.com/en/pages)
- [GitHub Actions Documentation](https://docs.github.com/en/actions)
- [Angular Deployment Guide](https://angular.io/guide/deployment)

