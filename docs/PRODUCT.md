# MooMinds: product and architecture assumptions

## Confirmed product direction

MooMinds is a free-to-use flashcard learning application. Reviews follow the classic five-box Leitner system. Users may opt in to study reminders by email or push notification.

Users can sign in with email and password, Google, or Discord. App-level TOTP two-factor authentication is supported. See the [authentication requirements](AUTH.md).

Users can publish their own learning courses, such as a course covering 2,000 common English words or algebraic identities. Other users can find and use these courses, rate them, and browse highlighted or top courses.

## Leitner review schedule

- MooMinds uses a chosen default interval schedule of **1, 2, 4, 8, and 16 days** for boxes one through five. These are product defaults, not a claim that every Leitner implementation uses the same dates.
- A correct answer moves a card to the next box, up to box five. An incorrect answer returns it to box one. A correctly answered card in box five remains in box five and becomes due again after that box's interval.
- A learner can change the five intervals in the settings of their own course copy. The intervals apply to that learner's progress in that copy; changing them does not alter the source course or anyone else's schedule.
- Changing intervals after learning has started does not move existing due dates. The new intervals apply after each card's next answer.
- When a learner edits one interval, the form suggests values for that box and later boxes by continuing the doubling pattern; earlier boxes stay unchanged. The learner may adjust every suggested value before saving.

## Study setup and session size

- Creating or publishing a source course is separate from studying it. The creator also starts a personal study copy to learn from their own course; source edits do not automatically change that copy.
- Before the first lesson from any personal copy, a short form lets the learner set the session size, the mix of new cards and reviews, and all five Leitner intervals. This happens once per study copy. Reminder preferences are configured separately.
- Each learner chooses their own settings; a copied course does not inherit its creator's learning intervals.
- The default session contains up to **20 cards**. When reviews are due, the target mix is **10 new cards and 10 due reviews**. If one group has too few available cards, the other group fills the remaining places. With no reviews due, up to 20 new cards can appear.
- Session size and mix can be changed in the personal copy's settings.

## Adding course content

- A course creator can add and edit flashcards through a form. A learner can also add or edit cards in their personal study copy without changing the source course.
- The initial card model has a prompt and an answer. Cards may include uploaded images; whether images belong on the prompt, answer, or both sides needs a UI decision.
- A creator or learner can import multiple flashcards from a **text-only CSV file**. The import flow should show a preview, allow column mapping, report invalid rows, and require confirmation before adding cards. CSV import does not upload images or fetch image references.
- After import, the user may open any imported card in the editor and attach an image separately.
- Uploaded files need type and size checks, safe storage and serving, and limits appropriate to the VPS. See [OWASP's file-upload guidance](https://cheatsheetseries.owasp.org/cheatsheets/File_Upload_Cheat_Sheet.html).

## Agreed community-course model

- A course has a creator and published versions. Editing a published course produces a new version rather than silently changing existing learners' copies.
- A learner makes a personal study copy of a course. This includes the creator when they want to study their own course. They may edit that copy, its flashcards, and its Leitner intervals. Their progress belongs only to them.
- The copy keeps a link to its source course and the source version from which it was made. When the creator publishes a new version, the learner may preview and optionally apply source changes. Updates are not automatic and must not silently overwrite local edits.
- An update is shown in one preview. The learner chooses which source changes to import; locally edited cards are kept unless the learner explicitly selects the source version for that card. Unchanged cards keep progress and new cards begin in box one.
- If an accepted update changes a card's prompt or answer, that card returns to box one. A minor description or metadata correction keeps its progress. Rules for deleted cards and ambiguous changes still need refinement. Stable logical card identities across versions help compare cards.
- A learner may publish their edited copy as a new course of their own, with a visible link to the source course. Publication rules for derivative content still need refinement.
- A course in the initial product scope has a title, description, creator, language or subject, and flashcards.
- The first search implementation uses [PostgreSQL full-text search with a GIN index](https://www.postgresql.org/docs/current/textsearch-indexes.html). [Trigram matching (`pg_trgm`)](https://www.postgresql.org/docs/current/pgtrgm.html) can be added if typo-tolerant search becomes useful.
- Top courses should consider both rating quality and the number of ratings. The exact ranking formula and eligibility rules remain to be agreed.

## Reminder channels

- The React and TypeScript GUI should be installable and usable as a progressive web app (PWA).
- Push reminders use Web Push for supported desktop browsers and mobile PWAs. On iOS/iPadOS, Web Push applies to web apps added to the Home Screen; browser and platform support must be checked before offering the channel. Email remains an alternative. See [WebKit's Web Push guidance](https://webkit.org/blog/13878/web-push-for-web-apps-on-ios-and-ipados/) and [MDN's service-worker overview](https://developer.mozilla.org/en-US/docs/Web/Progressive_web_apps/Guides/Offline_and_background_operation).
- Reminders remain opt-in. Timing, frequency, quiet hours, and time-zone rules still need refinement.

## Confirmed technology

| Component | Technology and responsibility |
| --- | --- |
| GUI | React and TypeScript |
| API | Java Spring Boot REST API |
| Worker | Java Spring Boot service for email and push notifications |
| API–Worker communication | RabbitMQ |
| Database | PostgreSQL |
| Deployment | Kubernetes on the project owner's VPS, with HPA |
| Secrets | Vault |

The [MooMinds backlog](https://github.com/Path-Of-Execution-Team/MooMinds/issues) tracks product and cross-component work. Component-specific implementation and bugs can be tracked in the API, GUI, and Worker repositories and linked to the product issues.

## Open decisions

- Whether another session can start immediately when more cards remain due after a full session.
- The exact CSV columns, duplicate handling, and row and file-size limits.
- Image placement on cards, supported formats, size limits, storage location, and accessibility text.
- Reminder timing, frequency, quiet hours, time zones, and fallback when Web Push is unavailable.
- User accounts and authentication, including how flashcards and preferences are associated with a user.
- Whether courses can also be private or unlisted, and whether they contain anything beyond flashcards.
- How deleted cards and ambiguous content changes are presented in the update preview.
- The rules for publishing a derivative course, including attribution and content permissions.
- The rating scale, rating eligibility, and the exact formula and presentation for top courses.
- Search filters, language handling, and how published courses are reviewed or reported.
- The MVP release boundary and quality targets.
- VPS capacity, off-server backups, restore objectives, and HPA limits. These are tracked as deployment work for later agreement.

These questions should be resolved during refinement before acceptance criteria and estimates are finalized.
