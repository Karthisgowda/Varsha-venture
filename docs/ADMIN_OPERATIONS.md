# Admin Operations

This guide explains how the admin should operate the portal after launch.

## Daily workflow

- Login to the admin dashboard.
- Check dashboard mode and auth status.
- Review new enquiries.
- Open each application detail.
- Verify customer contact information.
- Check uploaded document link.
- Move valid applications to `In progress`.
- Reject invalid applications with a clear follow-up call or email.
- Use pending sync only after Firebase rules are fixed.

## Customer follow-up

- Contact customer within one working day.
- Confirm loan type and required amount.
- Confirm employment type.
- Confirm mandatory documents.
- Ask for missing documents before moving application forward.
- Record notes outside the static dashboard until admin notes are implemented.

## Document expectations

- Salaried customers:
  - KYC proof.
  - Latest 3 months salary slips.
  - Latest 6 months bank statement.
- Self-employed customers:
  - KYC proof.
  - Latest 6 months bank statement.
  - Latest 2 years ITR.

## Real estate operations

- Verify property listing details before publishing.
- Keep property price, locality, and availability updated.
- Follow up property enquiries separately from loan-only enquiries.
- Track site visit requests.
- Connect property buyers with home loan support.

## Maintenance

- Review Firebase rules before production traffic increases.
- Rotate admin password if it was shared.
- Keep documentation updated after every feature release.
- Export or archive old leads on a fixed schedule.
