# Firebase Setup

This portal needs Firebase for cross-device admin dashboard data.

## 1. Create Firebase services

Enable these in Firebase Console:

- Cloud Firestore
- Cloud Storage

## 2. Add web config

Open `firebase-config.js` and replace every `PASTE_...` value with the Firebase web app config.

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
