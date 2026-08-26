# Mobile apps — case study

Two **FlutterFlow** apps, live on the **App Store** and **Google Play**. Short entries; the point for a hiring process is that they were designed, submitted, reviewed, and shipped — not that this repo contains the binaries.

---

## The apps

| App | What it does |
| --- | --- |
| **Woop Box** | Celebration and gifting app: AI-assisted songs, event planning, wishlists, Secret Santa, and shared reminders so a group can actually organise a moment. |
| **Travos** | Mobile app for the Travos marketplace: find trusted local providers for visas, real estate, and insurance, and track applications from a phone. |

Both went through Apple and Google review, not only an internal TestFlight / internal-track build.

## Tech stack

- **FlutterFlow** → Flutter / Dart
- Store delivery: Apple App Store + Google Play
- Typical backend pairing for this style of app: Firebase / Supabase (auth and data), plus the usual store requirements (privacy nutrition labels, signing, review notes)

## What this demonstrates

- **Mobile product delivery** — a shippable iOS *and* Android binary, not a responsive website bookmarked on a phone.
- **App Store / Play review process experience** — privacy disclosures, screenshots, rejection loops, versioning, and the unglamorous last mile that web-only builders often skip.
- Using a high-level builder **on purpose** for mobile, then still owning listing, review, and release — consistent with the rest of this portfolio: pick the tool that gets a real user onto a real store.
