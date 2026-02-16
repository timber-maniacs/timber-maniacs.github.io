# Gmail OAuth Setup Guide for GILGAMESH

This guide will walk you through setting up Google Cloud OAuth credentials to enable Gmail receipt syncing in your GILGAMESH game budget tracker.

## Prerequisites
- A Google account
- Access to [Google Cloud Console](https://console.cloud.google.com/)

## Step 1: Create a Google Cloud Project

1. Go to [Google Cloud Console](https://console.cloud.google.com/)
2. Click on the project dropdown at the top of the page
3. Click **"New Project"**
4. Enter a project name (e.g., "GILGAMESH Game Tracker")
5. Click **"Create"**
6. Wait for the project to be created, then select it from the project dropdown

## Step 2: Enable the Gmail API

1. In your Google Cloud project, go to **"APIs & Services" > "Library"**
2. Search for **"Gmail API"**
3. Click on **Gmail API** in the results
4. Click **"Enable"**
5. Wait for the API to be enabled

## Step 3: Configure OAuth Consent Screen

1. Go to **"APIs & Services" > "OAuth consent screen"**
2. Select **"External"** as the User Type
3. Click **"Create"**

### Fill in the required fields:

- **App name**: `GILGAMESH Game Tracker`
- **User support email**: Your email address
- **App logo**: (Optional) Upload an icon if you have one
- **Application home page**: Your GitHub Pages URL (e.g., `https://timber-maniacs.github.io`)
- **Authorized domains**:
  - Add `timber-maniacs.github.io` (or your custom domain)
- **Developer contact information**: Your email address

4. Click **"Save and Continue"**

### Add Scopes:

5. Click **"Add or Remove Scopes"**
6. In the filter, search for **"Gmail API"**
7. Select the scope: `https://www.googleapis.com/auth/gmail.readonly`
   - This allows read-only access to Gmail messages
8. Click **"Update"**
9. Click **"Save and Continue"**

### Add Test Users (for development):

10. Click **"Add Users"**
11. Enter your Gmail address (the account you'll use for testing)
12. Click **"Add"**
13. Click **"Save and Continue"**
14. Review the summary and click **"Back to Dashboard"**

> **Note**: While your app is in "Testing" mode, only test users you've added can authenticate. To make it available to anyone, you'll need to submit your app for verification, but for personal use, Testing mode is fine.

## Step 4: Create OAuth Client ID

1. Go to **"APIs & Services" > "Credentials"**
2. Click **"Create Credentials" > "OAuth client ID"**
3. Select **"Web application"** as the Application type

### Configure the OAuth client:

- **Name**: `GILGAMESH Web Client`
- **Authorized JavaScript origins**: Add your URLs:
  - `https://timber-maniacs.github.io` (your GitHub Pages domain)
  - `http://localhost:8000` (for local testing, optional)
- **Authorized redirect URIs**: Add:
  - `https://timber-maniacs.github.io` (same as your site)
  - `http://localhost:8000` (for local testing, optional)

4. Click **"Create"**

## Step 5: Copy Your Client ID

1. After creating the OAuth client, a dialog will show your credentials
2. **Copy the Client ID** - it will look like:
   ```
   123456789-abcdefghijklmnop.apps.googleusercontent.com
   ```
3. You can also find it later in the Credentials page

## Step 6: Update Your index.html

1. Open `index.html` in your code editor
2. Find this line near the beginning of the script section:
   ```javascript
   const GOOGLE_CLIENT_ID = 'YOUR_CLIENT_ID_HERE.apps.googleusercontent.com';
   ```
3. Replace `YOUR_CLIENT_ID_HERE.apps.googleusercontent.com` with your actual Client ID
4. Save the file

**Example:**
```javascript
const GOOGLE_CLIENT_ID = '123456789-abcdefghijklmnop.apps.googleusercontent.com';
```

## Step 7: Deploy and Test

1. Commit and push your changes to GitHub
2. Wait a moment for GitHub Pages to deploy (usually 1-2 minutes)
3. Visit your site: `https://timber-maniacs.github.io`
4. Click the **"Sync Gmail Receipts"** button on the Dashboard
5. You should see a Google OAuth consent screen
6. Sign in with the Google account you added as a test user
7. Grant the requested permissions (read-only access to Gmail)
8. The app will scan your emails and import gaming purchases!

## How It Works

The app searches your Gmail for purchase receipts from:
- **PlayStation Store** (`@email.playstation.com`, `@playstationmail.com`)
- **Nintendo eShop** (`@nintendo.com`, `@nintendo.net`)
- **Xbox/Microsoft Store** (`@email.microsoft.com`, `@xbox.com`)
- **Steam** (`@steampowered.com`)

For each receipt email found, it extracts:
- Game title
- Price (in EUR)
- Purchase date
- Platform

The app automatically detects duplicates and won't import the same purchase twice.

## Privacy & Security

✅ **Your data stays private:**
- All processing happens client-side in your browser
- No data is sent to any server (except Google's OAuth and Gmail API)
- Emails are processed in your browser and immediately discarded
- Only extracted purchase data (title, price, date, platform) is stored locally in IndexedDB

✅ **Read-only access:**
- The app only requests `gmail.readonly` scope
- It cannot send emails, delete emails, or modify anything in your Gmail

✅ **Local storage:**
- All purchase data is stored in your browser's IndexedDB
- Nothing is uploaded to any external server

## Troubleshooting

### "Access blocked: Authorization Error"
- Make sure you've added your Gmail address as a test user in the OAuth consent screen
- While in Testing mode, only test users can authenticate

### "Redirect URI mismatch"
- Ensure your GitHub Pages URL is added to "Authorized JavaScript origins" and "Authorized redirect URIs"
- Make sure you're accessing the site via HTTPS (GitHub Pages uses HTTPS by default)

### "API has not been used in project"
- Make sure you've enabled the Gmail API in your Google Cloud project
- Wait a few minutes after enabling and try again

### No purchases found
- Check that you have receipt emails from PlayStation, Nintendo, Xbox, or Steam in your Gmail
- The app searches the last 50 emails per platform (to avoid overwhelming on first sync)
- Email formats may vary - some receipts might not parse correctly

### Want to make the app public?
If you want anyone to use your app (not just test users):
1. Go to OAuth consent screen
2. Click "Publish App"
3. You may need to go through Google's verification process
4. For personal use, keeping it in Testing mode is recommended

## Need Help?

If you encounter issues:
1. Check the browser console for error messages (F12 > Console)
2. Verify all steps in this guide
3. Make sure your Client ID is correctly set in `index.html`
4. Ensure you're accessing via HTTPS

---

**Enjoy automatic receipt syncing! 🎮**
