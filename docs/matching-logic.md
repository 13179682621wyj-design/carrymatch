# Matching logic / 匹配逻辑

## Product reasoning

CarryMatch matches a **feasible handoff path**, not necessarily an identical airport destination. The product distinguishes a request (`kind='need'`) from available traveler capacity (`kind='trip'`).

## Inputs collected by the frontend

- Origin and destination country/city
- Travel date (traveler) or latest acceptable delivery date (requester)
- Available capacity or requested weight (kg)
- Origin shipping acceptance and destination forwarding preferences
- Item category and optional private description for requests

The frontend sets `visibility='private'` on new posts. UI text states that cross-city handoffs are considered only within the same country/region with mutual agreement; cross-border forwarding and multi-leg routing are not automatically supported.

## What the frontend actually does

The frontend submits structured posts and calls `cm_my_match_cards` to retrieve matches. **The matching algorithm itself runs in Supabase SQL and is not included here.** Therefore the exact date comparison, country normalization, weight threshold, ranking and exclusions cannot be verified from this repository alone.

## Proposed acceptance cases (not verified results)

| Case | Expected behavior to validate |
| --- | --- |
| Same route, compatible date, sufficient weight | Eligible match |
| Different users, mutually accepted domestic forwarding | Eligible if SQL rules permit |
| Insufficient available kg | No match |
| Traveler departure after latest delivery deadline | No match |
| Same user posts both sides | No self-match |
| Cross-border forwarding requiring extra leg | Not auto-matched |
| Invalid/ambiguous country or city names | Handle safely and consistently |

## Next iteration

Document SQL matching rules from the actual function definition, add regression cases for edge dates and geography, then introduce explainable match reasons and optional scoring. Avoid claiming a scoring algorithm is deployed before implementation.
