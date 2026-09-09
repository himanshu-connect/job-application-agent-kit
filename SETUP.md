# First-Time Setup & First Run Guide

This guide walks through setting this system up for the first time, then running it once, end to end, before you consider it "done." It assumes you have all the files in this repo: `README.md`, `templates/project-instructions-template.md`, `templates/search-workflow-template.md`, `templates/scheduled-task-prompt-template.md`, `spreadsheets/tracker-template.xlsx`, and `spreadsheets/companies-to-explore-template.xlsx`.

## Before you start

You'll need:

- A Claude account with access to Projects (claude.ai) or Cowork.
- Your resume or CV, and your LinkedIn profile if you have one — the raw material for your master profile.
- A short list of the career tracks or categories you're targeting (2–5 is typical — e.g. "Backend Engineering" and "Product Management," or a single track if you're focused).
- Optional: the Claude desktop app, if you want Claude to read and write your tracker spreadsheets directly on your computer rather than you uploading/downloading them each time.

## Part 1 — First-time setup

1. **Create a Project.** In claude.ai, create a new Project for your job search (e.g. "My Job Search"). This is where the instruction docs and your master profile will live so Claude can find them in any conversation, including scheduled runs.
2. **Give Claude your background.** Paste your resume, LinkedIn profile, and any specific achievements you want represented (numbers, scope, team sizes, outcomes) into a chat inside that Project. Ask Claude to build a master profile document from it. Be explicit that nothing should be invented — tailoring should only reorder and reword what's real.
3. **Pick your tracks.** Decide the categories you're searching across. Write them down — you'll enter them in a moment.
4. **Customize the two instruction docs.** Open `templates/project-instructions-template.md` and `templates/search-workflow-template.md`. Replace every `[bracketed placeholder]` with your own name, folder path, and tracks. Add both as docs inside your claude.ai Project (or save them as files in your project folder if you're working locally — either works).
5. **Set up the tracker workbooks.** Open `spreadsheets/tracker-template.xlsx` and `spreadsheets/companies-to-explore-template.xlsx`. Each has a **Config** sheet — replace "Track 1," "Track 2," etc. with your real track names, and edit the Company Types and Sources lists to match how you'll actually categorize things (see the platform list below for Sources ideas). Every dropdown in the workbook reads from this Config sheet automatically, so you only edit it once per file.
6. **Connect your folder (optional but recommended).** If you're using the Claude desktop app, connect the folder where you're keeping these files. This lets Claude read and update your tracker directly instead of you re-uploading it after every change, and is required if you plan to use the weekly scheduled task later.

## Part 2 — Run it once, start to finish

Don't consider setup complete until you've walked through one real cycle. This confirms the pieces actually talk to each other before you rely on it.

1. **Research one real company.** In chat, name a company you're actually interested in. Confirm Claude fills in a row in Companies to Explore — career page, industry, size, open roles, culture notes — and sets Status to Researched.
2. **Feed it one real job posting.** Paste an actual job description — either from that company or any other — and ask Claude to log it. Confirm a new row appears in `tracker.xlsx`'s Opportunities sheet with Decision = New, and that the Category, Company Type, and Source dropdowns show your customized options rather than the placeholder ones.
3. **Ask for a tailored resume and cover letter.** Tell Claude you want to pursue that role. Confirm it flips Decision to Pursuing, then produces a tailored resume and cover letter built from your master profile — read them and check every claim traces back to something real in your background. This is the single most important check in the whole system.
4. **Confirm the guardrail.** Verify Claude stopped at a saved, reviewable draft — it should not have attempted to submit anything anywhere, created any account, or clicked Apply on your behalf, even if the posting had a direct-apply link.
5. **Log a real application (when you actually apply).** Once you submit that application yourself, tell Claude you applied. Confirm it adds a row to the Pursuing sheet with Status = Applied, Date Applied = today, and a working Next Follow-up date exactly 7 days later, and that the source Opportunities row got a cross-reference note.
6. **Optional: dry-run the weekly automation.** If you set up the scheduled task from `templates/scheduled-task-prompt-template.md`, you can fire it manually once to see the check-in message, the digest format, and the approval-gate behavior before trusting it to run unattended on schedule.

## Setup complete — checklist

- [ ] Master profile document exists and reflects your real background, with no invented details.
- [ ] `project-instructions.md` and `search-workflow.md` are customized — no `[bracketed placeholders]` remain.
- [ ] Both workbooks' Config sheets reflect your real tracks, company types, and sources.
- [ ] At least one company is logged in Companies to Explore.
- [ ] At least one role is logged in Opportunities, and you've seen a tailored resume/cover letter produced from it.
- [ ] You've confirmed Claude stopped at a draft and did not attempt to submit anything.
- [ ] If applicable: the weekly scheduled task is set up and you've seen at least one digest or dry run.

## Appendix — Job platforms reference

A working list of platforms to consider for your Sources list and the `search-workflow.md` platform section. Coverage varies a lot by region and industry — use what's actually relevant to your job search, not the whole list. Verified current as of 2026; a couple of well-known names have changed (AngelList's jobs product is now Wellfound; Monster India is now Foundit; Otta was absorbed into Welcome to the Jungle), and at least one prior major platform (Hired.com) has shut down and is intentionally left off.

