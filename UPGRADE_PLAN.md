# FarmersNeed upgrade plan

## Phase 1 — Security and persistence (initial implementation)
- Added SQLite-backed farmer profiles and drone bookings using Node.js 22 built-in SQLite.
- Protected profile read/write and booking list/status with `X-Admin-Key`.
- Booking creation returns a `bookingToken`; single booking read/cancel requires `X-Booking-Token` or admin key.
- Added restricted CORS, smaller JSON request limit, response headers and .env exclusion.
- Removed the uploaded `.env` from the deliverable. **Rotate any API credentials previously stored in that file.**

### Important migration note
The old farmer signup form is intentionally blocked from saving profiles on the server until phone OTP authentication is implemented. Local browser profile storage is **not verified authentication**. The old phone-number booking lookup is blocked until a verified user session is implemented. Admin calls require an `X-Admin-Key` header matching `ADMIN_API_KEY`. Do not put the admin key in browser code. New booking clients must securely retain the returned booking token for owner read/cancel operations. Existing in-memory data cannot be migrated because it was never persisted.

## Phase 1 remaining (required before public launch)
- Implement phone OTP via a trusted provider, rate limits, expiring sessions and role-based permissions; replace admin-only farmer profile endpoints with session-based ownership checks.
- Update frontend profile and booking flows to use verified sessions, not phone-number lookup.
- Add CSRF protection if using cookies; validation, abuse protection, audit logs, backup/recovery, and database migrations.
- Review all other endpoints and user-generated HTML for access control and XSS.
- Remove exposed credentials from Git history if they were committed and rotate keys.

## Phase 2 — Frontend
Responsive modular UI, Telugu accessibility, verified login and service flows.

## Phase 3 — Agricultural intelligence
Evidence-backed crop models, image diagnosis, soil recommendations and weather alerts.

## Phase 4 — Marketplace
Verified farmer/buyer accounts, worker and drone provider workflows.

## Phase 5 — Production
Integration and security tests, monitoring, backups, deployments and field testing.
