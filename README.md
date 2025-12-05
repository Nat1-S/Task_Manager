# Natanel Shani ToDoList

A modern task management board with real-time collaboration, charts, and email-based authentication.

## Features

- ✅ Email-based authentication
- ✅ Task management (Epic, Deadline, Assignee, Risk, Status)
- ✅ Real-time sync across all users
- ✅ Progress charts (line chart + pie chart)
- ✅ Dark mode support
- ✅ Member management
- ✅ Task history (persisted in Firebase)

## Quick Start

1. **Set up Firebase:**
   - Go to https://console.firebase.google.com/
   - Create a new project
   - Enable Firestore Database
   - Copy your Firebase config

2. **Configure Firebase:**
   - Open `firebase-config.js`
   - Replace all `YOUR_*` values with your Firebase credentials

3. **Deploy:**
   - See `DEPLOYMENT.md` for detailed instructions
   - Recommended: Firebase Hosting (free)

## Files

- `login.html` - Login page
- `todo.html` - Main application
- `firebase-config.js` - Firebase configuration (update this!)
- `DEPLOYMENT.md` - Detailed deployment guide

## Admin Emails

Currently authorized:
- admin@natanelshani.com
- natanel@example.com
- Natanel.Shani@gmail.com
- adipeled11@gmail.com

Update in both `login.html` and `todo.html` to add more.

## Tech Stack

- Vanilla JavaScript
- Firebase Firestore (database)
- Firebase Hosting (deployment)

## License

Private project for Natanel Shani.

