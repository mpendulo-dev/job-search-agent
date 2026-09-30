# CLAUDE.md

This file is a permanent briefing for Claude Code about the person it's working with in this repository.

## Who I'm working with

- Product Engineering Specialist, Consultant at Accenture
- Frontend-focused, full-stack capable — primary stack: Angular, React, TypeScript
- Currently staffed on a telecom client engagement: ~15-person team across 6 squads, billable to a single client at a time
- Leads frontend development for a sub-team of 5 (3 juniors, 2 intermediate devs)

## Goals

- Growing into the engineering lead role further — leveling up leadership and mentoring
- Upskilling in AI on two fronts: using AI tools/agentic workflows to build software faster, and building AI-powered features/products for clients
- Staying marketable as the industry shifts; open to certifications but hasn't picked one yet

## Pain points — where automation/help is wanted

- **PR reviews**: team standards are fixed and don't change, so reviewing against them manually/repeatedly is wasted effort — wants this checked systematically instead (e.g. via CI/lint rules) rather than by eye each time
- **Testing**: wants manual testing effort reduced through automation (team uses Jest)
- **Email overload**: important emails get missed when busy (uses Outlook and Gmail)

## Tooling in use

- Version control / CI: GitHub, GitHub Actions
- Testing: Jest
- Email: Outlook and Gmail

## How to work with me

- Short, direct answers — no padding or over-explaining
- If unsure about something, double-check with me rather than guessing or assuming

## Active project: job search agent

Location: [job-search-agent/](job-search-agent/). Daily-scheduled pipeline that searches, scores, and drafts tailored ATS CVs/cover letters for frontend roles, tracks applications in [job-search-agent/applications-tracker.xlsx](job-search-agent/applications-tracker.xlsx), monitors email for replies, and preps interviews. Full spec in [job-search-agent/workflow.md](job-search-agent/workflow.md), criteria in [job-search-agent/criteria.md](job-search-agent/criteria.md), base resume in [job-search-agent/master-cv.md](job-search-agent/master-cv.md).

**Hard rule**: never submit a real application, create an account, or enter credentials/EEOC data unattended — every application stops at "ready for review" for explicit per-job approval. See workflow.md's "Hard constraints" section.

Setup complete: Gmail connected, sources confirmed (LinkedIn + Indeed), criteria confirmed. Runs daily on schedule — see workflow.md's checklist.
