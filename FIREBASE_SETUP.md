# Firebase Setup

This portal needs Firebase for cross-device admin dashboard data. Without this setup, GitHub Pages can only keep enquiries in the browser that submitted them.

## 1. Create Firebase services

Enable these in Firebase Console:

- Cloud Firestore
- Cloud Storage
- Authentication > Sign-in method > Anonymous

The live site depends on Anonymous Authentication. If anonymous sign-in is not enabled, the admin dashboard shows `Auth status: Not ready` and cross-device Firestore sync will not work.

## 2. Web config

The Firebase web config is installed in `firebase-config.js` for project `karthiks-digital-canvas`.

Use `firebase-config.example.js` as the shape reference. The real values must come from Firebase Console > Project settings > Your apps > Web app.

The website shows Firebase-ready status once this config loads. If records still do not appear across devices, Firestore or Storage rules need to be enabled in Firebase Console.

If the admin dashboard says "Firebase ready", config is loaded but Firestore has not confirmed data access yet. If it says "Shared", the cross-device dashboard is responding.

## 3. Suggested Firestore rules for testing

The website now signs in anonymously before saving enquiries. The repo includes this authenticated version in `firestore.rules`:

```txt
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /loanEnquiries/{id} {
      allow create: if request.auth != null;
      allow read, update: if request.auth != null;
    }
  }
}
```

For quick public testing only, you can temporarily use:

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

The repo includes this authenticated version in `storage.rules`:

```txt
rules_version = '2';
service firebase.storage {
  match /b/{bucket}/o {
    match /loan-documents/{allPaths=**} {
      allow write: if request.auth != null;
      allow read: if request.auth != null;
    }
  }
}
```

Quick public testing only:

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

If the dashboard says `Firebase ready` but `Auth status` says `Not ready`, enable Anonymous Authentication in Firebase Console. If `Auth status` says `Signed in` but the dashboard is not `Shared`, publish the Firestore and Storage rules.

## Deploy rules with Firebase CLI

After installing and logging into Firebase CLI:

```bash
firebase use karthiks-digital-canvas
firebase deploy --only firestore:rules,storage
```

The repo includes:

- `firebase.json`
- `firestore.rules`
- `storage.rules`

## Pending sync recovery

If a customer submits while Firebase rules are blocking writes, the browser keeps a pending local copy before sending the email. After fixing Firebase Authentication, Firestore, and Storage rules:

1. Login to the admin dashboard from the same browser that has pending records.
2. Check the `Pending sync` metric.
3. Press `Sync pending records`.
4. Refresh the admin dashboard on another device and confirm the synced enquiry appears.

## Email delivery

The loan form posts to `https://formsubmit.co/vvltdpvt@gmail.com` so the admin email receives the customer's name, phone number, email address, and uploaded document. FormSubmit may send a one-time activation email to `vvltdpvt@gmail.com`; approve that email once so future submissions deliver automatically.

The admin dashboard stores the complete application details. If Firebase is active, every device sees those details. If Firebase is not active, the dashboard only shows records from the same browser.
