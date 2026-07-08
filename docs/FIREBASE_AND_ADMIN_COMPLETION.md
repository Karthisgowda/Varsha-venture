# Firebase And Admin Completion

This file lists the exact backend work still required for reliable cross-device admin dashboard behavior.

## Current repo status

- Firebase config is present in `firebase-config.js`.
- Anonymous Firebase Auth is wired in the website.
- Firestore writes use collection `loanEnquiries`.
- Storage uploads use folder `loan-documents`.
- Pending sync exists for records saved locally during Firebase failure.
- Rule files exist in the repo:
  - `firebase.json`
  - `firestore.rules`
  - `storage.rules`

## Firebase Console tasks

- Open Firebase project `karthiks-digital-canvas`.
- Enable Authentication.
- Enable Anonymous sign-in provider.
- Enable Cloud Firestore.
- Enable Firebase Storage.
- Add the GitHub Pages domain to authorized domains if required.
- Publish Firestore rules from `firestore.rules`.
- Publish Storage rules from `storage.rules`.

## Verification flow

- Open the live site on a phone.
- Login as user and submit a test enquiry with a small test document.
- Open the live site on a laptop.
- Login as admin using `vvltdpvt@gmail.com` and the current admin password.
- Confirm dashboard mode becomes `Shared`.
- Confirm auth status becomes `Signed in`.
- Confirm the phone enquiry appears in the admin table.
- Use `View` to confirm full details are visible.
- Click `Next process` and confirm the user status changes.

## If it still fails

- If Auth status is `Not ready`, Anonymous sign-in is not enabled.
- If Auth status is `Signed in` but dashboard is not `Shared`, Firestore rules are blocking reads.
- If form saves but document link is missing, Storage rules are blocking uploads.
- If email is not received, approve FormSubmit activation email in `vvltdpvt@gmail.com`.
- If pending records exist, press `Sync pending records` after fixing Firebase.

## Production hardening

- Replace anonymous admin access with real admin-only authentication.
- Restrict admin reads and status updates to `vvltdpvt@gmail.com`.
- Keep customer create access separate from admin read/update access.
- Add audit logs for status changes.
- Add delete/retention policy for uploaded documents.
