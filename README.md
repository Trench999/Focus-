# Mnemo backend
1. Create DB, run `db/schema.sql`. Create two roles: `mnemo_app` (no superuser, no BYPASSRLS; grant on decks/documents/cards/reviews/users) and `mnemo_admin` (sessions, auth_tokens, login_attempts, users).
2. `cp .env.example .env.local` and fill in.
3. `npm i && npm run dev`
Routes: POST /api/auth/signup | login | logout, POST /api/generate {title,text}, GET/POST /api/review

Pages: `/` (login/signup) and `/app` (review queue + paste-to-generate).
Ingestion: `POST /api/ingest` accepts multipart (`file` PDF <=10MB + `title`) or JSON (`url` + `title`). Links are fetched server-side with SSRF checks (public hosts only, redirects re-validated).

Auth is username + password (3-24 letters/numbers/underscores, password min 10). There is no email, so no password reset: lost passwords can only be reset by an admin directly in the database.
Routes: GET /api/overview, GET /api/decks/:id.
