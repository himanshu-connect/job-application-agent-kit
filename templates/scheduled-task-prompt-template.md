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

DEVICE AVAILABILITY GATE — do this before anything else, including Step 0.
This whole run depends on [device] (the tracker files live there, and
platform search needs your own logged-in browser session). Confirm it's
actually reachable this firing: call a lightweight remote-devices tool
(e.g. get_device_info) once.
- If it succeeds (device connected): proceed to Step 0 below as normal —
  the rest of this prompt is unaffected.
- If it fails / no device is connected, check whether the text
  "[RETRY ATTEMPT" appears anywhere above this line in what you were
  given:
  - If it does NOT appear: this is the regular firing and the device
    isn't reachable. Send [Your Name] one short message saying the weekly
    run couldn't reach [device] at the scheduled time, so it's retrying
    once at [retry time, e.g. 4 hours later] today. Then call the
    create_trigger tool to schedule a one-time run: run_once_at =
    [retry time, converted to UTC], requires_local_device: true, name
    "[this task's name] — retry", and prompt = this entire prompt
    verbatim with a single new first line inserted: "[RETRY ATTEMPT — if
    the device is still unreachable now, skip this week's run entirely
    and do not schedule any further retry]". Then end this session
    immediately — do not run Step 0 or anything below it this firing.
  - If it DOES appear: this is that retry firing and the device is still
    unreachable. Send [Your Name] one short message saying this week's
    run is being skipped because the device wasn't reachable at either
    attempt, and that the normal schedule resumes next week. Then end
    this session immediately — do not schedule another retry, and do not
    run Step 0 or anything below it.
(This gate is optional but recommended once you've seen the plain version
work — it avoids a run silently failing partway through because the
device happened to be offline at the scheduled time.)

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

STEP 1 — Discovery. Use the Agent tool to spawn subagents in parallel —
one per track ([Track 1], [Track 2], [Track 3], [Track 4]) plus one
Platform Search subagent — rather than researching sequentially yourself.

(a) The track subagents run the career-page watch pipeline
(search-workflow.md), LIGHT depth only — one combined search query per
step, not an exhaustive multi-query sweep, to keep this sustainable within
search-quota limits over time. Each track subagent:
   1. Sweeps tracker.xlsx (Opportunities) and companies-to-explore.xlsx for
      rows added or edited since the last run that aren't fully processed
      yet (plus anything from Step 0) and that belong to its track.
   2. Discovers new companies not yet in companies-to-explore.xlsx that
      could plausibly be hiring for its track.
   3. Searches newly-added companies for current open roles matching its
      track, at the seniority floor defined in search-workflow.md.
   4. Runs one light general search for new matching postings in its
      track, independent of any specific company.
   5. Re-checks a sample (not all, to stay light) of companies already in
      companies-to-explore.xlsx for whether previously-noted open roles in
      its track are still live or have closed.
   Seniority floor, track-priority rules, and any noisy-source caveats are
   documented in search-workflow.md — follow them.

(b) The Platform Search subagent runs alongside the track subagents every
week: using Claude in Chrome against [Your Name]'s own already-logged-in
browser session, read-only, it searches [Your platforms, e.g. LinkedIn,
Indeed, etc.] for postings matching the tracks at the seniority floor
defined in search-workflow.md, and extracts candidate listings — search
and extract only, never click Apply, never log in on [Your Name]'s
behalf. If Chrome isn't reachable, or no session is logged in, this
subagent should fail gracefully and report that in its results — don't
block the other subagents or the rest of the run on it; just note in the
Step 3 digest that platform search couldn't run this week and why. (If you
haven't yet confirmed your browser session stays reliably logged in for
unattended runs, start by leaving this subagent out and running platform
search yourself on demand instead — fold it into Step 1 once you trust it.)

STEP 2 — Tracker update. Merge genuinely new findings from all Step 1
subagents into tracker.xlsx (new Opportunities rows, Decision=New) and
companies-to-explore.xlsx (new rows, or updated Status/notes), matching
the exact existing column headers, dropdown values, and formatting. Tag
each new row's Source appropriately (career-page watch vs. the specific
platform Platform Search found it on). Use openpyxl, run recalc.py after
edits (zero formula errors required), and commit back through the device
bridge with an mtime guard so you never clobber a concurrent edit. Do not
alter existing Pursuing-sheet rows other than reading them for the
follow-up check below. If the device isn't linked, or write-back fails,
don't block on it: save everything found into a new project doc via the
Projects tool instead, note the staged count in the digest, and merge it
in on a future run once the device is reachable.

STEP 3 — Digest & approval gate. Also read the Pursuing sheet and flag any
row where Next Follow-up is today or earlier with no status change since.
Then send [Your Name] one concise digest message covering: new companies
discovered, new matching roles found (company / role / link / how it was
found — career-page watch or platform search), previously-open roles now
closed, whether platform search ran this week (and why not, if it
didn't), any pending-merge count, and Pursuing rows due for follow-up. End
the digest by asking them to reply naming which, if any, of the new
opportunities to pursue. Wait for the reply — this is the approval gate.
Nothing in Step 4 happens without an explicit reply naming specific
opportunities.

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
submission.
