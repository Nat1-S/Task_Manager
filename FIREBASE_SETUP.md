# Firebase Setup Guide - Connect Your Database

## Step 1: Get Your Firebase Configuration

1. Go to your Firebase Console: https://console.firebase.google.com/
2. Select your project: **Tasks Manager**
3. Click the **gear icon** (⚙️) next to "Project Overview"
4. Click **"Project settings"**
5. Scroll down to **"Your apps"** section
6. If you don't have a web app yet:
   - Click the **`</>`** (web) icon
   - Register your app with a nickname (e.g., "Todo App")
   - Click **"Register app"**
7. Copy the `firebaseConfig` object that looks like this:

```javascript
const firebaseConfig = {
  apiKey: "AIzaSy...",
  authDomain: "tasks-manager-3aed5.firebaseapp.com",
  projectId: "tasks-manager-3aed5",
  storageBucket: "tasks-manager-3aed5.appspot.com",
  messagingSenderId: "123456789",
  appId: "1:123456789:web:abcdef"
};
```

## Step 2: Update firebase-config.js

1. Open `firebase-config.js` in your project
2. Replace all the `YOUR_*` values with your actual Firebase config values
3. Save the file

**Example:**
```javascript
const firebaseConfig = {
  apiKey: "AIzaSyC...",  // Your actual API key
  authDomain: "tasks-manager-3aed5.firebaseapp.com",
  projectId: "tasks-manager-3aed5",
  storageBucket: "tasks-manager-3aed5.appspot.com",
  messagingSenderId: "123456789",
  appId: "1:123456789:web:abcdef"
};
```

## Step 3: Set Up Firestore Security Rules

1. In Firebase Console, go to **Firestore Database**
2. Click on the **"Rules"** tab
3. Replace the rules with this (for now, allows all access):

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

4. Click **"Publish"**

**⚠️ Note:** These rules allow anyone to read/write. For production, you should restrict access based on authentication.

## Step 4: Test the Connection

1. Open your website
2. Log in with an authorized email
3. Create a task
4. Check Firebase Console → Firestore Database → Data tab
5. You should see:
   - A **"tasks"** collection
   - A **"members"** collection (when you add members)

## Step 5: Verify Data Structure

Your Firestore will have:

### Collection: `tasks`
Each document ID = task ID (number as string)
```
{
  id: 1,
  epic: "Work",
  task: "Complete project",
  deadline: "2024-12-31",
  assignee: "John",
  risk: "Medium",
  status: "Open",
  createdAt: "2024-01-15"
}
```

### Collection: `members`
Document ID: `list`
```
{
  list: ["John", "Jane", "Bob"]
}
```

## Troubleshooting

### Tasks not saving?
- Check browser console (F12) for errors
- Verify `firebase-config.js` has correct values
- Check Firestore Rules are published

### Can't see data in Firebase Console?
- Make sure you're looking at the correct project
- Refresh the Data tab
- Check if collections were created

### Real-time sync not working?
- Check browser console for Firebase errors
- Verify Firebase SDK is loading (check Network tab)

## Next Steps

Once connected:
- ✅ Tasks will save automatically
- ✅ Changes sync in real-time across all users
- ✅ Data persists even after closing browser
- ✅ All team members see the same tasks

Your database is now connected! 🎉

