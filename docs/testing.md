# Test plan / 测试与验收

This is a **test plan**, not a claim that every case passed. The project description reports prior two-user functional testing; individual test evidence is not committed.

| ID | Scenario | Expected result | Status |
| --- | --- | --- | --- |
| T01 | New browser session | Anonymous user/session created | Not re-run |
| T02 | Edit own profile | Changes persist for same identity | Not re-run |
| T03 | Post request and trip from separate users | Both records saved | Not re-run |
| T04 | Same user publishes both sides | No self-match | Not re-run |
| T05 | Compatible route/date/weight | Match returned according to SQL rules | Not re-run |
| T06 | Insufficient capacity or incompatible date | No match | Not re-run |
| T07 | Send contact request | Recipient sees pending request | Not re-run |
| T08 | Reject request | Chat remains unavailable | Not re-run |
| T09 | Accept request | Only two parties can exchange messages | Not re-run |
| T10 | Third user attempts to access chat | Database denies access | Not re-run |
| T11 | User attempts to read another user's private posts | Database denies access | Not re-run |
| T12 | Return from chat to inbox | Conversation remains accessible | Not re-run |
| T13 | Background/foreground tab | Message updates recover | Not re-run |
| T14 | Mobile narrow viewport | No clipped form or navigation | Not re-run |
| T15 | Site reload | Existing anonymous session persists if storage retained | Not re-run |

## Evidence template

For each test record: date, code commit, environment, two test identities (pseudonyms only), steps, expected vs actual, screenshot with private details redacted, and issue link.

## Security checks

Test with distinct accounts and validate backend denial, not just UI hiding. Never post real personal itineraries or private chats as test evidence. A passing manual UI test does not replace an RLS/RPC security review.
