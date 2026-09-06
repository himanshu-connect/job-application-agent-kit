# Search\ Workflow

How `tracker.xlsx` and `companies-to-explore.xlsx` work together — what each
contains, how they're populated, the steady-state update rhythm, what feeds
the career-page watch, and what happens once an application actually goes
out. Replace every `[bracketed placeholder]` with your own details as you
set this up, and delete this sentence once you have.

## 1. What each file contains

**`tracker.xlsx`**
- **Opportunities** — every job posting found, before any decision to pursue it.
- **Pursuing** — the subset actually applied to, with a status pipeline and follow-up dates.

**`companies-to-explore.xlsx`**
- **Companies to Explore** — target companies researched independent of any
  specific posting: career page, snapshot, open roles, culture signals.

Both are template workbooks: row 1 is a merged legend, row 2 is the header,
row 3 is a grey-italic example to overwrite, panes are frozen below the
example, filters are on, and the categorical columns have dropdown
validation. Each workbook has a **Config** sheet — edit the lists there
(your Tracks, Company Types, Sources) and the dropdowns update automatically.

## 2. Schema

### Opportunities (tracker.xlsx)
| Column | Notes |
|---|---|
| Date Found | |
| Date Posted | The listing's own posted date — used to tell a still-live posting from a genuine re-post |
| Company | |
| Role | |
| Category | Your tracks — set in the Config sheet |
| Company Type | Your company-type list — set in the Config sheet |
| Source | Your platforms — set in the Config sheet |
| Location | |
| Salary Range | |
| JD Link | |
| Fit Notes | |
| Decision | New / Reviewing / Pursuing / Passed |
| Notes | |
| Track Priority | 1 (highest) through 5 (lowest) — define your own ranking of tracks; see §7 |

