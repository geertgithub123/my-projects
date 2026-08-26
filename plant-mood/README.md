# Plant Mood — case study

**Live product:** [plantmood.farm](https://plantmood.farm)

Software for people who actually grow — hydroponic towers, racks, NFT channels, and microgreen trays — not a generic “farm ERP” with fields that do not match the bench.

---

## Problem

Managing a hydroponic or microgreen operation is several jobs glued together with notebooks:

- **Design** — will this room even fit the towers, and what will power, pipe, and plants cost before you buy?
- **Batch tracking** — germination, blackout, light, harvest: every tray is on a different clock.
- **Sales** — leftover harvest has a shelf life measured in hours, not weeks.

Spreadsheets do not know the floor plan. IoT dashboards do not know the crop recipe. Shop tools do not know which rack is ready tomorrow. Growers stitch this themselves and lose harvests in the gaps.

## What I built

Plant Mood is a farm operating system with a **quick-start path** (sketch the room, see the numbers, start tracking) and a set of tools that stay useful after day one:

- **2D / 3D farm designer** — drag racks, towers, and water channels onto a floor plan. The layout estimates plant capacity, pipe lengths, electricity cost, setup cost, monthly revenue, and payback in the grower’s currency.
- **Digital-twin farm operator** — the same floor plan becomes the live map. Click a rack or channel to see active batches, growth stage, and open tasks. Wrong-stage trays surface before they cost a harvest.
- **Batch timeline** — seed → harvest across the whole farm on one screen (germination, blackout, light, harvest-now), with colour-coded stages and countdowns.
- **Calculators** (public, no login required for the core set) — nutrient mixer / EC & pH correction, light-intensity simulator, harvest calendar, profit calculator.
- **Public shop** — turn harvest into orders instead of a side spreadsheet.
- **Automation** — n8n-driven **Telegram updates** (batch and task alerts) and **document generation** (shopping lists, grow guides matched to the layout).

The public tools are intentionally ungated. The manager is where a farm’s own batches, inventory, and shop live.

## Architecture (sanitized)

See [diagrams/architecture.mmd](./diagrams/architecture.mmd).

Grower → Next.js app → Supabase (auth, farm layouts, batches, shop) → n8n (Telegram, generated PDFs/guides). Spatial UI (2D grid + 3D preview) is a first-class part of the product, not a screenshot overlay.

## Tech stack

| Layer | What I used |
| --- | --- |
| Product / UI | Next.js, TypeScript, 2D canvas + 3D preview for layouts |
| Backend | Supabase (auth, database, storage) |
| Automation | n8n — Telegram notifications, document generation |
| Hosting | Vercel |
| Adjacent data | IoT-style pulls and grower-entered sensor / recipe values (the product is useful with or without hardware) |

## What this demonstrates

- **Product design for a real operator**, not a generic CRUD admin: the floor plan *is* the UI.
- **Spatial / 3D UI** — layout, capacity, and cost in the same interaction.
- **IoT-adjacent data** — batches and tasks sit next to environmental / recipe numbers without requiring a proprietary hardware lock-in to start.
- **End-user automation** — Telegram and generated documents so the farm does not need another person to “run the software”.
