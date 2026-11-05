# MooMinds release roadmap

Milestones describe release goals, not sprints. The order below is a proposed delivery sequence, with no promised dates or estimates. Issues remain in the central [product backlog](https://github.com/Path-Of-Execution-Team/MooMinds/issues); implementation work in component repositories should link to those issues. The team can refine scope before a sprint without changing the product requirements in [PRODUCT.md](PRODUCT.md).

## M1 — MVP: Study and Share

**Goal:** A user can create or find a text-based course, make a personal study copy, and complete repeatable five-box Leitner sessions on the deployed application.

The first release includes:

- Email/password sign-up, sign-in, and password recovery.
- Course and flashcard creation through a form, text-only CSV import, publication, and basic search of published courses.
- A personal, editable study copy for any course, including one the learner created. Source edits never silently change a study copy.
- One-time study setup per copy, the agreed 20-card default and 10-new/10-due target when reviews exist, configurable intervals, and simple multiple-choice and hard typed-answer modes.
- Five-box scheduling and progress persistence. Both modes use the same scheduling rules.
- A usable React/TypeScript PWA, Spring Boot API, PostgreSQL, and a repeatable Kubernetes deployment on the VPS. Vault-backed secrets, a capacity decision, backups, and a tested restore are release gates. HPA configuration and its resource limits must be checked against the actual VPS capacity.

**Release check:** The team can run the create → publish → find → copy → configure → study → return for a due review journey on the deployed system; account recovery works; data survives redeployment and a backup restore; core access, privacy, and failure paths have been checked. The exact test evidence and performance targets are decided in issue #6.

## M2 — Community and Content

**Goal:** Learners can discover trusted courses, maintain an edited copy when its source changes, and enrich cards with images.

This milestone adds course ratings and top-course discovery, optional source-update previews with explicit conflict choices, publication of a derivative course with attribution, and image attachments through the card editor. Moderation, ranking, image storage, and update-conflict rules are refined before implementation.

## M3 — Reminders and Sign-in Options

**Goal:** Learners can choose reminder channels and additional sign-in methods without losing control of their accounts.

This milestone adds opt-in email and Web Push reminders through the Spring Boot Worker and RabbitMQ, Google and Discord sign-in, optional authenticator-app TOTP, account linking, and recovery codes. Reminder timing, consent, queue delivery, and account-recovery rules need decisions before implementation.

## Planning rules

- These milestone boundaries are a planning proposal. The team confirms them in issue #6 and may split large stories during refinement.
- Milestones track release outcomes across all four repositories. GitHub Project iterations, once available, track short sprints. A story is assigned to a sprint only after refinement and team estimation.
- No dates, assignees, or Fibonacci points are implied by this roadmap.
- A design decision is recorded in a short decision record linked from its issue before dependent implementation work starts.
