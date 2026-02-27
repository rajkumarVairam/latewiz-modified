# Cloudflare Deployment Checklist

Quick checklist to deploy LateWiz to Cloudflare Pages.

## ✅ Pre-Deployment Checklist

- [ ] Code pushed to GitHub
- [ ] Cloudflare account created
- [ ] Late API key obtained from [getlate.dev](https://getlate.dev/dashboard/api-keys)

## 📋 Deployment Steps

### 1. Get Cloudflare Credentials (5 minutes)

- [ ] Get Account ID from https://dash.cloudflare.com/ → Workers & Pages
- [ ] Create API Token at https://dash.cloudflare.com/profile/api-tokens
  - Use "Edit Cloudflare Workers" template
  - Copy token immediately

### 2. Add GitHub Secrets (3 minutes)

Go to GitHub repo → Settings → Secrets and variables → Actions

**Required Secrets:**
- [ ] `CLOUDFLARE_API_TOKEN` - Your Cloudflare API token
- [ ] `CLOUDFLARE_ACCOUNT_ID` - Your Cloudflare account ID
- [ ] `LATE_API_KEY` - Your Late API key (optional but recommended)

**Optional Variables (Variables tab):**
- [ ] `NEXT_PUBLIC_APP_URL` - Your app URL (default: https://latewiz.pages.dev)
- [ ] `NEXT_PUBLIC_APP_NAME` - App name (default: LateWiz)

### 3. Create Cloudflare Project (2 minutes)

- [ ] Go to https://dash.cloudflare.com/ → Workers & Pages
- [ ] Click Create → Pages → Create project
- [ ] Name: `latewiz`
- [ ] Click Create project

### 4. Deploy (1 minute)

```bash
git add .
git commit -m "Deploy to Cloudflare"
git push origin main
```

- [ ] Go to GitHub → Actions tab
- [ ] Watch "Deploy to Cloudflare Pages" workflow
- [ ] Wait for completion (3-5 minutes)

### 5. Verify (1 minute)

- [ ] Visit https://latewiz.pages.dev
- [ ] Test login/functionality
- [ ] Check that API key works

## 🎉 Post-Deployment (Optional)

- [ ] Add custom domain in Cloudflare Dashboard
- [ ] Update `NEXT_PUBLIC_APP_URL` variable
- [ ] Configure DNS for custom domain
- [ ] Test custom domain

## 🔄 Future Updates

To deploy updates:

```bash
git add .
git commit -m "Your changes"
git push origin main
```

GitHub Actions will automatically rebuild and deploy.

## 📚 Full Documentation

See [CLOUDFLARE_DEPLOYMENT.md](./CLOUDFLARE_DEPLOYMENT.md) for:
- Detailed instructions
- Troubleshooting guide
- Environment variables reference
- Security best practices

## ⏱️ Total Time

- First deployment: ~15 minutes
- Future deployments: Automatic on push

---

**Need help?** Check [CLOUDFLARE_DEPLOYMENT.md](./CLOUDFLARE_DEPLOYMENT.md) for troubleshooting.
