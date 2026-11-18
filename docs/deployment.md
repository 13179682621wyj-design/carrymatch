# Deployment runbook / 部署说明

**Current architecture:** GitHub repository stores static frontend files; Cloudflare Workers hosts the public frontend; Supabase hosts auth/database/RPC.

## Release procedure

1. Commit reviewed frontend changes to GitHub.
2. Check that `index.html` and `hero.jpg` are both included.
3. Deploy the static assets to the Cloudflare Worker service `carrymatch` using the currently configured deployment workflow.
4. Open the public site: https://carrymatch.13179682621wyj-863.workers.dev/
5. Check browser console, image load, anonymous sign-in and posting.
6. Test matching, contact acceptance and chat with **two different test sessions**.
7. Record GitHub commit, deployment timestamp, test result and rollback instructions in release notes.

**Important:** GitHub-to-Cloudflare automatic deployment has **not been verified**. A GitHub commit alone may not update production.

## Supabase dependency

The frontend expects a working Supabase project with the tables and RPCs documented in [database-architecture.md](database-architecture.md). Uploading the HTML file does not create or migrate the database. Do not publish database passwords, service-role secrets or private SQL-editor URLs.

## Before changing the database

- Save a reviewed, sanitized migration script and rollback plan.
- Confirm policies and grants in a nonproduction environment.
- Avoid executing unreviewed schema changes against production.
- Verify compatibility with the deployed frontend version.

## Rollback

Redeploy the last known-good static assets. If a database migration is involved, use a separately reviewed rollback; rolling back HTML alone may not reverse schema changes.
