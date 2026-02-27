# Quick Start - Deploy to Cloudflare Pages

Get LateWiz running on Cloudflare Pages in 15 minutes.

## What You Need

- GitHub account (with this code pushed)
- Cloudflare account (free) - [Sign up](https://dash.cloudflare.com/sign-up)
- Late API key - [Get one](https://getlate.dev/dashboard/api-keys)

## 5 Steps to Deploy

### 1️⃣ Get Cloudflare Info (3 min)

**Account ID:**
- Go to https://dash.cloudflare.com/
- Click "Workers & Pages"
- Copy your Account ID (shown on right)

**API Token:**
- Go to https://dash.cloudflare.com/profile/api-tokens
- Click "Create Token"
- Use "Edit Cloudflare Workers" template
- Copy the token

### 2️⃣ Add to GitHub (2 min)

Go to your repo → Settings → Secrets and variables → Actions

Click "New repository secret" and add:
- `CLOUDFLARE_API_TOKEN` = (your token)
- `CLOUDFLARE_ACCOUNT_ID` = (your account ID)
- `LATE_API_KEY` = (your Late API key)

### 3️⃣ Create Cloudflare Project (1 min)

- Go to https://dash.cloudflare.com/
- Workers & Pages → Create → Pages → Create project
- Name: `latewiz`
- Click Create

### 4️⃣ Push to GitHub (1 min)

```bash
git push origin main
```

### 5️⃣ Wait & Visit (5 min)

- Go to GitHub → Actions tab
- Watch the deployment
- Visit https://latewiz.pages.dev when done

## That's It! 🎉

Your app is live. Future pushes to `main` will auto-deploy.

## Need More Details?

- **Full guide**: [CLOUDFLARE_DEPLOYMENT.md](./CLOUDFLARE_DEPLOYMENT.md)
- **Checklist**: [DEPLOYMENT_CHECKLIST.md](./DEPLOYMENT_CHECKLIST.md)
- **What changed**: [CHANGES.md](./CHANGES.md)

## Troubleshooting

**Build fails?**
- Check you added all 3 secrets in GitHub
- Verify secret names are exact (case-sensitive)

**App shows errors?**
- Verify your Late API key is correct
- Check it starts with `sk_`

**More help?**
See [CLOUDFLARE_DEPLOYMENT.md](./CLOUDFLARE_DEPLOYMENT.md) for detailed troubleshooting.
