# CarryMatch · 顺路带

**让每一次顺路，都多一种可能。**  
*Make every journey a chance to connect.*

An independent, privacy-conscious cross-border matching MVP inspired by everyday requests in international student group chats.

[**Live MVP / 在线体验**](https://carrymatch.13179682621wyj-863.workers.dev/) · [**Portfolio case study / 项目案例**](https://yujie-portfolio.vercel.app/#carry-story)

![Airplane wing above the clouds — CarryMatch hero](./hero.jpg)

> **Project status:** Independently designed and AI-assisted developed MVP, currently in validation and iteration. This is a matching prototype, **not** a shipping company or a guaranteed delivery service.

## 01 · Where it started / 项目起点

During my studies in Singapore, I repeatedly saw messages in student groups:

> “Is anyone flying back to China soon? I need help bringing something.”  
> “I have spare checked-luggage allowance on my next trip.”  
> “Can someone help return a small online order?”

People who needed help and travelers with spare capacity were already there. But group-chat posts disappeared quickly, searching across groups was inefficient, and people were understandably reluctant to publish detailed travel plans.

**The insight:** People do not necessarily need someone flying to the exact same destination. They need a **feasible, mutually agreed handoff path**.

For example, a traveler flying from Singapore to Shanghai might be able to help someone sending an eligible item onward to Wuxi, if domestic forwarding is acceptable to both parties.

在新加坡留学期间，我观察到留学生群中反复出现的求帮带与空余行李额消息。供需真实存在，却容易因为群聊信息被刷走、路线表达不规范及隐私顾虑而错过。项目的核心洞察是：**用户需要的是可行的物品交接路径，而不只是目的地完全一致的航班。**

## 02 · Product approach / 产品方案

CarryMatch is a **two-sided matching platform**, not another public message board.

| Feature / 功能 | What it does / 说明 |
| --- | --- |
| Dual-sided posting / 双向发布 | Post an item-carrying request or available luggage capacity. |
| Structured routes / 结构化路线 | Capture origin and destination countries/cities, travel or delivery date, and weight. |
| Flexible handoffs / 灵活交接 | Consider agreed domestic shipping/forwarding preferences in basic route matching. |
| Anonymous profiles / 匿名身份 | Generate an anonymous identity and allow nickname/avatar editing. |
| Contact requests / 联系申请 | Ask to connect; messaging is available after the other party accepts. |
| In-app messages / 站内聊天 | Support two-party conversations and message updates. |
| Notifications / 站内通知 | Surface matching and contact-related updates. |

**Current scope:** Basic route matching supports eligible domestic forwarding arrangements. Cross-border forwarding and multi-leg transfer routes are **not** automatically matched in the current MVP.

## 03 · My role / 我的工作

**Independent Product Owner · Product Designer · AI-Assisted Developer**

I led the project from observation to a working prototype:

- **Product discovery:** Reframed informal student-group requests into two user journeys and a structured matching problem.
- **Interaction design:** Designed posting flows, anonymous profiles, match cards, contact requests, inbox and chat.
- **Matching logic:** Translated routes, dates, weight and forwarding preferences into data fields and matching conditions.
- **Data and access model:** Built around Supabase PostgreSQL, with row-level security (RLS) and database RPC interfaces; authorization behavior requires continued testing.
- **Implementation and delivery:** Developed a responsive HTML/CSS/JavaScript frontend with AI-assisted coding and deployed the prototype through Cloudflare Workers.
- **Validation:** Tested core flows using two separate anonymous users and iterated on messaging/navigation behavior.

## 04 · Technical overview / 技术架构

```text
Browser · Responsive HTML / CSS / JavaScript
                |
                v
Supabase JavaScript SDK
                |
                v
Supabase Auth (anonymous sessions)
                |
                v
PostgreSQL + RLS + controlled RPC functions
                |
                +-- Profiles and posts
                +-- Matching and contact requests
                +-- Messages and notifications

Static frontend hosted on Cloudflare Workers
```

**Stack:** JavaScript · HTML/CSS · Supabase Auth · PostgreSQL · RLS · Supabase RPC · Cloudflare Workers

The repository currently includes the frontend entry point (`index.html`) and its hero image (`hero.jpg`). The database schema, RLS policies and RPC definitions are **not included** in this repository; the frontend alone is not a fully reproducible backend deployment.

The Supabase **publishable key** in the frontend is a client-side identifier, not a server-side service-role secret. Backend access still depends on correctly configured RLS and RPC authorization.

## 05 · Progress and limitations / 当前进展

**Implemented / 已实现**
- Responsive mobile-first interface and two-sided posting
- Anonymous identity/profile flow
- Rule-based match retrieval and contact requests
- Consent-based contact acceptance and two-party chat
- Inbox/chat tabs and periodic message refresh
- Online MVP deployment and two-user functional testing

**Being improved / 持续优化**
- Global route input consistency and match accuracy
- Chat synchronization and notification experience
- Privacy, authorization and edge-case testing
- User research with a broader participant group

**Not provided / 尚未提供**
- Payment, escrow or transaction settlement
- Shipping fulfillment, customs clearance or delivery guarantees
- Automatically optimized multi-leg or cross-border forwarding

> **Safety note:** CarryMatch is for exploring matches involving permitted items only. Users must independently comply with airline baggage rules, customs regulations and applicable laws. A match is not a transport guarantee.

## 06 · Latest repository snapshot / 当前代码版本

The uploaded frontend is labeled **V3.10 — Persistent message tabs**. This iteration keeps Chat and Contact Requests tabs visible and returns users to the inbox after viewing chat details. The supplied release note indicates no database migration was required for this frontend update.

## 07 · What I learned / 项目反思

The most meaningful part of CarryMatch was not building another website. It was learning to convert a messy, real-world behavior into a product system: identifying two-sided needs, defining structured inputs, designing privacy-conscious interactions, and translating business rules into database queries and a working interface.

**核心收获：** 从真实生活观察出发，把模糊需求拆解为双边用户流程、匹配规则、数据结构与可测试的产品原型，同时明确 MVP 的能力边界。

---

**Built independently in 2026 · Product discovery, interaction design and AI-assisted prototyping.**

[Explore CarryMatch](https://carrymatch.13179682621wyj-863.workers.dev/) · [View portfolio](https://yujie-portfolio.vercel.app/)