| Platform | Category | What it's for |
|---|---|---|
| LinkedIn Jobs | General / Global | The broadest general-purpose job board and professional network; strong for recruiter visibility and referrals as well as listings. |
| Indeed | General / Global | Large aggregator pulling listings from many company sites and boards; good breadth, variable listing quality. |
| Glassdoor | General / Global | Job board plus company reviews and salary data; useful for researching a company alongside its openings. |
| ZipRecruiter | General / US | General-purpose US job board with employer-side matching. |
| Dice | Tech / US | US tech- and IT-focused job board, popular for contract and engineering roles. |
| Built In (builtin.com) | Tech / Startup / US | US tech and startup jobs with city-specific hubs (Built In NYC, Built In LA, etc.) and company culture content. |
| Wellfound | Startup / Global | Startup-focused hiring platform (formerly AngelList Talent, now a separate company/brand). |
| Handshake | Early Career | Campus recruiting platform connecting students/recent grads with employers. |
| RemoteOK | Remote | Remote-only job board across tech, design, marketing, and more. |
| We Work Remotely | Remote | One of the largest dedicated remote-job boards, broad category coverage. |
| Welcome to the Jungle | Startup / Culture / Europe | Startup and scale-up jobs with a strong culture/employer-branding angle (absorbed the former "Otta"). |
| Naukri.com | India | India's largest general-purpose job portal, owned by Info Edge. |
| Instahyre | India / Tech | India tech-hiring platform with recruiter-matching features. |
| IIMJobs | India / Management | India platform geared toward management, finance, and consulting roles (Info Edge-owned). |
| Hirist | India / Tech | India tech-focused job board (Info Edge-owned). |
| Cutshort | India / Tech | India tech talent and hiring platform, skills-driven matching. |
| Foundit | India / APAC / MEA | General-purpose job and talent-management platform (formerly Monster India/APAC/Middle East, rebranded 2022). |
| Talent500 | India / GCC recruiting | Recruiter-matching platform connecting vetted tech talent (mostly India-based) with Global Capability Centers and global employers — not a self-serve board; you're matched rather than applying directly in most cases. |
| Jobright.ai | AI-native | Newer AI-driven job-matching platform with an "autopilot" application assistant; the most-discussed AI-native entrant as of 2026 — evaluate carefully, since "auto-apply" features can conflict with the review-before-submit principle this system is built around. |
| Michael Page / Randstad / ManpowerGroup | Recruitment Agency / Global | International staffing and executive-search firms with a strong India presence; work mid-to-senior placements across finance, tech, sales, and leadership roles. |
| ABC Consultants / TeamLease / CIEL HR | Recruitment Agency / India | India-founded staffing and executive-search firms — ABC Consultants (leadership hiring, since 1969) and TeamLease and CIEL HR (staffing, RPO, and talent-advisory work) are among the longest-established. |

> **A note on "AI-native" auto-apply tools:** they're worth naming here specifically because they can work against this system's core principle — several market themselves on submitting applications automatically on your behalf. If you use one for discovery, keep its auto-apply features switched off and route anything worth pursuing back through your own tailoring-and-review step instead.

> **A note on recruitment agencies:** these work differently from the platforms above. You typically register or submit your resume once, and a recruiter matches you to roles behind the scenes, rather than you finding and applying to a specific posting yourself. This system's usual workflow — log a posting, tailor a resume to its JD, track it — doesn't map cleanly onto that; treat an agency placement more like a company you're exploring than a tracked job posting, and log outcomes in `companies-to-explore.xlsx` or as manual notes rather than forcing it into the Opportunities sheet.

## A closing reminder

The mechanics here — spreadsheets, dropdowns, a scheduled task — are just plumbing. The two rules that actually matter are: never let it invent something about you that isn't true, and never let it submit anything without you seeing it first. Everything else in this kit exists to make those two rules easy to follow consistently, not to work around them.
