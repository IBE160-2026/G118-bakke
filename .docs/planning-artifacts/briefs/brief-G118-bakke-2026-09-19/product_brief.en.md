---
title: "Product Brief: Barneloggen"
status: final
created: 2026-09-19
updated: 2026-09-19
language: en
translation_of: product_brief.md
---

# Product Brief: Barneloggen

## Executive Summary

Barneloggen is a responsive web application where parents quickly log their child's sleep, meals and diaper changes, see them together in a weekly calendar, and get help from AI to record and summarise. The AI never gives medical advice. It is a solo project in IBE160 (Programming with AI), developed with AI as a coding assistant and due by mid-November 2026.

The background is personal. The author is the parent of a nine-month-old and mostly logs sleep and meals. Barneloggen is tested daily on the author's own child.

This brief is the basis for further work (PRD, architecture, epics). In the longer term, outside this project, the ambition is a full application for tracking children's growth and development.

## The Problem

Parents of small children have to remember and compare a lot: when the child slept, for how long, what it has eaten and when new foods were introduced. Without a simple tool this becomes notes and guesswork, and it is hard to see patterns from day to day and week to week.

At nine months the child is moving on to solid food, and it becomes important to know which foods the child has had, how often, and when they were first introduced.

## The Solution

A web application for mobile, tablet and PC, built around fast logging and a clear overview.

- **Logging:** sleep (with quality and rules against overlapping sleep, including across midnight), meals (with your own food catalogue and several foods per meal) and diaper changes (with colour and consistency).
- **Overview:** a weekly calendar with seven days side by side, a dashboard, history and simple statistics.
- **AI as a helper, not an adviser:** the user types a sentence such as "Emma ate half a banana and some oat porridge at 10 o'clock", and the AI proposes structured fields in a draft the user confirms. The AI never saves anything itself and does not invent amounts or foods.
- **No medical advice:** the AI only describes recorded observations. The limit is built into feature design and response handling, not just a disclaimer.

## What Makes This Different

There is no technical moat. The strength lies in:

- **Focus where the usage is:** sleep and meals get the most quality. Diapers are included so the app is complete for most parents.
- **Food catalogue and first foods:** you can see which foods the child has had, how often and when they were first logged.
- **Safe AI by construction:** the AI only fills in a fixed schema that the user confirms, with no free-text route that could drift into advice.
- **Tested on a real child** in everyday life, not only against a requirements list.

## Who This Serves

**Primary user and test user:** the author, a parent of a nine-month-old, who logs several times a day, often one-handed and short on time, and wants to see patterns over weeks.

**Wider audience:** parents and guardians of small children. The data model supports several child profiles per user from the start, while switching between children in the interface comes in tier 2. Shared access for several guardians is a later extension.

## Scope

Three tiers, with no hard cuts:

- **Tier 1, core (finished and polished):** login (including Demo login) and child profile, sleep, meals with a food catalogue, diapers, weekly calendar, dashboard, history with editing and deletion, simple statistics, AI-assisted meal logging and a custom design system.
- **Tier 2, nice to have, in priority order:** growth logging; AI summaries and trend analysis (first sleep, then per area, then an overall picture with week-on-week comparison); AI logging for all entry types; AI suggestions for foods; switching between children; a food catalogue page; more charts; night mode, PWA and voice input.
- **Tier 3, planned for later:** pumping, temperature, medication log, milestones, notes; several guardians; data export; free-text questions to the AI (needs its own safety review); assessment of medical-device regulation and privacy before any public launch.

Out of scope: anything that gives medical assessments, diagnoses or dosage advice.

## Success Criteria

**For the user (tested on the author's own child):**
- The user can log sleep or a meal in under 10 seconds, one-handed, on mobile.
- The user sees last week's sleep and meals in the weekly calendar at a glance.

**For the project:**
- Tier 1 is finished and polished in a published version by the feature freeze around 1 November, and a demo of about three minutes runs without errors on fictional data.
- Overlapping sleep is rejected in every test case, including across midnight.
- AI meal drafts are correct or need at most one correction in at least 8 of 10 test sentences.
- A fixed test set ("is this normal?") always gets an answer without assessment or advice.
- The design is tidy and pleasant, including on mobile.

## Privacy and Data

Development and demo use fictional data. The author also uses their own child's real entries for testing. Therefore:

- One application with two separate accounts: a demo account filled with fictional data (Demo login) and the author's own account with real data. Server-side access control keeps them apart, and the Demo login never gives access to the other account.
- Real data stays out of source code and seed data.
- API keys are not exposed in the frontend.
- AI calls send only what is needed (no name, photo or date of birth), and the provider's terms on data retention and training are checked.

## Open Questions

- Technology choice and hosting are settled in the architecture phase.
- Choice of AI provider, based on its terms for data retention and training.

## Vision

If the project succeeds, Barneloggen becomes the foundation for a full application for tracking children's growth and development: all entry types, shared access, data export and safe, descriptive AI summaries over time. That requires its own assessment of privacy and regulation before any public launch and lies outside this project.
