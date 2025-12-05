# Deployment Guide - Natanel Shani ToDoList

## Free Deployment Options

### Option 1: Firebase Hosting (Recommended - Free & Easy)

Firebase Hosting is perfect for this project because:
- ✅ Free tier (generous limits)
- ✅ Fast CDN
- ✅ Free SSL certificate
- ✅ Easy deployment
- ✅ Works with Firebase Firestore (database)

#### Steps:

1. **Create Firebase Project**
   - Go to https://console.firebase.google.com/
   - Click "Add project"
   - Enter project name (e.g., "natanel-todo")
   - Disable Google Analytics (optional)
   - Click "Create project"

2. **Enable Firestore Database**
   - In Firebase Console, go to "Firestore Database"
   - Click "Create database"
   - Start in "Test mode" (for now)
   - Choose a location (closest to your users)
   - Click "Enable"

3. **Get Firebase Config**
   - Go to Project Settings (gear icon)
   - Scroll to "Your apps"
   - Click the web icon `</>`
   - Register app with nickname (e.g., "Todo App")
   - Copy the `firebaseConfig` object

4. **Update firebase-config.js**
   - Open `firebase-config.js`
   - Replace all `YOUR_*` values with your actual Firebase config values

5. **Set Firestore Security Rules**
   - Go to Firestore Database → Rules
   - Replace with:
   ```
   rules_version = '2';
   service cloud.firestore {
     match /databases/{database}/documents {
       match /tasks/{taskId} {
         allow read, write: if request.auth != null || true; // For now, allow all (you can restrict later)
       }
       match /members/{memberId} {
         allow read, write: if request.auth != null || true;
       }
     }
   }
   ```
   - Click "Publish"

6. **Install Firebase CLI**
   ```bash
   npm install -g firebase-tools
   ```

7. **Login to Firebase**
   ```bash
   firebase login
   ```

8. **Initialize Firebase in your project**
   ```bash
   firebase init
   ```
   - Select "Hosting" and "Firestore"
   - Select your project
   - Public directory: `.` (current directory)
   - Single-page app: No
   - Overwrite index.html: No

9. **Deploy**
   ```bash
   firebase deploy
   ```

10. **Your site will be live at:**
    `https://YOUR_PROJECT_ID.web.app`

---

### Option 2: Netlify (Free & Simple)

1. **Create account** at https://www.netlify.com/
2. **Drag and drop** your project folder to Netlify
3. **Done!** Your site is live

**Note:** For Netlify, you'll still need Firebase for the database. Follow steps 1-5 from Option 1, then deploy to Netlify.

---

### Option 3: Vercel (Free & Fast)

1. **Create account** at https://vercel.com/
2. **Install Vercel CLI:**
   ```bash
   npm install -g vercel
   ```
3. **Deploy:**
   ```bash
   vercel
   ```
4. **Follow prompts**

---

## Setting Up Firebase Firestore

After deploying, your tasks will be saved in Firebase Firestore and shared across all users.

### Firestore Collections Structure:

- **tasks**: Stores all tasks
  - Each task has: id, epic, task, deadline, assignee, risk, status, createdAt
  
- **members**: Stores team members
  - Each member is stored as a string in an array

### Viewing Your Data:

1. Go to Firebase Console
2. Navigate to Firestore Database
3. You'll see your collections and documents

---

## Security Notes

For production, update Firestore rules to restrict access:

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /tasks/{taskId} {
      allow read: if true; // Anyone can read
      allow write: if request.auth != null; // Only authenticated users can write
    }
    match /members/{memberId} {
      allow read: if true;
      allow write: if request.auth != null;
    }
  }
}
```

---

## Troubleshooting

- **Can't see tasks?** Check Firebase Console → Firestore to see if data is being saved
- **Deployment failed?** Make sure `firebase-config.js` has correct values
- **Tasks not syncing?** Check browser console for errors

---

## Cost

All options are **FREE** for low-scale usage:
- Firebase: 50K reads/day, 20K writes/day (free tier)
- Netlify/Vercel: 100GB bandwidth/month (free tier)

This is more than enough for a small team!

