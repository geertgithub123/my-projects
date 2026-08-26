# Travos — case study

**Live product:** [travos.app](https://travos.app) — also shipped as a FlutterFlow app on the App Store and Google Play (see [mobile-apps](../mobile-apps/)).

A marketplace that matches **foreigners in Southeast Asia** with **trusted local service providers** — visas, real estate, insurance, and the other errands that usually mean a Facebook group and a leap of faith.

---

## Problem

Expats, digital nomads, and new arrivals need local specialists (visa runs, rental contracts, health insurance) in a market where language, regulation, and trust are the actual product. Directories are ads. Freelancer chats do not track documents. Agencies still run the back office in spreadsheets. The foreigner cannot tell a competent shop from a commission farm until it is too late.

## What I built

Travos is a two-sided platform:

- **Clients** find agencies, apply for a service, track the application, and upload required documents in one place.
- **Agencies** manage clients, applications, documents, and day-to-day operations instead of a pile of chat threads.
- Around that core: a **knowledge hub** (articles / video) and **user-generated content** so the next person is not starting from zero.

The product is the match **and** the shared workflow, not only a listing page.

## Tech stack

| Layer | What I used |
| --- | --- |
| Product / UI | Next.js, TypeScript |
| Backend | Supabase (auth, database, storage, documents) |
| Hosting | Vercel |

## What this demonstrates

- **Marketplace / matching product** — two user types, applications as a first-class object, documents in-band.
- **Cross-border domain** — visas, housing, and insurance for people who are not in their home legal system.
- Shipping a service marketplace as a solo (AI-assisted) full-stack build, not a brochure site.
