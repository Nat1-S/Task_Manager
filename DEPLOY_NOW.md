# Deploy Your Todo App - Quick Guide

## Step 1: Update Firebase Config (IMPORTANT!)

Before deploying, you MUST update `firebase-config.js` with your actual Firebase credentials:

1. Go to: https://console.firebase.google.com/
2. Select your project: **Tasks Manager**
3. Click ⚙️ (gear icon) → **Project settings**
4. Scroll to **"Your apps"** section
5. Click on your web app (or create one if needed)
6. Copy the `firebaseConfig` object
7. Open `firebase-config.js` in your project
8. Replace all `YOUR_*` values with your actual values

**Example:**
```javascript
const firebaseConfig = {
  apiKey: "AIzaSyC...",  // Your real API key
  authDomain: "tasks-manager-3aed5.firebaseapp.com",
  projectId: "tasks-manager-3aed5",
  storageBucket: "tasks-manager-3aed5.appspot.com",
  messagingSenderId: "123456789",
  appId: "1:123456789:web:abcdef"
};
```

## Step 2: Set Firestore Security Rules

1. In Firebase Console → **Firestore Database** → **Rules** tab
2. Replace with:
```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /tasks/{taskId} {
      allow read, write: if true;
    }
    match /members/{memberId} {
      allow read, write: if true;
    }
  }
}
```
3. Click **"Publish"**

## Step 3: Deploy Your Website

### Option A: Firebase Hosting (Recommended - Free)

1. **Install Firebase CLI:**
   ```bash
   npm install -g firebase-tools
   ```

2. **Login to Firebase:**
   ```bash
   firebase login
   ```

3. **Initialize Firebase in your project:**
   ```bash
   firebase init
   ```
   - Select: **Hosting**
   - Select your project: **Tasks Manager**
   - Public directory: `.` (current directory)
   - Single-page app: **No**
   - Overwrite index.html: **No**

4. **Deploy:**
   ```bash
   firebase deploy
   ```

5. **Your site is live at:**
   `https://tasks-manager-3aed5.web.app`

---

### Option B: Netlify (Easiest - Free)

1. Go to: https://www.netlify.com/
2. Sign up/login (free)
3. Click **"Add new site"** → **"Deploy manually"**
4. Drag and drop your project folder
5. **Done!** Your site is live

**Note:** Make sure `firebase-config.js` is updated before deploying!

---

### Option C: Vercel (Fast - Free)

1. Go to: https://vercel.com/
2. Sign up/login (free)
3. Click **"Add New Project"**
4. Import your Git repository
5. Click **"Deploy"**
6. **Done!** Your site is live

---

## Step 4: Test Your Deployment

1. Visit your deployed website
2. Log in with an authorized email
3. Create a task
4. Check Firebase Console → Firestore Database → Data tab
5. You should see your task in the `tasks` collection!

## Step 5: Verify Data is Saving

1. Create a task on your website
2. Go to Firebase Console → Firestore Database → Data
3. You should see:
   - Collection: `tasks`
   - Document with your task data
4. Refresh your website - task should still be there!

## Troubleshooting

### Tasks not saving?
- ✅ Check `firebase-config.js` has correct values
- ✅ Check Firestore Rules are published
- ✅ Open browser console (F12) - look for errors
- ✅ Check Firebase Console → Firestore → Data tab

### Can't access website?
- ✅ Check deployment completed successfully
- ✅ Verify the URL is correct
- ✅ Check if files are in the correct directory

### Real-time sync not working?
- ✅ Check browser console for errors
- ✅ Verify Firebase SDK is loading
- ✅ Check network tab in browser DevTools

---

## You're Done! 🎉

Once deployed and `firebase-config.js` is updated:
- ✅ Tasks save automatically to Firestore
- ✅ Data persists across sessions
- ✅ Real-time sync across all users
- ✅ All changes are saved in your database

Your todo app is now live and saving data! 🚀

