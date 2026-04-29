# Radiant Classes Website

This project is ready to host on GitHub Pages or Render, and it can use Firebase for live demo submissions and admin login.

## Files

- `index.html` - main website
- `admin.html` - admin panel
- `firebase-config.js` - Firebase project settings
- `render.yaml` - Render static site configuration

## Publish On GitHub Pages

1. Create a new GitHub repository.
2. Upload these files to the repository root:
   - `index.html`
   - `admin.html`
   - `firebase-config.js`
   - `.nojekyll`
   - `README.md`
3. Open the repository on GitHub.
4. Go to `Settings` -> `Pages`.
5. Under `Build and deployment`, choose:
   - `Source`: `Deploy from a branch`
   - `Branch`: `main`
   - `Folder`: `/ (root)`
6. Save the settings.
7. Wait a few minutes for GitHub Pages to publish the website.

Your live site URL will look like:

`https://your-github-username.github.io/your-repository-name/`

## Firebase Setup

Before the live form and admin panel work online, complete these Firebase steps:

1. Create a Firebase project at the Firebase console.
2. Add a `Web App` to the project.
3. Copy the Firebase config values into `firebase-config.js`.
4. In `firebase-config.js`, also set:
   - `window.RADIANT_ADMIN_EMAIL` to your real admin email
5. In Firebase Authentication:
   - enable `Email/Password`
   - enable `Google`
6. Create the admin user in Firebase Authentication with the same email as `window.RADIANT_ADMIN_EMAIL`.
7. In Authentication -> Settings -> Authorized domains, add your live domain:
   - `radiant-classes.onrender.com`
8. Create a Cloud Firestore database in production mode or test mode.
9. Add these Firestore security rules and replace the email with your real admin email:

```txt
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /demoRequests/{document=**} {
      allow create: if true;
      allow read, delete: if request.auth != null
        && request.auth.token.email == "admin@example.com";
    }

    match /signinRequests/{document=**} {
      allow create: if true;
      allow read, delete: if request.auth != null
        && request.auth.token.email == "admin@example.com";
    }
  }
}
```

After this setup:

- `Book Free Demo Session` saves online in Firestore
- the admin panel reads live enquiry data from Firestore
- admin login uses Firebase Authentication
- student popup sign-in supports Google and Email/Password

## Publish On Render

1. Create a new GitHub repository.
2. Upload these files to the repository root:
   - `index.html`
   - `admin.html`
   - `firebase-config.js`
   - `.nojekyll`
   - `README.md`
   - `render.yaml`
3. Push the repository to GitHub.
4. Log in to Render.
5. Click `New +` -> `Static Site`.
6. Connect your GitHub account to Render.
7. Select your repository.
8. Render should detect the static site automatically.
9. If Render asks for settings, use:
   - `Build Command`: leave empty
   - `Publish Directory`: `.`
10. Click `Create Static Site`.

Your Render URL will look similar to:

`https://radiant-classes.onrender.com`

## Update Firebase Config

Edit `firebase-config.js` and replace the placeholder values:

```js
window.RADIANT_FIREBASE_CONFIG = {
  apiKey: "YOUR_FIREBASE_API_KEY",
  authDomain: "YOUR_PROJECT_ID.firebaseapp.com",
  projectId: "YOUR_PROJECT_ID",
  storageBucket: "YOUR_PROJECT_ID.firebasestorage.app",
  messagingSenderId: "YOUR_MESSAGING_SENDER_ID",
  appId: "YOUR_APP_ID"
};

window.RADIANT_ADMIN_EMAIL = "admin@example.com";
```

## Admin Login

The admin panel now uses Firebase Authentication.

- open `admin.html`
- log in with the Firebase admin email and password you created in the Firebase console
