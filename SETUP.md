# TitanTrack Setup Guide

## Step 1: Set up Firebase

1. Go to [Firebase Console](https://console.firebase.google.com/)
2. Click "Add project" or select existing project
3. Enter project name (e.g., "titantrack")
4. Follow the setup wizard

### Enable Realtime Database

1. In Firebase Console, go to "Build" > "Realtime Database"
2. Click "Create Database"
3. Choose location (closest to you)
4. Start in **test mode** (we'll secure it later)
5. Click "Enable"

### Get Firebase Config

1. Go to Project Settings (gear icon) > General
2. Scroll down to "Your apps"
3. Click the web icon `</>`
4. Register app with nickname "TitanTrack"
5. Copy the `firebaseConfig` object

### Update gym_tracker.html

Open `gym_tracker.html` and replace this section (around line 210):

```javascript
const firebaseConfig = {
    apiKey: "YOUR_API_KEY",
    authDomain: "YOUR_PROJECT_ID.firebaseapp.com",
    databaseURL: "https://YOUR_PROJECT_ID-default-rtdb.firebaseio.com",
    projectId: "YOUR_PROJECT_ID",
    storageBucket: "YOUR_PROJECT_ID.appspot.com",
    messagingSenderId: "YOUR_MESSAGING_SENDER_ID",
    appId: "YOUR_APP_ID"
};
```

With your actual Firebase config values.

### Secure Your Database (Important!)

1. In Firebase Console, go to "Realtime Database" > "Rules"
2. Replace the rules with:

```json
{
  "rules": {
    ".read": true,
    ".write": true
  }
}
```

**Note:** These rules allow anyone to read/write. For better security, implement Firebase Authentication later.

## Step 2: Deploy to GitHub Pages

### Create GitHub Repository

1. Go to [GitHub](https://github.com)
2. Click "New repository"
3. Name it `titantrack` (or any name)
4. Make it **Public**
5. Don't initialize with README
6. Click "Create repository"

### Push Your Code

Open terminal in your project folder and run:

```bash
git init
git add .
git commit -m "Initial commit - TitanTrack"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/titantrack.git
git push -u origin main
```

Replace `YOUR_USERNAME` with your GitHub username.

### Enable GitHub Pages

1. Go to your repository on GitHub
2. Click "Settings"
3. Click "Pages" in the left sidebar
4. Under "Source", select "main" branch
5. Click "Save"
6. Wait 1-2 minutes

Your app will be live at: `https://YOUR_USERNAME.github.io/titantrack/`

## Step 3: Use on Mobile

1. Open the GitHub Pages URL on your phone
2. Add to home screen:
   - **iOS**: Tap Share button → "Add to Home Screen"
   - **Android**: Tap menu (⋮) → "Add to Home Screen"

Now you have TitanTrack as an app icon on your phone!

## Troubleshooting

- **Data not syncing**: Check Firebase config is correct
- **Page not loading**: Wait a few minutes after enabling GitHub Pages
- **Firebase errors**: Make sure Realtime Database is enabled and rules are set

## Security Note

The current setup allows anyone with the URL to access your data. To add authentication:
1. Enable Firebase Authentication (Email/Password or Google)
2. Update database rules to require authentication
3. Add login UI to the app

For personal use, you can keep the URL private and it should be fine.
