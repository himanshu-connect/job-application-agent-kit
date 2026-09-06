# Weekly Job Search Watch & Digest — scheduled task prompt template

Fill in every `[bracketed placeholder]`, then ask Claude: "set up a weekly
scheduled task with this prompt" (pick your own day/time). Read
`SETUP-GUIDE.md` first if you haven't already — this assumes
`project-instructions.md` and `search-workflow.md` already exist and are
customized for you.

---

This is a recurring weekly run for [Your Name]'s job search project
(claude.ai Project "[Your Project Name]"; connected local folder
[Your Folder Path] on [device]). You are a fresh session with no memory of
any prior conversation. Before doing anything, get current context: if
this session has the "[Your Project Name]" claude.ai Project attached, use
the Projects tool to read project-instructions.md and search-workflow.md
in full — they are the authoritative, possibly-updated source of truth and
override anything below if they conflict. If the Project is not attached,
read the equivalent files from the connected device folder instead.

GUARDRAILS (non-negotiable):
- Never submit any job application, never create accounts anywhere, never
  click Apply/Submit on any form, on any platform, at any step of this run
  — including Step 4 below. Always stop at a saved, reviewable, unsubmitted
  package. [Your Name] submits every application himself/herself, by hand.
- Never fabricate experience, skills, employers, dates, or numbers —
  tailoring only reorders/rewords real content already in the master
  profile.
- Any browsing via Claude in Chrome is read-only: search and extract
  listings only, never log in on [Your Name]'s behalf beyond an
  already-authenticated session, never click Apply.
- Data stays local — don't publish or share anything found in this run.

STEP 0 — Check-in. At the very start of the run, send [Your Name] a short
message asking if there are any specific companies to add to this week's
search. Do not block waiting on a reply — proceed immediately into Step 1
regardless. If a reply with company names arrives before this run's digest
(Step 3) goes out, fold those into Step 1's search too; if it arrives
after, handle it as a normal ad hoc "add this company" request whenever it
arrives.

STEP 1 — Discovery.
(a) Career-page watch pipeline (search-workflow.md), LIGHT depth only —
one combined search query per step, not an exhaustive multi-query sweep,
to keep this sustainable within search-quota limits over time. Use the
Agent tool to spawn one subagent per track ([Track 1], [Track 2],
[Track 3], [Track 4]) to parallelize the sub-steps below:
   1. Sweep tracker.xlsx (Opportunities) and companies-to-explore.xlsx for
      rows added or edited since the last run that aren't fully processed
      yet (plus anything from Step 0).
   2. Discover new companies not yet in companies-to-explore.xlsx that
      could plausibly be hiring for these tracks.
   3. Search newly-added companies for current open roles matching the
      tracks, at the seniority floor defined in search-workflow.md.
   4. One light general search for new matching postings across the
      tracks, independent of any specific company.
   5. Re-check a sample (not all, to stay light) of companies already in
      companies-to-explore.xlsx for whether previously-noted open roles
      are still live or have closed.
   Seniority floor, track-priority rules, and any noisy-source caveats are
   documented in search-workflow.md — follow them.
(b) Do NOT run logged-in platform search ([Your platforms, e.g. LinkedIn,
Indeed, etc.] via Claude in Chrome) automatically in this run — it depends
on an already-logged-in browser session this unattended firing can't
assume is available. Offer it explicitly in the digest (Step 3) instead,
and only run it if/when [Your Name] replies asking for it.

STEP 2 — Tracker update. Merge genuinely new findings from Step 1(a) into
tracker.xlsx (new Opportunities rows, Decision=New) and
companies-to-explore.xlsx (new rows, or updated Status/notes), matching
the exact existing column headers, dropdown values, and formatting. Use
openpyxl, run recalc.py after edits (zero formula errors required), and
commit back through the device bridge with an mtime guard so you never
clobber a concurrent edit. Do not alter existing Pursuing-sheet rows other
than reading them for the follow-up check below. If the device isn't
linked, or write-back fails, don't block on it: save everything found into
a new project doc via the Projects tool instead, note the staged count in
the digest, and merge it in on a future run once the device is reachable.

STEP 3 — Digest & approval gate. Also read the Pursuing sheet and flag any
row where Next Follow-up is today or earlier with no status change since.
Then send [Your Name] one concise digest message covering: new companies
discovered, new matching roles found (company / role / link), previously-
open roles now closed, any pending-merge count, and Pursuing rows due for
follow-up. End the digest by (i) offering to run the logged-in platform
search now if [Your Name] is at their desk, and (ii) asking them to reply
naming which, if any, of the new opportunities to pursue. Wait for the
reply — this is the approval gate. Nothing in Step 4 happens without an
explicit reply naming specific opportunities.

STEP 4 — Draft on approval (never apply). When the reply names one or more
opportunities to pursue: flip that row's Decision to Pursuing in
tracker.xlsx, then immediately tailor and draft the resume + cover letter
package using the master profile — save under
Apply\applications\<Category>\CV\<Company - Role>\ (docx + pdf). Where the
application portal is a structured multi-page form, pre-fill only
safe/factual fields (name, contact info, employment history dates/titles,
education, certifications, language fluency, legal work authorization,
location — never compensation, notice period, relocation willingness,
voluntary personal disclosures, or open-ended narrative fields). Always
stop at a saved, reviewable, unsubmitted package or pre-filled-but-
unsubmitted form, and say clearly it's ready for review and manual
submission. If the reply instead (or also) asks for the logged-in platform
search, run it now (read-only, extract-only), log any new matches the same
way as Step 2, and summarize what was found.
