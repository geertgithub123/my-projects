# ToDoForFree — case study

**Live product:** [todoforfree.com](https://todoforfree.com)

A two-sided marketplace for **genuinely free** local activities, food, sightseeing, and partner offers — claimed in the real world, not as another coupon wall.

---

## Problem

“Free things to do near me” is scattered across Facebook groups, stale blogs, tourist flyers, and brand campaigns that are free in name only. Travellers and locals waste time filtering. Businesses that *do* have a real freebie (a tasting, a tour, a weekday perk) have no clean way to put it in front of people who will actually show up — and no reason to bother if the listing just gets scraped.

The product problem is two-sided: **discovery that is local and honest**, plus **a partner loop** that rewards businesses for participating.

## What I built

ToDoForFree is a location- and category-based discovery product with a claim flow and a partner program:

- **Discovery** — browse freebies by city, category, and audience; map-first where it helps. Listings are meant to be *truly free*, not “free with a timeshare pitch”.
- **QR / OTP claim flow** — a user claims an offer with a short verification path (QR at the venue and/or a one-time code) so partners can see real redemptions instead of anonymous clicks.
- **Partner program** — businesses and local partners publish offers, see performance (views, claims), and get **UGC benefits**: guests who claim can contribute photos and social proof the partner would otherwise have to hire for.
- **Sourcing automation** — n8n helps keep the catalogue alive: sourcing candidate listings and **pulling venue photos via the Google Maps API** so a partner page does not launch as a grey box.

Roles in the marketplace include everyday users, **partners**, and higher-trust local roles (e.g. country leads / brand ambassadors) so the catalogue can grow without a central editorial army.

## Tech stack

| Layer | What I used |
| --- | --- |
| Product / UI | Next.js, TypeScript, Tailwind, Mapbox |
| Backend | Supabase (auth, database, storage, edge functions) |
| Claims | QR generation + OTP / verification flow |
| Maps & photos | Google Maps / Places APIs (photos and location), Mapbox for the product map |
| Automation | n8n — listing sourcing, photo backfill |
| Hosting | Vercel |

## What this demonstrates

- **Two-sided marketplace design** — users want free things; partners want footfall and content. The claim flow is the contract between them.
- **Geolocation features** — city/landmark context, maps, and QR that only make sense *in place*.
- **Partner-facing tooling** — dashboards and UGC, not only a consumer feed.
- **Automation as catalogue ops** — n8n + Maps APIs so inventory does not depend on me copy-pasting every listing.
