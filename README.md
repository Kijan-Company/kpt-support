# Kijan Personal Tracker — User Feedback & Support

This repository is the **central ticket store** for user feedback, bug reports,
feature requests, and support questions about Kijan Personal Tracker (KPT).

## Channels (intake)

| Channel      | Audience     | Where                                | Submission flow                          |
|--------------|--------------|--------------------------------------|------------------------------------------|
| **Web form** | End users    | https://kijan.ch/feedback.html      | Opens GitHub Issue Form for the chosen category |
| **GitHub**   | Contributors | https://github.com/Kijan-Company/kpt-support/issues/new/choose | Native UI, all 4 templates available |
| **Email**    | End users    | contact@kijan.ch                     | Manually triaged into issues by maintainers |

The web form is a static page in `KijanPersonalTracker/kpt-website/feedback.html`.
It does **not** host any server-side code: each submit button opens a deep link
to this repo's GitHub Issue Form for the matching category (`bug`, `feature`,
`question`, `feedback`). The form is configured via `feedback-config.js` so the
repo URL is editable in one place.

## State machine

Every issue carries labels that encode both **status** and **category**.
Maintainers move issues through the state machine by adding / removing status
labels.

```
   new ─intake─▶ triage ─▶ in-progress ─▶ resolved ─▶ closed
                    │            │             │
                    └── needs-info (re-triage when user replies)
```

- **intake** — auto-applied by every Issue Form template. Indicates the issue
  was captured through the support pipeline and has not yet been triaged.
- **triage** — a maintainer is reviewing and assigning priority / category.
- **in-progress** — work has started.
- **needs-info** — waiting on the reporter for clarification.
- **resolved** — fix shipped (or answer provided). Repo auto-closes after 7 days.
- **closed** — terminal state. Auto-close will leave a confirmation comment.

## Categorisation

- `bug` — defect, crash, wrong behaviour
- `feature` — request for new functionality
- `question` — usage / installation / configuration help
- `feedback` — UX, performance, accessibility, ideas, anything else
- `complaint` — service / process complaint (rare)
- `documentation` — doc gap that doesn't fit a bug report
- `security` — security disclosure (also report via contact@kijan.ch)

## Routing by component

`comp:<area>` labels route issues to the right maintainer:

| Label            | Owner            |
|------------------|------------------|
| `comp:website`   | kpt-website      |
| `comp:web-dashboard` | dashboard repo |
| `comp:backend`   | KPT backend      |
| `comp:ciq-app`   | Garmin Connect IQ|
| `comp:symptoms-app` | Expo app      |
| `comp:other`     | unassigned       |

## Priority / severity

| Label       | When                                    |
|-------------|-----------------------------------------|
| `priority:p0` / `sev:critical` | Production outage, data loss, security |
| `priority:p1` / `sev:high`     | Major feature broken, no workaround    |
| `priority:p2` / `sev:medium`   | Major feature broken, workaround exists |
| `priority:p3` / `sev:low`      | Cosmetic, minor, nice-to-have          |

## Source tracking

Every submission is tagged with the channel it arrived through:

- `src:web`     — feedback.html form
- `src:github`  — direct issue on this repo (contributor / GitHub user)
- `src:email`   — manually triaged from contact@kijan.ch
- `src:telegram` — manually triaged from Telegram

## SLAs (response / resolution)

Configured via process document — see `docs/SUPPORT-PROCESS.md` in
`KijanPersonalTracker` repo (linked from the doc site once published).

| Severity | First response | Resolution target |
|----------|----------------|-------------------|
| critical | 4 hours        | 24 hours          |
| high     | 1 business day | 1 week            |
| medium   | 3 business days| 2 weeks           |
| low      | 1 week         | next release      |

## Automation hooks

- `.github/ISSUE_TEMPLATE/*.yml` — the 4 Issue Form templates that the web form
  links to. Edit these to change the structured questions users see.
- (Future) GitHub Actions can auto-apply `intake`, route by `comp:*` label,
  close `resolved` issues after 7 days, and post SLA reminders.

## Contact

- Email: contact@kijan.ch
- Telegram: @Hermy_Channel
- Privacy-sensitive reports: contact@kijan.ch with subject `private`
