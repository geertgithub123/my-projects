# Seveso Automation AI — case study

An **air-gapped, on-premise AI platform** for Seveso-class (and similarly regulated) process-industry sites that cannot send operational documents or process data to a public cloud — but still want retrieval, automation, and a usable operator interface.

This work is **self-directed**, based on six years of domain experience as an industrial engineer on a Seveso-class chemical site. It is not a commissioned case study for a named operator, and **no plant, customer, or employer is identified here**.

---

## Problem

A Seveso-class site has the same knowledge problems as any complex plant — SOPs, P&IDs, SDS files, lab results, shift notes — plus a hard constraint: **cloud AI tools are off the table**.

Typical symptoms:

- Procedures and drawings live in shared drives; answers depend on who is on shift.
- Lab and process numbers are transcribed by hand; history is hard to query.
- Meetings and training content are produced slowly, so they go stale.
- Operators already watch many screens; they do not need a thirteenth SaaS login that phones home.

The site still wants AI’s benefits: grounded answers with citations, fewer repetitive documents, and automation that does not require a new IT department.

## What I built

A **local AI platform** designed to run on hardware physically at the site (developed and proven on a **mini PC**), with **no cloud dependency** for models, files, or prompts.

Capabilities in the current build:

- **Local RAG** over internal documents (procedures, drawings, SDS-style files) with source citations in the chat UI.
- **Workflow automation** (self-hosted n8n) for ingest, alerts, backups, and document pipelines.
- **Meeting workflow** — invites, recordings, and a path to **summarization** (transcript → summary) without leaving the LAN.
- **Training content generation** from the same approved document set (drafts grounded in local files, not a public model’s memory of the internet).
- **Process-parameter visualisation** — dashboards and trends for lab / sensor-style time series (wired to live plant systems only when the site allows a one-way, on-prem path).
- **Internal knowledge library** — searchable document store plus role-based access so lab, operations, and management do not all see the same surfaces.

Architecture principle: **data, models, and software stay on site**. USB (or equivalent) is how models move; there is no “just call an API” escape hatch in the design.

## Current status — honest

| Stage | Status |
| --- | --- |
| Proposal / concept | Done |
| **Built** (local prototype) | **Yes** — app, auth, RAG chat, document ingest, workflow stack, and dashboards running on a local mini PC |
| **Piloted** at a live production plant | **Not yet** — air-gapped production deployment and live instrument / DCS wiring are site-visit work and are not claimed as complete |

Treat this as a **working on-prem prototype**, not as a reference that a named factory is running in production.

## Architecture (sanitized)

See [diagrams/architecture.mmd](./diagrams/architecture.mmd).

No public hostnames. Conceptually:

`operator workstation → reverse proxy on the LAN → web app → local database + object storage → local embedding/vector store → local LLM → cited answer`

n8n runs **on the same LAN** for file-drop ingest, alerts, and backups. Role-based access (operator / lab / management / admin) is enforced in the app and the database, not only in the UI.

## Tech stack

| Layer | What I used |
| --- | --- |
| Hosting | Local mini PC / on-prem Docker stack — **no cloud AI APIs** |
| App | Next.js dashboard, role-based navigation |
| Data | Self-hosted Postgres (with time-series where needed), object storage for documents |
| RAG | Local embedding model + vector database; chat answers must cite retrieved chunks |
| LLM | Local model runtime (Ollama-class) on site hardware |
| Automation | Self-hosted n8n |
| Ops | Reverse proxy, container management, local git/backup path |

Exact vendor SKUs, plant network names, and instrument inventories are omitted on purpose.

## What this demonstrates

This is the intersection of **chemical / process operations experience** and **current AI engineering**:

- Designing for **air-gap and regulation** first, features second.
- RAG that is useful on **the site’s own documents**, with citations an operator can check.
- Automation that belongs **next to the plant**, not in a vendor cloud.
- Honest scoping: a complete local prototype is not the same thing as a signed-off plant pilot.

That combination — domain constraint plus a shipped local stack — is the point of this case study.