### Pursuing (tracker.xlsx)
| Column | Notes |
|---|---|
| Company | |
| Role | |
| Category | |
| Source | |
| Date Applied | |
| Application Folder | Path to the tailored resume + cover letter package under `Apply\applications\<Category>\CV\<Company - Role>\` |
| Status | Applied / Under Review / Interview Scheduled / Interviewed / Offer / Rejected / Withdrawn |
| Next Follow-up | Formula: Date Applied + 7 days — overwrite the cell to adjust |
| Last Contact | |
| Notes | |

### Companies to Explore (companies-to-explore.xlsx)
| Column | Notes |
|---|---|
| Company | |
| Website | |
| Career Page URL | |
| Industry | |
| Company Type | Your company-type list — set in the Config sheet |
| HQ / Locations | |
| Company Size | |
| Open Roles (matching your tracks) | |
| Culture / Reputation Notes | |
| Priority | High / Medium / Low — research urgency |
| Watch Career Page | Yes / blank — optional manual priority marker |
| Status | To Research / Researched / Added to Opportunities / Not Pursuing |
| Last Checked | |
| Notes | |

## 3. How each gets populated

- **Companies to Explore**: you name a company in chat → the agent
  web-searches it and fills the row (career page, industry/size/HQ, open
  roles matching your tracks, culture/reputation notes) → Status set to
  Researched.
- **Opportunities**: a row is added whenever a real posting surfaces — from
  a company just explored, from a platform, or from a JD you paste
  directly. Decision starts at New.
- **Pursuing**: a row is added only after you confirm by hand that you
  actually submitted an application — never inferred or pre-logged. Status
  starts at Applied, Next Follow-up auto-fills.

## 4. Steady-state working rhythm

1. New company to research → row/update in **Companies to Explore**.
2. New posting found → row in **Opportunities**, Decision = New.
3. You review an Opportunities row → Decision moves to Reviewing → Pursuing
   (going to apply) or Passed (not interested; the row stays as historical
   record — nothing gets deleted).
4. Once you confirm you applied → a new **Pursuing** row is created; the
   source **Opportunities** row's Notes gets a one-line cross-reference so
   the two sheets stay traceable.
5. Outcomes as they happen (interview, rejection, offer, etc.) → update the
   matching **Pursuing** row's Status, Last Contact, Notes.

## 5. Career-page watch — pipeline (once you're ready to schedule it)

A watch run is a five-step pipeline, not just a re-check of the existing
list:

1. **Sweep for new input.** Check for any company names or leads you've
   mentioned since the previous run that haven't been formally added yet.
2. **Discover new companies.** Search for companies not yet in Companies to
   Explore that could plausibly be hiring for your tracks — industry news,
   expansion announcements, LinkedIn company search, etc.
3. **Search newly-added companies for roles.** Any company added in step 1
   or 2 gets the full per-company search (career page + platforms, all
   tracks).
4. **Open-exploration pass.** Independent of any company list, run a
   keyword search across all your tracks — this surfaces roles at
   companies you had no reason to add otherwise.
5. **Re-check the existing list.** Re-search companies already in
   Companies to Explore, reconcile against existing Opportunities rows
   using the de-dup rule (§6) — a still-open match gets "Reconfirmed
   open" noted, a genuinely new match becomes a new row, a role that no
   longer surfaces gets flagged as possibly closed.

**Run depth is a knob, not a fixed setting.** Each step can run at full
depth (every track searched separately, per company/query) or a lighter
combined depth (one combined query per company/query). Full depth is
thorough but can exhaust search quota fast, especially across a large
company list — start light for a recurring/scheduled run, and reserve full
depth for an occasional manual deep-dive.

## 6. De-duplication across search passes

**Match rule:** same Company (case-insensitive) AND either an identical JD
link, or a normalized title match (ignore case/punctuation/minor wording
differences).

**Once matched, Date Posted decides what happens:** if the new listing's
Date Posted matches the existing row's, it's the same still-live listing —
skip, just note "Reconfirmed open — [date]". If Date Posted is materially
newer, it may be a genuine re-post — a new requisition for the same title
can coexist with or replace an old one; use judgment and log it as a new
row if it reads as a fresh opening, especially if the old row was Passed.
If Date Posted is unavailable, default to treating it as the same listing
but note the assumption.

**A tracked role that disappears** on re-search gets "Not found on
re-search — may be closed" noted in Notes; leave Decision as-is rather
than auto-closing it out.

## 7. Filter criteria — what counts as a "matching" role (fill this in for yourself)

Define these once, then apply them consistently. This is the section
you'll keep refining as you use the system — treat it as a living document.

**Seniority floor:** [e.g. "5+ years, individual contributor or above" or
"Director and above, judged by actual scope not title text"]. Watch for
title inflation/deflation — the same title means different things at
different companies (especially large enterprises vs. startups); check the
JD's actual stated years and scope, not just the title.

**Track priority:** rank your tracks 1 (highest) to however many you have,
for when multiple matches compete for your attention. This becomes the
Track Priority dropdown values in Opportunities.

**Title/keyword sets per track:** for each track, list the job titles and
keywords that would count as a match (e.g. "Senior Backend Engineer,
Staff Engineer, Backend Tech Lead" for a Backend Engineering track).

**Location priority:** [list your preferred locations, ranked, plus
whether you're open to remote/relocation — a location outside your list
still gets logged, just flagged, not excluded].

**Salary floor:** [your number, if you have one] — not usually a hard
disqualifier; log below-floor roles with a flag rather than skipping them.

**Company-level exclusions:** any companies you rule out entirely for
personal or ethical reasons. Once added here, every open role at that
company is skipped regardless of fit — this overrides everything else.
Keep a running list as you add exclusions, with or without a stated
reason (a bare "excluded" is a complete reason on its own).

## 8. Search mechanism — how a company gets searched for open roles

Runs automatically whenever you name a company:

1. Company's own career page.
2. [Your primary platform, e.g. LinkedIn] (via Claude in Chrome, your
   logged-in session, read-only — search only, never apply).
3. [Your other platforms] — same pass, read-only.

Filter every result through §7. Cap results per source (e.g. top 5) to
keep it fast and reviewable — ask for a deeper pass on a specific company
any time.

**Where it lands:** the company's Open Roles cell in Companies to Explore
gets overwritten fresh each search (a live snapshot, not a log); each
individual matching role becomes its own Opportunities row, auto-filled
per the schema in §2.

**Same role found via multiple sources:** one Opportunities row, not two —
Source records every channel it was found on. Default application channel
is the company's own career page/ATS, not a third-party mirror or
aggregator — those often gate "Apply" behind creating an account, which
this system never does.

## 9. Applying in person — how a Pursuing package actually gets submitted

**The non-negotiable guardrail is unchanged: the agent never clicks
Submit/Apply, never creates an account anywhere — you submit every
application yourself, by hand.**

What the agent does to make that fast, per role, once asked:
1. Re-verify the posting is still live and identify the actual application
   platform (company's own ATS vs. an external recruiter vs. a mirror site).
2. If there's a clean, direct, non-account-gated link: open it and pre-fill
   only what's purely factual and non-sensitive — name, email, phone,
   location, current company, resume attachment, and unambiguous factual
   yes/no answers grounded in your master profile.
3. Never fill in: compensation, notice period, relocation willingness,
   voluntary personal disclosures, or any open-ended narrative field —
   these stay yours.
4. Hand back a short note: the link, what was filled, what needs your
   judgment before submitting.
5. Once you confirm by hand that you actually clicked Submit, log it in
   Pursuing — never before that confirmation.

**When there's no clean direct-apply path** (only reachable via an
account-gated mirror, or an external recruiter with no direct link), the
agent says so plainly and hands you the original posting to apply from
yourself.

## 10. Your decisions log (start this section as you go)

As you use this system, judgment calls will come up that are worth writing
down so they're applied consistently next time — a company you've decided
to exclude, a title-inflation pattern you've noticed at a specific
employer, a platform that turns out to be full of stale listings. Add
dated entries here the same way you'd add to the sections above; this
section is meant to grow.
