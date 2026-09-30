# Daily Job Search Agent — Runbook

This is the instruction set a scheduled run follows. Inputs: [master-cv.md](master-cv.md), [criteria.md](criteria.md), [applications-tracker.xlsx](applications-tracker.xlsx).

## Cloud execution notes

This runs as a cloud routine against a clone of `https://github.com/mpendulo-dev/job-search-agent`. The sandbox has no persistent browser login and no access to Mpendulo's local machine — read this section before the Hard Constraints below.

- Use whatever web search/fetch tools are available in the session to search Indeed and LinkedIn's public (no-login) job search results. Do not attempt to log into LinkedIn — there is no persistent session here, so LinkedIn coverage is best-effort only; Indeed is the primary source.
- Edit `applications-tracker.xlsx` with Python (`openpyxl`) — match the existing header row and the `Status` dropdown values already defined in the sheet.
- At the end of every run: `git add`, commit (short message describing what changed, e.g. "Daily run 2026-10-01: 4 new listings, 2 tailored"), and `git push` to `main` so Mpendulo sees results locally.
- The Gmail connector must be attached to this routine from https://claude.ai/code/routines (cloud sessions here can't see or attach claude.ai connectors) — if it's not attached yet, skip the Email Monitoring section for that run and note it in the commit message instead of failing the run.

## Hard constraints (never violate)

- Never create an account on any job board or ATS.
- Never enter a password to authenticate anywhere, or attempt to log into LinkedIn or any other site. If a source needs login, skip it and log it as "needs manual login" instead of prompting for or entering credentials.
- Never click final Submit/Apply on a real application. Every application package stops at "ready for review" and waits for explicit per-job approval from Mpendulo in chat.
- Never bypass a CAPTCHA or other bot-detection — skip that listing and log it.
- Never enter EEOC/demographic/government-ID data anywhere.

## Daily run

1. **Search**: check each source in [criteria.md](criteria.md) (Sources section) using the session's web search/fetch tools. Read listing pages, don't hammer sites with high-volume automated requests.
2. **Dedupe**: skip any listing already present in the tracker (match on company + title + posted date).
3. **Score**: apply the rubric in criteria.md to every new listing. Log every listing to the tracker with score + one-line reason, regardless of outcome.
4. **Tailor** (score 6+ only):
   - Read the full job spec.
   - Generate an ATS-compliant CV from master-cv.md: plain single-column layout, no tables/text-boxes/graphics, standard section headers (Summary, Skills, Experience, Education, Certifications), keywords from the job spec worked into the summary/skills/bullets truthfully (never fabricate skills, titles, or dates not present in master-cv.md).
   - Draft a short tailored cover letter (3–4 paragraphs: why this role, relevant proof points, why this company).
   - Save both into `job-search-agent/applications/<company>-<role-slug>-<date>/` alongside the original job spec text and the score breakdown.
   - Set tracker status = `ready for review` in [applications-tracker.xlsx](applications-tracker.xlsx).
5. **Never submit.** Stop there for that listing.

## Email monitoring (requires Gmail/Outlook connector)

- Check inbox daily for replies matching tracked applications (sender domain or subject matching company/role in the tracker).
- On match: update tracker status (`rejected`, `interview requested`, `assessment requested`, `no response yet`) and summarize the email content next to it.
- On an interview/assessment request: immediately kick off **Interview Prep** (below) rather than waiting for the weekly report.

## Weekly report (Mondays, covering the prior 7 days)

Summarize and share (update applications-tracker.xlsx + chat):
- New listings found / scored / tailored / submitted (by Mpendulo) this week
- Current status of every open application
- Any replies received and what they need
- Sources that returned nothing useful (flag for criteria/source review)

## Interview prep (triggered by a positive reply)

Produce, per interview:
- **Org research**: what the company does, recent news/product launches, funding/size, engineering culture signals (tech blog, Glassdoor themes, public tech stack if discoverable)
- **Role research**: re-read the original job spec against master-cv.md, identify the 3–5 gaps/strengths to address proactively
- **Scorecard**: a one-page prep scorecard — likely interview stages, competencies being assessed, matching proof points from experience, and 2–3 likely technical/behavioral questions per stage with a suggested angle to answer from

## Setup status

- [x] Gmail connected (2026-09-30) — email monitoring active
- [x] Sources confirmed: LinkedIn + Indeed
- [x] Seniority/location assumptions confirmed
- [x] Tracker: [applications-tracker.xlsx](applications-tracker.xlsx)
