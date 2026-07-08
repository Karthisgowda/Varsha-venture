# Complete Online Website Pending Work

This file tracks the remaining work needed to make the Varsha Venture portal a complete production-ready online website.

## Critical launch blockers

- Enable Firebase Anonymous Authentication in Firebase Console.
- Publish `firestore.rules` and `storage.rules` from this repository.
- Confirm customer submissions from phone appear in admin dashboard on laptop.
- Confirm document upload works for PDF, image, DOC/DOCX, and ZIP files up to 10 MB.
- Confirm FormSubmit activation email is approved for `vvltdpvt@gmail.com`.
- Replace test Firebase rules with production-grade admin-only rules before handling real customer data at scale.

## Core loan portal work

- Add a proper customer dashboard page showing submitted enquiry status.
- Add application reference number for every enquiry.
- Add status timeline: Submitted, Under review, Documents pending, In progress, Approved, Rejected.
- Add admin filters by status, loan type, date, city, and amount.
- Add admin search by name, mobile, email, and application reference.
- Add export option for admin records as CSV.
- Add document preview links inside admin detail panel.
- Add clear error messages for Firebase auth, Firestore, Storage, and email delivery failures.
- Add privacy policy and terms pages for customer consent.
- Add contact section with phone, WhatsApp, email, and office address.

## Security and compliance

- Move admin login to a real authentication provider before production use.
- Restrict admin read/update access to the admin account only.
- Avoid exposing full customer KYC data in public-readable Firestore rules.
- Add audit trail for admin status changes.
- Add consent timestamp and customer IP/session metadata where legally appropriate.
- Add data retention policy for uploaded documents.

## Design and usability

- Add mobile-first testing for all form steps.
- Improve admin dashboard table behavior on small screens.
- Add loading states for upload, save, sync pending records, and status updates.
- Add empty states that explain exactly what the admin should do next.
- Add success screen with application reference and next steps.
- Add brand content for Varsha Venture services and trust signals.

## Deployment

- Confirm GitHub Pages is serving the latest `main` branch.
- Add a custom domain if available.
- Configure Firebase authorized domains for the live website domain.
- Test the full flow from at least two devices.
- Keep `README.md` updated with live link, admin access, and setup requirements.
