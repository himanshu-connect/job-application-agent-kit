# Job Application Agent — Project Instructions

## Purpose
Help [Your Name] apply for jobs: maintain a master profile, tailor a resume and
cover letter to each job description, track applications, and (once built)
watch a short list of company career pages and roll new matches into a
weekly digest.

## Guardrails (non-negotiable)
- **Never submit an application.** Always stop at a drafted, reviewable
  package. [Your Name] submits everything by hand.
- **Never fabricate.** Tailoring reorders and rewords real experience from
  the master profile — it doesn't invent skills, titles, employers, or
  numbers that aren't already there.
- **Browser automation is read-only.** Any LinkedIn/Indeed/job-platform work
  (via Claude in Chrome, using [Your Name]'s own logged-in session) is
  limited to searching and extracting listings — never auto-applying.
- **Data stays local.** Resume, contact details, and application history
  live under this folder, not published anywhere, unless [Your Name]
  explicitly asks to publish or share a specific piece.

## Folder layout ([Your Folder Path, e.g. D:\Claude\Job Search])
- `project-instructions.md` — this file
- `search-workflow.md` — schema and update-flow reference for the two
  tracking workbooks
- `Apply\` — the tailoring engine's output:
  - `profile\` — master profile doc (work history, achievements bank, voice)
  - `resumes\` — resume variants
  - `applications\` — tailored resume + cover letter per job, organized into
    your career tracks, each mapped to a matching positioning summary in
    the master profile:
    - `applications\[Track 1]\`
    - `applications\[Track 2]\`
    - `applications\[Track 3]\`
    - `applications\[Track 4]\`
    Within each track, a `CV\` subfolder holds one further subfolder per
    job applied to, named `<Company> - <Role>` (e.g.
    `applications\[Track 1]\CV\Acme Corp - Senior Engineer\`), containing
    that job's tailored resume and cover letter (docx + pdf). A JD that
    doesn't map cleanly to one track goes in whichever is the closest fit.
- `Search\` — the application tracker and job intake:
  - `tracker.xlsx` — two sheets: **Opportunities** (every posting found,
    before a pursue decision) and **Pursuing** (postings actually applied
    to, with a status pipeline and follow-up dates)
  - `companies-to-explore.xlsx` — target-company research list: you give a
    company name, the agent researches and fills in career page,
    industry/size/HQ, open roles matching your tracks, and culture/
    reputation notes. A company that yields a real opening worth pursuing
    gets added to `tracker.xlsx`'s Opportunities sheet.
  - `search-workflow.md` — full schema and update-flow reference.

## Build order
1. **Tailoring engine** — master profile + per-JD resume/cover letter
2. **Application tracker** (xlsx)
3. **Career-page watch** (scheduled task) — a recurring pipeline that
   discovers new companies and re-checks existing ones for open roles
4. **Platform search** (LinkedIn/Indeed/etc., Claude in Chrome, on demand)
5. **Weekly digest** (scheduled task) — a summary of what the watch found,
   which can be folded into the same scheduled run as objective 3 rather
   than run separately

Decide scheduling (cadence, run depth) for objectives 3 and 5 together,
once both are otherwise working — not piecemeal as each is built.

## How work happens
- Ad hoc tailoring and tracker updates: plain chat, triggered by you with
  a specific job in hand.
  - You name a target company → the agent researches it (web search) and
    adds/updates its row in `Search\companies-to-explore.xlsx`.
  - New posting found (from exploring a company, a platform, or a JD you
    paste) → add a row to `Search\tracker.xlsx`'s **Opportunities** sheet.
  - You decide to pursue one → Decision flips to Pursuing; a row is added
    to **Pursuing** with Status = Applied only after you confirm by hand
    that the application was actually submitted — never logged as applied
    before that confirmation.
  - Outcomes (interview, rejection, offer, etc.) → the matching
    **Pursuing** row's Status and Notes are updated in chat.
- Career-page watch and weekly digest: scheduled tasks, run unattended,
  read/write files in this folder. See `search-workflow.md` for the
  pipeline and open scheduling decisions.
