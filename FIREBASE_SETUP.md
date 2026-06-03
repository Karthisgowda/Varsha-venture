# Firebase Setup

This portal needs Firebase for cross-device admin dashboard data. Without this setup, GitHub Pages can only keep enquiries in the browser that submitted them.

## 1. Create Firebase services

Enable these in Firebase Console:

- Cloud Firestore
- Cloud Storage

## 2. Add web config

Open `firebase-config.js` and replace every `PASTE_...` value with the Firebase web app config.

Use `firebase-config.example.js` as the shape reference. The real values must come from Firebase Console > Project settings > Your apps > Web app.

The website now shows a yellow warning in admin login and dashboard while those placeholder values are still present. When the real config is added, the warning changes to a green shared-dashboard message.

If the admin dashboard says "Local only", phone submissions will not appear on a laptop. That is expected until the real Firebase config and rules are live.

## 3. Suggested Firestore rules for testing

Use stricter authenticated rules before production. For testing the public form:

```txt
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /loanEnquiries/{id} {
      allow create: if true;
      allow read, update: if true;
    }
  }
}
```

## 4. Suggested Storage rules for testing

```txt
rules_version = '2';
service firebase.storage {
  match /b/{bucket}/o {
    match /loan-documents/{allPaths=**} {
      allow write: if true;
      allow read: if true;
    }
  }
}
```

## Important

These test rules are open enough for development. Before real public use, add Firebase Auth and lock admin reads/updates to the admin account.

## How to confirm it is working

1. Open the live website.
2. Login as admin.
3. Check the `Dashboard mode` card.
4. It must say `Shared`, not `Local only`.
5. Press `Check shared dashboard`.
6. Submit an enquiry from a phone.
7. Refresh the admin dashboard on the laptop.

If the dashboard still says `Local only`, the phone record cannot appear on the laptop because the site is still running without Firebase.

## Email delivery

The loan form posts to `https://formsubmit.co/vvltdpvt@gmail.com` so the admin email receives the customer's name, phone number, email address, and uploaded document. FormSubmit may send a one-time activation email to `vvltdpvt@gmail.com`; approve that email once so future submissions deliver automatically.

The admin dashboard stores the complete application details. If Firebase is active, every device sees those details. If Firebase is not active, the dashboard only shows records from the same browser.
