# MooMinds: product and architecture assumptions

## Confirmed product direction

MooMinds is a free-to-use flashcard learning application. Reviews follow the classic five-box Leitner system. Users may opt in to study reminders by email or push notification.

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
- The MVP release boundary, quality targets, and VPS capacity assumptions for HPA.

These questions should be resolved during refinement before acceptance criteria and estimates are finalized.
