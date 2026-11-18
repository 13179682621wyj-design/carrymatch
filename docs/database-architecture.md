# Database contract / 数据库接口文档

**Status: frontend-observed contract only.** This document records what `index.html` expects. It does **not** assert that all columns, indexes, grants or RLS policies have been independently verified in Supabase.

## Tables referenced directly

| Table | Frontend usage | Important fields observed |
| --- | --- | --- |
| `profiles` | Select by `id`; insert/update own profile | `id`, `nickname`, `avatar_key`, `avatar`, `bio` |
| `posts` | Insert, list, delete own listings | `id`, `owner`, `kind`, `origin`, `destination`, country/city fields, `travel_date`, `latest_delivery_date`, `weight_kg`, `available_kg`, `status`, `visibility`, `description`, `item_category`, forwarding flags |
| `notifications` | List recent notifications; mark read | `id`, `title`, `body`, `created_at`, `read_at` |

The frontend posts flags including `accepts_domestic_forwarding`, `accepts_domestic_parcels`, `accepts_origin_shipping`, `accepts_destination_shipping`, `traveler_accepts_origin_shipping`, and `traveler_accepts_destination_shipping`.

## RPCs referenced

| RPC | Client input | Purpose inferred from call |
| --- | --- | --- |
| `cm_my_match_cards` | none | Matching cards for current user |
| `cm_my_contacts` | none | Contact requests and accepted conversations |
| `cm_request_contact` | `p_need`, `p_trip` | Request a connection |
| `cm_respond_contact` | `p_request`, `p_accept` | Accept/reject request |
| `cm_my_messages` | `p_request` | Read conversation |
| `cm_send_message` | `p_request`, `p_content` | Send message |

**Unverified:** SQL bodies, return types, ownership checks, function execution grants, `SECURITY DEFINER` settings, indexes and policies.

## Backend review checklist / 待核实

- [ ] `profiles`: users can update only their own profile.
- [ ] `posts`: owners can read/delete their own records; other users cannot enumerate private listings.
- [ ] `notifications`: users can read/update only their own notifications.
- [ ] Contact RPCs check that caller is a valid party and status transitions are permitted.
- [ ] Message RPCs require an accepted contact and enforce conversation membership.
- [ ] Match RPC returns only necessary anonymous summaries, not private descriptions or contact details.
- [ ] `EXECUTE` grants are restricted appropriately; SQL functions do not bypass authorization.
- [ ] Query performance and indexes are checked against representative data.

Do not upload production table exports containing user messages, email addresses or itineraries to this public repository.
