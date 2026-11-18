# CarryMatch architecture / 技术架构

**Source of truth:** Frontend `index.html` at repository main, reviewed 2026-11-19. Backend implementation has not been inspected.

```text
Cloudflare Workers static assets
  index.html + hero.jpg
       |
       v
Browser / Supabase JS v2
       |
       +-- Supabase Auth: anonymous sign-in and persisted browser session
       +-- PostgREST: profiles, posts, notifications
       +-- RPC: cm_my_match_cards, cm_my_contacts,
                cm_request_contact, cm_respond_contact,
                cm_my_messages, cm_send_message
       |
       v
Supabase PostgreSQL (tables, policies and SQL functions managed separately)
```

## Client flows / 客户端流程

1. Startup calls `auth.getSession()`, then `signInAnonymously()` if needed.
2. `ensureProfile()` reads or creates the user's `profiles` row.
3. `refresh()` loads `posts`, `notifications`, matching cards and contacts.
4. Posting inserts a `posts` row with route, date, weight and shipping preferences.
5. Matching cards come from `cm_my_match_cards`; users request contact via `cm_request_contact`.
6. A recipient responds through `cm_respond_contact`. Accepted conversations use `cm_my_messages` and `cm_send_message`.
7. Chat refreshes every 3 seconds while visible; inbox-related lists every 12 seconds when relevant and visible.

## Key design decisions

- Responsive static frontend; no dedicated custom application server is visible in the repository.
- Anonymous identity is persisted in the browser; clearing site data may lose access to an anonymous account.
- Browser-side UI hides private details, but **real access control must be enforced in Supabase RLS and RPC**.
- Frontend directly queries `posts` and `notifications` without an explicit owner filter in the JavaScript. Correct per-user filtering therefore depends on backend RLS. Verify this before public launch.
- Supabase SQL source and production RLS policies are not present in the repository. Do not treat this document as a security certification.

## Architecture verification checklist

- [ ] Export and review current table definitions (without user data).
- [ ] Review RLS on every exposed table and security mode of every RPC.
- [ ] Verify anonymous users cannot read or modify other users' posts/messages.
- [ ] Confirm exact SQL matching behavior and index usage.
- [ ] Confirm deployed Cloudflare asset revision matches the GitHub commit.
