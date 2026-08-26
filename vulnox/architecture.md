# Vulnox architecture (technical)

This note is for a technical reviewer. It describes **shape**, not production identifiers.

There is **no** workflow JSON, **no** live API URLs, **no** real table dumps, and **no** credentials in this repository.

## Data flow (happy path)

```
Client → Stripe checkout
      → payment confirmation
      → task created in the product database
      → edge function enqueues work
      → n8n orchestrates scanners and/or the evidence-review agent
      → results and files written back to storage + database
      → deliverable generated
      → customer notified and can download from the app
```

Three service families share this spine; they differ in *what* n8n runs:

| Service | After payment, the orchestrator… |
| --- | --- |
| Vulnerability assessment | Runs a scoped reconnaissance / assessment pipeline against **customer-authorised targets only**, then compiles findings into a report. |
| Gap analysis | Does **not** scan the internet. It maps questionnaire answers → SCF controls → evidence requests, waits for uploads, runs AI review, then compiles a gap pack. |
| Digital footprint analysis | Queries **public historical archives** (e.g. web-archive style sources) for previously published material, then flags likely sensitive leftovers for the customer to remediate. |

Recurring work (re-assessments, reminder emails, stale-evidence nudges) is driven by **scheduled jobs** in Supabase, not by a human operator refreshing a queue.

## How Supabase edge functions trigger n8n

n8n is not polled from the browser.

1. A **database event** or **HTTP call from Stripe** (payment succeeded) lands in Supabase.
2. A **trigger** (or the Stripe webhook handler) invokes an **edge function**.
3. The edge function is the only component that knows how to start the right n8n workflow. It sends a small **job envelope**: customer id, service type, framework (if any), and a correlation id. It does **not** send secrets that belong in n8n’s own credential store.
4. n8n runs the workflow, then writes status and artefacts **back** through a documented callback (another edge function or a service-role write to specific tables). The product UI reads those tables; it never talks to scanner hosts.

Auth stays on Supabase Auth. **Row-level security** is the isolation model: a customer session can only read their own orders, evidence, and deliverables.

Conceptually, the connective tissue is:

`payment / upload event → edge function → n8n webhook → workers → callback → tables + storage → UI`

## Schema (conceptual)

Real production names are omitted. The model is:

- **`customers` / `accounts`** — who paid, who can log in.
- **`orders` / `jobs`** — one paid service instance, status machine (paid → in progress → review → delivered).
- **`frameworks`** — the 250+ catalogues (GDPR, ISO 27001, …). Each framework is a *view* over a shared control language.
- **`controls`** — SCF control records. A framework maps many-to-many onto controls.
- **`evidence_requests`** — derived from controls (the Evidence Request List / ERL). This is what the customer is asked to upload.
- **`evidence_files`** — objects in storage plus metadata (which request, who uploaded, mime type).
- **`review_results`** — AI (or later human) scores per evidence request.
- **`findings`** — assessment-pipeline output, always scoped to the paying customer’s authorised assets.
- **`deliverables`** — generated PDFs / dashboards, stored as files with a pointer from the job.

Views (not extra microservices) aggregate scores for report templates so the renderer does not need to understand raw mapping tables.

## How SCF → ERL mapping works

**SCF (Secure Controls Framework)** is a common control catalogue. Individual regulations and standards (GDPR, ISO 27001, SOC 2, …) are mapped *onto* SCF, instead of maintaining 250 independent questionnaires.

**ERL (Evidence Request List)** is the practical layer: for a given control, what artefact would convince an auditor the control is in place?

Pipeline:

1. Customer answers a **questionnaire** whose questions are already tagged with SCF control identifiers.
2. Selected framework + answers → a set of **applicable SCF controls** (not the entire catalogue).
3. Each applicable control expands to one or more **evidence requests**.
4. The customer uploads files against those requests.
5. The **AI review agent** receives: the control text, the request, and the file (or an extracted text representation). It returns a structured verdict (`met` / `partial` / `missing`) plus a short justification bound to that file. It is not asked to invent findings outside the evidence.
6. Unanswered or `missing` items become the gap list and feed the remediation roadmap.

This is why adding a new framework is primarily a **mapping** problem, not a new product.

## What is deliberately not in this repo

- n8n workflow exports (they contain webhook URLs and credential references).
- Edge-function source that would reveal production endpoints.
- Scanner configuration, wordlists, or any code that could be pointed at a domain the operator does not own.
- Real schema dumps, RLS policies copied from production, or `.env` files.

If you are evaluating the engineering: the interesting part is the **event-driven handoff** (Stripe → DB → edge function → n8n → DB → deliverable) and the **SCF/ERL data model**, not a list of tool binary names.
