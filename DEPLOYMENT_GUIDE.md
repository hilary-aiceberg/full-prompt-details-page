# GitHub Pages Deployment Guide for AIceberg App

## Step 1: Update package.json

Open `package.json` and add the `homepage` field right after `"private": true,`:

```json
{
  "name": "aiceberg-app",
  "version": "0.1.0",
  "private": true,
  "homepage": "https://YOUR-GITHUB-USERNAME.github.io/YOUR-REPO-NAME",
  "dependencies": {
    ...
```

Replace:
- `YOUR-GITHUB-USERNAME` with your actual GitHub username
- `YOUR-REPO-NAME` with your repository name

## Step 2: Add deployment scripts to package.json

Add these two scripts to the `"scripts"` section in package.json:

```json
"scripts": {
  "start": "react-scripts start",
  "build": "react-scripts build",
  "test": "react-scripts test",
  "eject": "react-scripts eject",
  "predeploy": "npm run build",
  "deploy": "gh-pages -d build"
},
```

## Step 3: Initialize Git repository (if not already done)

```bash
cd aiceberg-app
git init
git add .
git commit -m "Initial commit"
```

## Step 4: Create GitHub repository and push

1. Go to GitHub and create a new repository
2. **Important:** Don't initialize with README, .gitignore, or license (we already have files)
3. Copy the repository URL
4. Run these commands:

```bash
git remote add origin https://github.com/YOUR-USERNAME/YOUR-REPO-NAME.git
git branch -M main
git push -u origin main
```

## Step 5: Deploy to GitHub Pages

```bash
npm run deploy
```

This command will:
1. Build your React app for production
2. Create a `gh-pages` branch
3. Push the built files to that branch

## Step 6: Configure GitHub Pages (First time only)

1. Go to your repository on GitHub
2. Click **Settings** → **Pages** (in the sidebar)
3. Under "Source", select **Deploy from a branch**
4. Under "Branch", select **gh-pages** and **/root**
5. Click **Save**

## Step 7: Access your site

After a few minutes, your site will be live at:
`https://YOUR-GITHUB-USERNAME.github.io/YOUR-REPO-NAME`

## Future Updates

Whenever you make changes:

```bash
# Make your changes to the code
git add .
git commit -m "Description of changes"
git push origin main

# Deploy the updates
npm run deploy
```

## Troubleshooting

### Blank page after deployment
- Make sure the `homepage` field in package.json is correct
- Check browser console for errors
- Verify the gh-pages branch was created

### 404 Error
- Ensure GitHub Pages is enabled in repository settings
- Check that the source is set to the gh-pages branch
- Wait a few minutes after first deployment

### Build fails
- Run `npm install` to ensure all dependencies are installed
- Check for any console errors when running `npm start` locally
