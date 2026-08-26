# my-projects

I am an industrial engineer with six years of operations experience at a Seveso-class chemical site and no formal software-engineering degree. I design and ship production software anyway — SaaS products, workflow automation, and AI systems — using AI-assisted development. This repository is a **case-study portfolio**: it explains what I built, how it is architected, and which problems it solves, so a recruiter and a technical hiring manager can both understand the work in under five minutes.

This is documentation and architecture, not a working product dump. There is no scanning code, no credentials, and no client data here.

## Projects

| Project | One-line description | Case study |
| --- | --- | --- |
| **Vulnox** | Automated security and compliance platform: vulnerability assessment, gap analysis across 250+ frameworks, and digital footprint analysis. | [vulnox/](./vulnox/) |
| **Plant Mood** | Hydroponic and microgreen farm OS: 2D/3D designer, digital-twin operator, calculators, shop, and grower automation. | [plant-mood/](./plant-mood/) |
| **Seveso Automation AI** | Air-gapped local AI platform for regulated industrial sites (RAG, workflows, knowledge library). | [seveso-automation-ai/](./seveso-automation-ai/) |
| **ToDoForFree** | Two-sided marketplace for genuinely free local activities and partner offers. | [todoforfree/](./todoforfree/) |
| **Travos** | Marketplace matching foreigners in Southeast Asia with trusted local service providers. | [travos/](./travos/) |
| **Mobile apps** | Two FlutterFlow apps shipped to the App Store and Google Play. | [mobile-apps/](./mobile-apps/) |

Public products (the domains I own and want listed): [vulnox.io](https://vulnox.io), [plantmood.farm](https://plantmood.farm), [todoforfree.com](https://todoforfree.com), [travos.app](https://travos.app).

## How I build

I do not hide the AI-assisted workflow. It is the production system.

- **Cursor** is the daily engineering environment. I specify architecture, constraints, and domain rules; the agent implements; I review, test, and iterate. The industrial-engineering habit — define the process, then automate it — maps cleanly onto this loop.
- **Supabase** is the default backend: auth, Postgres, storage, edge functions, row-level security, cron, and transactional email. I model the data first, then hang product behaviour off it.
- **n8n** is the orchestration layer. Long-running, multi-step, and third-party work (scans, document generation, sourcing, notifications) lives in workflows, not in a custom job server I would have to maintain alone.
- **GitHub** is source control and the public trail of the work. This repo is the recruiter-facing summary; the live products are separate.
- **Vercel** hosts the customer-facing web apps. Ship, preview, iterate.

The result is that one person can own the full path from payment (or signup) to deliverable, without a backend team, while still producing systems with auth, queues, reporting, and domain-specific logic.

## What this repo is not

- Not a pentest toolkit, scanner, or exploit collection.
- Not a dump of n8n workflow JSON, Supabase schema exports, or `.env` files.
- Not real customer data, scan results, or vulnerability findings.
- Authenticated testing / IDOR case studies are **not included** until they are rewritten against my own apps and independently verified.

## Contact

- **Email:** `[your-email@example.com]`
- **LinkedIn:** `[your LinkedIn URL]`

---

Portfolio repository: [github.com/geertgithub123/my-projects](https://github.com/geertgithub123/my-projects)
