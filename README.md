# Job Application Agent — Starter Kit

A template system for running your job search with Claude: a master profile that gets tailored per job, a spreadsheet-based tracker, and (optionally) a weekly scheduled task that goes looking for new roles and reports back.

Everything in here is generic — no one's personal data, just the structure. Swap in your own name, career tracks, and CV, and it's yours.

## How it works

You tell Claude about a company or paste a job description → it researches the company and/or logs the posting in the tracker → you decide which ones to pursue → Claude tailors your resume and cover letter from your master profile → you review and submit it yourself.

The one rule that never bends: **Claude never clicks submit.** It drafts, it pre-fills factual fields, it stops. You apply.

## What's in this repo

| File | Purpose |
|---|---|
| [`SETUP.md`](SETUP.md) | Full first-time setup and first-run walkthrough, plus a reference list of job platforms |
| [`docs/Job-Application-Agent-Setup-Guide.docx`](docs/Job-Application-Agent-Setup-Guide.docx) | The same setup guide as a Word document |
| [`templates/project-instructions-template.md`](templates/project-instructions-template.md) | The guardrails and folder-layout rulebook — copy into your own Claude Project |
| [`templates/search-workflow-template.md`](templates/search-workflow-template.md) | How the tracker spreadsheets work, the search pipeline, and the filter-criteria template you fill in for yourself |
| [`templates/scheduled-task-prompt-template.md`](templates/scheduled-task-prompt-template.md) | A ready-to-adapt prompt for the optional weekly automated search-and-digest run |
| [`spreadsheets/tracker-template.xlsx`](spreadsheets/tracker-template.xlsx) | Opportunities + Pursuing tracker, with an editable Config sheet for your own tracks/company types/sources |
| [`spreadsheets/companies-to-explore-template.xlsx`](spreadsheets/companies-to-explore-template.xlsx) | Target-company research list, same Config-sheet pattern |

## Quick start

1. Read [`SETUP.md`](SETUP.md) — it walks through creating a Claude Project, building your master profile, customizing the two template docs, and setting up the two workbooks.
2. Run it once end-to-end before trusting it: research one real company, tailor one real resume, confirm the tracker updates — all covered in `SETUP.md`'s "Run It Once" section.
3. Optionally set up the weekly scheduled task once you're comfortable with the manual flow.

## The guardrails, restated plainly

Never let it submit an application, create an account, or click Apply anywhere — always stop at a reviewable draft. Never let it invent experience — tailoring reorders what's real, it doesn't add what isn't. Keep browser automation read-only on job platforms — search and extract, never act. Keep your data local unless you explicitly choose to share something. These aren't optional extras; they're what make it safe to let this run at all.

## Making it yours

The specific decisions — which platforms to search, what counts as a "senior enough" title, which locations you'll consider, any companies you rule out on principle — are things to work out for your own search. `search-workflow-template.md` has a "decisions log" section at the bottom for exactly this; expect to grow it over time.
