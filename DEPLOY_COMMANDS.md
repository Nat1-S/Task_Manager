# Quick Deploy Commands

## Step 1: Commit and Push to GitHub

```bash
# Check what files changed
git status

# Add all changes
git add .

# Commit with a message
git commit -m "Add Prioritize filter to backlog"

# Push to GitHub
git push
```

## Step 2: Deploy to Your Hosting Service

### If using Netlify (Auto-Deploy):
✅ **Automatic!** If you connected your GitHub repo to Netlify, it will auto-deploy in 1-2 minutes after you push.

**To check:**
- Go to https://app.netlify.com/
- Check your site's "Deploys" tab
- Wait for the new deployment to finish

**To manually trigger:**
- Go to Netlify Dashboard → Your Site → Deploys → "Trigger deploy"

---

### If using Firebase Hosting:

```bash
# Deploy to Firebase
firebase deploy --only hosting
```

**Your site will be live at:**
- `https://YOUR_PROJECT_ID.web.app`
- `https://YOUR_PROJECT_ID.firebaseapp.com`

---

### If using Vercel:

```bash
# Deploy to Vercel
vercel --prod
```

---

## Quick One-Line Commands (All-in-One)

**For GitHub + Netlify (auto-deploy):**
```bash
git add . && git commit -m "Add Prioritize filter to backlog" && git push
```

**For GitHub + Firebase:**
```bash
git add . && git commit -m "Add Prioritize filter to backlog" && git push && firebase deploy --only hosting
```

**For GitHub + Vercel:**
```bash
git add . && git commit -m "Add Prioritize filter to backlog" && git push && vercel --prod
```

---

## After Deployment

1. **Wait 1-2 minutes** for deployment to complete
2. **Visit your site** (e.g., `nataneltasks.netlify.app`)
3. **Hard refresh** your browser (Ctrl+Shift+R or Cmd+Shift+R) to clear cache
4. **Test the new Prioritize filter** in the backlog!

---

## Troubleshooting

- **Changes not showing?** Clear browser cache or use incognito mode
- **Deployment failed?** Check the deployment logs in your hosting dashboard
- **Git push failed?** Make sure you're logged in: `git config --global user.name "Your Name"`

