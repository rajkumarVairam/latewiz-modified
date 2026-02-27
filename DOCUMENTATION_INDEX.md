# Documentation Index

All documentation for deploying LateWiz to Cloudflare Pages.

## 🚀 Getting Started

Start here based on your needs:

### New to Deployment?
→ **[QUICKSTART.md](./QUICKSTART.md)** - 5 steps, 15 minutes

### Want a Checklist?
→ **[DEPLOYMENT_CHECKLIST.md](./DEPLOYMENT_CHECKLIST.md)** - Step-by-step checklist

### Need Full Details?
→ **[CLOUDFLARE_DEPLOYMENT.md](./CLOUDFLARE_DEPLOYMENT.md)** - Complete guide with troubleshooting

### Want to Know What Changed?
→ **[CHANGES.md](./CHANGES.md)** - All modifications explained

## 📚 Documentation Files

| File | Purpose | When to Use |
|------|---------|-------------|
| **QUICKSTART.md** | 5-step quick guide | First deployment |
| **DEPLOYMENT_CHECKLIST.md** | Interactive checklist | Step-by-step deployment |
| **CLOUDFLARE_DEPLOYMENT.md** | Complete reference | Troubleshooting, details |
| **CHANGES.md** | What was modified | Understanding changes |
| **README.md** | Project overview | General information |
| **CONTRIBUTING.md** | Contribution guide | Contributing to project |

## 🔧 Configuration Files

| File | Purpose |
|------|---------|
| `.github/workflows/cloudflare-deploy.yml` | GitHub Actions deployment |
| `package.json` | Dependencies and scripts |
| `next.config.ts` | Next.js configuration |
| `.node-version` / `.nvmrc` | Node.js version (20) |

## 🎯 Recommended Reading Order

### First Time Deploying
1. [QUICKSTART.md](./QUICKSTART.md) - Get started fast
2. [DEPLOYMENT_CHECKLIST.md](./DEPLOYMENT_CHECKLIST.md) - Follow the checklist
3. [CLOUDFLARE_DEPLOYMENT.md](./CLOUDFLARE_DEPLOYMENT.md) - If you need help

### Understanding the Setup
1. [CHANGES.md](./CHANGES.md) - What was changed
2. [CLOUDFLARE_DEPLOYMENT.md](./CLOUDFLARE_DEPLOYMENT.md) - How it works

### Troubleshooting
1. [CLOUDFLARE_DEPLOYMENT.md](./CLOUDFLARE_DEPLOYMENT.md) - Troubleshooting section
2. Check GitHub Actions logs
3. Check Cloudflare Pages logs

## 🔑 Key Information

### Required GitHub Secrets
- `CLOUDFLARE_API_TOKEN`
- `CLOUDFLARE_ACCOUNT_ID`
- `LATE_API_KEY` (optional)

### Optional GitHub Variables
- `NEXT_PUBLIC_APP_URL`
- `NEXT_PUBLIC_APP_NAME`

### Deployment Method
- **Automatic**: Push to `main` branch
- **Manual**: GitHub Actions → Run workflow

### Build Time
- First deployment: ~5 minutes
- Subsequent deployments: ~3 minutes

## 📖 Quick Links

- [Cloudflare Dashboard](https://dash.cloudflare.com/)
- [Get Late API Key](https://getlate.dev/dashboard/api-keys)
- [GitHub Actions](https://github.com/features/actions)
- [Cloudflare Pages Docs](https://developers.cloudflare.com/pages/)

## ❓ Common Questions

**Q: Can I build locally on Windows?**
A: No, use GitHub Actions. The build tool doesn't work on Windows.

**Q: Do I need to install anything locally?**
A: No, GitHub Actions handles everything.

**Q: How do I update my app?**
A: Just push to GitHub. It auto-deploys.

**Q: Can I use a custom domain?**
A: Yes, configure it in Cloudflare Dashboard after deployment.

**Q: Is the Late API key required?**
A: Optional. If not set, users enter their own key.

## 🆘 Getting Help

1. Check [CLOUDFLARE_DEPLOYMENT.md](./CLOUDFLARE_DEPLOYMENT.md) troubleshooting section
2. Review GitHub Actions logs
3. Check Cloudflare Pages deployment logs
4. Open an issue on GitHub
5. Join the [Telegram community](https://t.me/latewiz)

---

**Ready to deploy?** Start with [QUICKSTART.md](./QUICKSTART.md)! 🚀
