# Troubleshooting Permission Denied Error

## If Rules Are Updated But Still Getting Errors:

### Step 1: Make Sure Rules Are PUBLISHED (Not Just Saved)

1. In Firebase Console → Firestore → Rules tab
2. After updating rules, you MUST click **"Publish"** button (top right)
3. Wait for confirmation: "Rules published successfully"
4. The rules in the editor are NOT active until published!

### Step 2: Clear Browser Cache

1. Press `Ctrl + Shift + Delete` (Windows) or `Cmd + Shift + Delete` (Mac)
2. Select "Cached images and files"
3. Click "Clear data"
4. Refresh your website

### Step 3: Verify Firestore is Enabled

1. Go to Firebase Console
2. Click **Firestore Database**
3. Make sure you see "Cloud Firestore" (not "Realtime Database")
4. If you see "Create database", click it and enable Firestore

### Step 4: Check Project ID Matches

1. Firebase Console → Project Settings
2. Note your **Project ID** (should be: `tasks-manager-3aed5`)
3. Open `firebase-config.js`
4. Verify `projectId: "tasks-manager-3aed5"` matches exactly

### Step 5: Test Connection

1. Open your website
2. Open browser console (F12)
3. Look for:
   - `✅ Firebase connected successfully!`
   - `📊 Project ID: tasks-manager-3aed5`
4. If you see errors, check the error code

### Step 6: Verify Rules Are Active

In Firebase Console → Firestore → Rules:
- Rules should show: `allow read, write: if true;`
- Check the history (left side) - should show "Published" status
- If it says "Draft", click "Publish"

### Step 7: Try Test Mode Rules (Temporary)

If still not working, try test mode:

```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /{document=**} {
      allow read, write: if request.time < timestamp.date(2026, 12, 31);
    }
  }
}
```

**⚠️ Remember:** Test mode expires! Use the proper rules for production.

### Step 8: Check Network Tab

1. Open browser DevTools → Network tab
2. Refresh page
3. Look for requests to `firestore.googleapis.com`
4. Check if they return 403 (Forbidden) or 200 (OK)

### Common Issues:

- **Rules not published** → Click "Publish" button
- **Wrong project** → Check project ID matches
- **Firestore not enabled** → Enable it in Firebase Console
- **Browser cache** → Clear cache and refresh
- **Multiple Firebase apps** → Check if Firebase is initialized twice

### Still Not Working?

1. Check browser console for specific error codes
2. Verify `firebase-config.js` has correct values
3. Make sure you're using the correct Firebase project
4. Try in incognito/private browsing mode

