# MooMinds: product and architecture assumptions

## Confirmed product direction

MooMinds is a free-to-use flashcard learning application. Reviews follow the classic five-box Leitner system. Users may opt in to study reminders by email or push notification.

Users can publish their own learning courses, such as a course covering 2,000 common English words or algebraic identities. Other users can find and use these courses, rate them, and browse highlighted or top courses.

## Agreed community-course model

- A course has a creator and published versions. Editing a published course produces a new version rather than silently changing the version learners already use.
- A learner adds a published course to their library and studies a specific version. The learner's Leitner boxes, review dates, and results belong to that learner, independently of the creator and other learners.
- When a new version is published, the learner is offered an update and chooses whether to apply it. Updates are not automatic.
- After an accepted update, unchanged cards keep their learning progress and new cards begin in box one. The rules for removed or substantially changed cards still need refinement. Stable logical card identities across versions are needed to recognize unchanged cards.
- A course in the initial product scope has a title, description, creator, language or subject, and flashcards.
- The first search implementation uses [PostgreSQL full-text search with a GIN index](https://www.postgresql.org/docs/current/textsearch-indexes.html). [Trigram matching (`pg_trgm`)](https://www.postgresql.org/docs/current/pgtrgm.html) can be added if typo-tolerant search becomes useful.
- Top courses should consider both rating quality and the number of ratings. The exact ranking formula and eligibility rules remain to be agreed.

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

- Exact review intervals and when cards in each of the five Leitner boxes become due.
- Whether an incorrect answer always returns a card to box one, and how a card in box five is handled after a correct answer.
- Whether push means web push, mobile push, or both.
- How users opt in or out, choose channels, and set reminder times and time zones.
- User accounts and authentication, including how flashcards and preferences are associated with a user.
- Whether courses can also be private or unlisted, and whether they contain anything beyond flashcards.
- How removed or substantially changed cards affect a learner's progress during an accepted course update.
- The rating scale, rating eligibility, and the exact formula and presentation for top courses.
- Search filters, language handling, and how published courses are reviewed or reported.
- The MVP release boundary, quality targets, and VPS capacity assumptions for HPA.

These questions should be resolved during refinement before acceptance criteria and estimates are finalized.
