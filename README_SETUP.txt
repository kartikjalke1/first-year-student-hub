# ProjectHub — setup guide

This is a static HTML + Firebase starter. It does not use browser Local Storage for project, approval, response, or certificate data. Those records are stored in Firebase Cloud Firestore / Storage.

## Important before use
The HTML is a starter, not a ready-connected live service. You must create a Firebase project and paste its Web App config into `index.html`. Firebase setup is free to start, but quotas and billing policies can change. Enable billing only with an adult/administrator's guidance if needed.

## 1. Create Firebase project
1. Open https://console.firebase.google.com/ and create a project.
2. Add a Web App and copy the Firebase config values.
3. In `index.html`, replace all `PASTE_...` config values.
4. In Authentication > Sign-in method, enable **Email/Password**.
5. Create a **Cloud Firestore** database.
6. Create a **Storage** bucket.

## 2. Create the first admin
1. Temporarily use the signup form on your site to create your own account.
2. In Firebase Console > Authentication > Users, copy your account's **UID**.
3. In Firestore, open `users/{your UID}` and change `status` to `approved` and `role` to `admin`.
4. Replace `PASTE_YOUR_ADMIN_AUTH_UID` in BOTH `firestore.rules` and `storage.rules` with that UID.
5. Also replace `ADMIN_UID` in `index.html` with that UID.
6. Publish the Firestore rules and Storage rules.
7. Sign out and sign in again.

The app uses a username field by mapping it to a synthetic Firebase email (`username@projecthub-login.invalid`). Users should choose unique usernames. Do not reuse important personal passwords.

## 3. Publish
Upload `index.html` to the root of your GitHub repository. In repository Settings > Pages, choose Deploy from a branch, branch `main`, folder `/(root)`.

## Current features
- Student signup request and admin approval
- Admin project publishing with Electronics / Computer / combined category
- Student Interested / Not interested response
- Admin participant list
- Admin certificate upload; each student sees their own certificates
- Cloud Firestore real-time project updates

## Notes / limitations to improve next
- The admin must manually remove Firebase Authentication accounts if permanently deleting a student; changing status to `removed` blocks the app's approved-user view when security rules are also updated to deny them.
- Add password reset, username uniqueness enforcement, audit logs, project edit/delete, team formation, project file uploads, and stronger admin account provisioning before using this for a real class.
- The starter uses an admin UID allow-list in rules. Never rely only on hiding admin buttons in the browser; security rules are the actual access control.
