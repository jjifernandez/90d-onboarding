# Agent instructions — 90-day onboarding

This repository holds **living 90-day onboarding plans** for new engineering hires. It is not an application. Do not add product code, infra, or secrets here.

## Purpose

Keep a hire-facing plan that states:

- Who the hire reports to, who the onboarding buddy is, and who to go to for what
- Operating expectations for the first 90 days
- Week 1, month 1, month 2, and month 3 goals and deliverables
- Day-90 success criteria and stretch expectations

The reader is the new hire. Write in second person. Do not turn the plan into a third-person status report about them.

## Layout


| Path                      | Role                                                                    |
| ------------------------- | ----------------------------------------------------------------------- |
| `README.md` / `AGENTS.md` | Human and agent docs                                                    |
| `docs/90-day-plan.md`     | Current hire's 90-day plan (Juan Jose Iguaran Fernandez, Machine Learning Engineer, start Sep 21, 2026) |
| `docs/meeting-logs.md`    | Onboarding meeting notes. Newest first. |


Hiring drafts are generated into the interviews repo (`roles/<role>/candidates/<slug>/90-day-plan.md`). This repo is the working copy after the hire accepts. Do not move scorecards, transcripts, or offer prep here.

## Working rules

**Do not fabricate facts.** Names, start dates, managers, buddies, work hours, customers, repos, and success criteria must come from the user, a transcript, or an existing file. If a field is unknown, leave it blank or write `TBD`. Do not invent a plausible value.

**Preserve the plan's structure.** Keep welcome, who-to-go-to, operating expectations, the 90-day objective, staged week/month sections, and day-90 success criteria. Do not freehand a new outline unless the user asks.

**Edit, do not silently rewrite history.** After the hire has started, change dates, owners, or success criteria only when asked. Typo and link fixes are fine. Do not soften expectations or drop deliverables on your own.

**Link out instead of copying.** PRDs, test repos, and CI/CD work live in other repos. Point at them. Do not paste a PRD or a codebase tour into this repo.

**Do not commit secrets.** No credentials, tokens, customer PII, or live backend files.

**Do not add application code.** No test suites, pipelines, Terraform, or product features. This repo is the plan, not the work the plan describes.

## How to update a plan

1. Read `docs/90-day-plan.md` (or the plan the user named).
2. Change only what the user asked for. Keep surrounding tone and section order.
3. If adding a second hire, put their plan under `docs/` with a filename that identifies the person and role, then add a row to the README table. Do not overwrite the existing plan.
4. Keep mermaid timelines in sync with the month sections when you change deliverables.

## How to add a meeting log

1. Open `docs/meeting-logs.md`.
2. Insert a new `## YYYY-MM-DD: Meeting title` section **below the file intro and above every older log**. Do not append at the bottom.
3. Include **When** and **Attendees** when known. Use checkboxes for next steps, with an owner.
4. Do not rewrite older logs. Typo and link fixes in the new entry are fine.
5. Do not invent attendees, quotes, or action items. If unknown, omit the field.
