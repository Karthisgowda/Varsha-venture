# Varsha Venture Loan Website

Static loan-provider portal for Varsha Venture.

## Features

- Professional portal navigation with normal page scrolling where content needs space
- User login before loan detail upload
- Three-step loan enquiry form with ZIP/PDF/image/document upload up to 10 MB
- Separate admin login and dashboard screen
- Firebase-ready shared admin dashboard across devices
- Compact admin email submission to `vvltdpvt@gmail.com` with customer name, phone, email, and attachment
- GitHub Pages-ready static deployment

## Admin Access

- Email: `vvltdpvt@gmail.com`
- Password: `VVLoan@2026`

## Email Note

The form posts to `https://formsubmit.co/vvltdpvt@gmail.com`. FormSubmit may send a one-time activation email to `vvltdpvt@gmail.com`; approve that email once so future enquiry emails deliver automatically.

## Deployment

The live site is deployed with GitHub Pages from the `main` branch.

## Firebase

Firebase config is installed in `firebase-config.js` for project `karthiks-digital-canvas`.

See `FIREBASE_SETUP.md` to confirm Firestore and Storage are enabled with rules that allow the website to create enquiries, upload loan documents, and let the admin dashboard read/update application status.
