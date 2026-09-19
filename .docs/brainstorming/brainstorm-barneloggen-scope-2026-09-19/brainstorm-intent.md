# Barneloggen: scope intent (input for PRD)

Source: brainstorm session 2026-09-19 (`.memlog.md`), based on `Barneloggen_prosjektforslag.txt`.

## Context and constraints
- Responsive web app for parents to log a baby's routines, see them on a calendar, and get AI-assisted entry and summaries. IBE160 course project.
- Solo. Claude writes the code. Deadline mid-November 2026 (about 8 weeks from 2026-09-19).
- **Absolutes:** a working site and a pleasing design. **Completeness** affects the grade but is not absolute, so depth beats breadth.
- The scarce resource is the owner's review and testing time, not coding time.
- **No medical advice, ever.** AI only describes recorded observations. Enforced in feature design, AI instructions and response handling, not by disclaimer alone. Fictional data only during development.

## Scope: three tiers, nothing dropped outright

### Tier 1 - Core (finished and polished)
Every shipped feature means create, read, update, delete, validation, empty state and error state.
- Sign-in via OAuth or magic link, plus a one-click **Demo login**. Child profile (name, birth date, optional nickname, photo, comment). `child_id` on every entry.
- **Sleep:** start, end, computed duration, quality (calm / restless / not rated; unrated is never treated as calm). No overlapping sleep intervals for one child (touching endpoints allowed), cross-midnight handled. Other entry types may occur during sleep.
- **Meals:** types (breastfeeding, expressed milk, formula, solids, other) with type-specific fields. Own food catalog; several foods per meal via MealItem, optional amount and unit. Foods created on first use.
- **Diapers:** time, type (wet / stool / both), optional consistency, colour, comment.
- **Week calendar (hero screen):** seven days, time axis, sleep as blocks, other entries as non-overlapping markers or clickable groups, week navigation, child selection, type filter, day view on small screens. All entries open for detail and edit.
- Dashboard (today's totals, last meal, last sleep, shortcuts), history with filters, edit and delete, basic statistics computed in plain code.
- **AI meal entry:** a natural-language sentence becomes a draft in an editable confirm card shown beside the original text. Never saved without confirmation, never invents amounts or foods, reuses existing foods.
- Custom design system: warm, calm, colour-coded per entry type (sleep indigo, meals amber, diapers teal, growth green), mobile-first, human Norwegian microcopy, skeleton loaders, illustrated empty states.

### Tier 2 - Nice-to-have, built in this order after Tier 1 is stable (before ~1 Nov freeze)
1. **Growth:** date, weight and/or length; separate charts; no normal/abnormal judgement.
2. **AI trend analysis**, in steps: one sleep summary card, then per area (sleep, food, diapers, growth), then a whole-picture summary with week-on-week comparison. Backend computes stats and sends a limited structured packet; output states period, data basis and gaps; no causes, no norms, no advice; missing entries are not read as "did not happen".
3. **AI quick-add for every entry type** (one text or voice bar).
4. **AI food suggestions:** category, default unit, possible duplicates.
5. Multi-child switcher.
6. Food catalog management page.
7. Per-domain charts and period comparison.
8. Night mode, installable PWA, voice input (if not already delivered with the design system).

### Tier 3 - Planned future (documented in PRD, not built)
- Pumping, temperature, medication log (records only, no dosing advice), milestones, general notes.
- Summaries with clickable links into timeline entries.
- Multiple guardians per child.
- CSV / data export.
- Free-text questions to AI about the records (needs its own safety review).
- Regulatory review (EU medical device and privacy rules) before any public launch.

## Design-for-extension rules (keep Tier 3 cheap)
- One shared pattern for entry types so a new type is a small change.
- `child_id` on all entries; ownership modelled so shared guardian access can be added later.
- One shared query layer feeding calendar, history and statistics.
- AI works only from a structured stats packet and fills fixed schemas (schema-only output); no free-text answer path in Tier 1 or 2.
- Store times in UTC, one date utility, tests for cross-midnight logic.

## Delivery approach
- Deploy an authenticated empty app with design tokens in week 1. Main is always deployable; a five-minute Sunday demo check each week.
- Hard feature freeze about 1 November; weeks 7-8 are bug bash, polish, documentation, backup screenshots and recording.
- Seeded fictional dataset (about 4 weeks for one child) so every screen is demoable early.
- Boring, familiar stack (suggestion: TypeScript full-stack with a hosted Postgres, hosted auth). Project context file so every Claude session follows the same conventions.
- Tests only for the riskiest logic: sleep overlap and cross-midnight, AI output validation, and a guardrail set ("is this normal?" must always produce a non-advice reply).
- BMad planning artefacts, a short decision log and the prompt log double as evidence of method in the report; report includes a "Scope decisions" section.

## Risks and fallbacks
| Risk | Fallback |
|---|---|
| Calendar layout with overlaps and cross-midnight | Week grid, then day view, then grouped list; ship the level that is stable at freeze. Start from a restyled calendar library |
| AI safety or unavailability | Schema-only output, phrase scan on summaries, mock or cached AI for the demo |
| Timezone and midnight bugs | UTC storage, single date utility, dedicated tests |

## Open items
- Check what the examiner or rubric actually values before locking scope (about 15 minutes; could reshape priorities).
- Confirm the stack and hosting choice in the architecture step.
- Confirm UI language (Norwegian assumed).
