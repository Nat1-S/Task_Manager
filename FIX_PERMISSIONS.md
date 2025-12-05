# Fix Firestore Permission Denied Error

## The Problem
You're seeing: `Permission denied on resource project YOUR_PROJECT_ID`

This means your Firestore security rules are blocking access.

## Solution: Update Firestore Security Rules

### Step 1: Go to Firestore Rules
1. Open Firebase Console: https://console.firebase.google.com/
2. Select your project: **Tasks Manager**
3. Click **Firestore Database** in the left menu
4. Click the **"Rules"** tab at the top

### Step 2: Replace the Rules
Copy and paste this EXACT code:

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

### Step 3: Publish the Rules
1. Click **"Publish"** button (top right)
2. Wait for confirmation: "Rules published successfully"

### Step 4: Verify
1. Refresh your website
2. Open browser console (F12)
3. You should see: `✅ Firebase connected successfully!`
4. Try creating a task - it should work now!

## Alternative: Test Mode Rules (Temporary)

If you want to test quickly, you can use test mode (less secure):

```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /{document=**} {
      allow read, write: if request.time < timestamp.date(2025, 12, 31);
    }
  }
}
```

⚠️ **Warning:** Test mode expires after 30 days. Use the first rules for permanent access.

## Still Having Issues?

1. **Check your project ID matches:**
   - Firebase Console → Project Settings
   - Compare with `firebase-config.js` → `projectId`

2. **Verify Firestore is enabled:**
   - Firebase Console → Firestore Database
   - Should show "Cloud Firestore" (not "Realtime Database")

3. **Check browser console:**
   - Look for specific error messages
   - Make sure no ad blockers are interfering

4. **Try clearing browser cache:**
   - Ctrl+Shift+Delete → Clear cache
   - Refresh the page

## After Fixing

Once rules are published:
- ✅ Tasks will save to Firestore
- ✅ Tasks will load on page refresh
- ✅ Real-time sync will work
- ✅ No more permission errors!

