# Deploy LateWiz to Cloudflare Pages

Complete guide for deploying LateWiz to Cloudflare Pages using GitHub Actions.

## Overview

This project is configured to automatically deploy to Cloudflare Pages whenever you push to GitHub. The build happens on GitHub's servers (Linux), so it works perfectly from Windows.

## Prerequisites

- GitHub account with your code pushed
- Cloudflare account ([sign up free](https://dash.cloudflare.com/sign-up))
- Late API key from [getlate.dev](https://getlate.dev/dashboard/api-keys)

## Deployment Steps

### Step 1: Get Cloudflare Credentials

#### 1.1 Get Your Account ID

1. Go to https://dash.cloudflare.com/
2. Click **Workers & Pages** in the left sidebar
3. Your **Account ID** is displayed on the right side
4. Copy it (you'll need it in Step 2)

#### 1.2 Create API Token

1. Go to https://dash.cloudflare.com/profile/api-tokens
2. Click **Create Token**
3. Use the **"Edit Cloudflare Workers"** template
4. Or create a custom token with:
   - **Account** → **Cloudflare Pages** → **Edit**
5. Click **Continue to summary** → **Create Token**
6. **Copy the token immediately** (you won't see it again!)

### Step 2: Add Secrets to GitHub

1. Go to your GitHub repository
2. Click **Settings** → **Secrets and variables** → **Actions**

#### Required Secrets (Click "New repository secret")

Add these three secrets:

| Secret Name | Value | Where to Get |
|------------|-------|--------------|
| `CLOUDFLARE_API_TOKEN` | Your API token | From Step 1.2 |
| `CLOUDFLARE_ACCOUNT_ID` | Your account ID | From Step 1.1 |
| `LATE_API_KEY` | Your Late API key | [Get here](https://getlate.dev/dashboard/api-keys) |

**Note on LATE_API_KEY:**
- If you set this, all users share the same API key
- If you skip this, users will be prompted to enter their own key
- Recommended: Set it for simplicity

#### Optional Variables (Click "Variables" tab → "New repository variable")

| Variable Name | Default Value | Description |
|--------------|---------------|-------------|
| `NEXT_PUBLIC_APP_URL` | `https://latewiz.pages.dev` | Your app's public URL |
| `NEXT_PUBLIC_APP_NAME` | `LateWiz` | Custom app name |

### Step 3: Create Cloudflare Pages Project

1. Go to https://dash.cloudflare.com/
2. Click **Workers & Pages** → **Create application** → **Pages**
3. Click **Create project** (not "Connect to Git")
4. Enter project name: `latewiz`
5. Click **Create project**
6. You'll see "Waiting for your first deployment" - that's perfect!

### Step 4: Deploy

Push your code to GitHub:

```bash
git add .
git commit -m "Configure Cloudflare deployment"
git push origin main
```

### Step 5: Watch Deployment

1. Go to your GitHub repository
2. Click the **Actions** tab
3. You'll see "Deploy to Cloudflare Pages" running
4. Click on it to see live logs
5. Wait 3-5 minutes for completion
6. Your app will be live at `https://latewiz.pages.dev`

## How It Works

The `.github/workflows/cloudflare-deploy.yml` file automatically:

1. Triggers on every push to `main` branch
2. Installs dependencies
3. Builds your app with `@cloudflare/next-on-pages`
4. Deploys to Cloudflare Pages

## Environment Variables Reference

### Build-Time Variables (Set in GitHub Secrets/Variables)

| Variable | Type | Required | Purpose |
|----------|------|----------|---------|
| `CLOUDFLARE_API_TOKEN` | Secret | ✅ Yes | Deploy to Cloudflare |
| `CLOUDFLARE_ACCOUNT_ID` | Secret | ✅ Yes | Your Cloudflare account |
| `LATE_API_KEY` | Secret | ⚠️ Optional | Late API backend |
| `NEXT_PUBLIC_APP_URL` | Variable | ❌ No | App public URL |
| `NEXT_PUBLIC_APP_NAME` | Variable | ❌ No | Custom app name |
| `NODE_VERSION` | Auto-set | ✅ Yes | Node.js 20 (automatic) |

### About NEXT_PUBLIC_* Variables

- These are embedded in the build
- Visible in browser/client-side code
- **Never put secrets here!**
- Use for: URLs, app names, feature flags

## Custom Domain (Optional)

After deployment, you can add a custom domain:

1. Go to Cloudflare Dashboard → Workers & Pages → Your project
2. Click **Custom domains** tab
3. Click **Set up a custom domain**
4. Enter your domain (e.g., `app.yourdomain.com`)
5. Follow the DNS configuration instructions
6. Update `NEXT_PUBLIC_APP_URL` variable in GitHub

## Updating Your App

Just push to GitHub:

```bash
git add .
git commit -m "Your changes"
git push origin main
```

GitHub Actions will automatically rebuild and deploy.

## Manual Deployment Trigger

You can also trigger deployment manually:

1. Go to **Actions** tab in GitHub
2. Click **Deploy to Cloudflare Pages**
3. Click **Run workflow** → **Run workflow**

## Troubleshooting

### "Resource not accessible by integration" Error

**Problem:** Missing GitHub secrets

**Solution:** 
- Verify you added `CLOUDFLARE_API_TOKEN` and `CLOUDFLARE_ACCOUNT_ID`
- Check spelling (case-sensitive)
- Make sure they're in "Secrets" not "Variables"

### "Project not found" Error

**Problem:** Cloudflare Pages project doesn't exist

**Solution:**
- Create project in Cloudflare Dashboard (Step 3)
- Project name must be exactly `latewiz`
- Or change `projectName` in `.github/workflows/cloudflare-deploy.yml`

### Build Fails with "Module not found"

**Problem:** Dependencies not installed

**Solution:**
- Check the Actions log for specific error
- Usually auto-resolves on retry
- Verify `package.json` is committed

### "Invalid API key" Error at Runtime

**Problem:** Late API key is incorrect or missing

**Solution:**
- Verify `LATE_API_KEY` secret in GitHub
- Get a new key from [getlate.dev](https://getlate.dev/dashboard/api-keys)
- Key should start with `sk_`
- Re-run the deployment after updating

### Deployment Succeeds but App Shows Errors

**Problem:** Environment variables not set correctly

**Solution:**
- Check all secrets are added in GitHub
- Verify no typos in secret names
- Re-run deployment after fixing

### "This version has a security vulnerability" Warning

**Problem:** Next.js 15.5.2 has a known CVE

**Solution:**
- This is expected - it's the latest version Cloudflare supports
- Cloudflare is working on Next.js 16 support
- For production, monitor for updates
- The vulnerability is low-risk for most use cases

## Monitoring & Logs

### GitHub Actions Logs
- Go to **Actions** tab → Select a workflow run
- View build logs, errors, and deployment status

### Cloudflare Pages Logs
- Go to Cloudflare Dashboard → Your project
- Click **Deployments** tab
- View deployment history and logs

### Runtime Logs
- Go to Cloudflare Dashboard → Your project
- Click **Functions** tab → **Logs**
- View real-time function execution logs

## Project Structure

```
latewiz/
├── .github/
│   └── workflows/
│       └── cloudflare-deploy.yml    # GitHub Actions workflow
├── src/                              # Your app code
├── package.json                      # Dependencies & scripts
├── next.config.ts                    # Next.js config (no standalone output)
└── CLOUDFLARE_DEPLOYMENT.md         # This file
```

## Key Configuration Changes

This project has been configured for Cloudflare:

1. ✅ Next.js downgraded to 15.5.2 (Cloudflare compatible)
2. ✅ React downgraded to 19.0.0 (compatible with Next.js 15)
3. ✅ Removed `output: "standalone"` from `next.config.ts`
4. ✅ Added `@cloudflare/next-on-pages` for building
5. ✅ GitHub Actions workflow configured

## Support & Resources

- [Cloudflare Pages Docs](https://developers.cloudflare.com/pages/)
- [Next.js on Cloudflare](https://developers.cloudflare.com/pages/framework-guides/nextjs/)
- [Late API Docs](https://docs.getlate.dev)
- [GitHub Actions Docs](https://docs.github.com/en/actions)

## Security Best Practices

1. ✅ Never commit secrets to Git
2. ✅ Use GitHub Secrets for sensitive data
3. ✅ Rotate API keys regularly
4. ✅ Use different keys for dev/staging/production
5. ✅ Only use `NEXT_PUBLIC_*` for non-sensitive data

---

**Need help?** Open an issue on GitHub or check the [Late community](https://t.me/latewiz).

**Ready to deploy?** Follow Step 1 above! 🚀
