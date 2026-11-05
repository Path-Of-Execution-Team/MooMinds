# Scrum in MooMinds

## Source of truth

The [organization GitHub Project](https://github.com/orgs/Path-Of-Execution-Team/projects/10) is the central work board for MooMinds, API, GUI, and Worker. Product stories and cross-component decisions live as [MooMinds issues](https://github.com/Path-Of-Execution-Team/MooMinds/issues). Component-specific implementation issues and bugs can live in the relevant component repository and should link to their product issue.

The Project has Status (Backlog, Doing, Pull Request, Testing, Done), Story points (number), and Sprint (two-week iteration) fields. Its [Board view](https://github.com/orgs/Path-Of-Execution-Team/projects/10/views/6) groups work into those five status columns; other views are All work, Backlog, Current sprint, Roadmap, and Done. Release milestones are defined in [ROADMAP.md](ROADMAP.md) and are separate from sprints. Three provisional two-week iterations begin on 9 November, 23 November, and 7 December 2026. The team can adjust the cadence and dates before its first sprint; no issue has been assigned to a sprint. New issues must be added to the Project during refinement; linking a repository does not automatically add every new issue.

## Working rhythm

1. **Refinement:** clarify the user goal, acceptance criteria, dependencies, and component ownership. Split large stories and keep them in Backlog until work starts.
2. **Planning Poker:** each team member selects a Fibonacci card privately; reveal together, discuss differences, and vote again if needed. Record only the agreed estimate in Story points. The scale is 1, 2, 3, 5, 8, 13; `?` means more refinement is needed. Split work estimated above 13. Points represent relative effort and uncertainty, not hours or individual performance.
3. **Sprint planning:** select refined issues based on team capacity and a sprint goal, then assign the Sprint field. Do not fill an iteration with the entire release milestone.
4. **During the sprint:** move started work to Doing, then Pull Request when a change is submitted for review. Link the pull request to its issue and note blockers there.
5. **Testing and review:** move a reviewed change to Testing, show the working result, check its acceptance criteria, and move it to Done only after acceptance.
6. **Retrospective:** use the retrospective issue template, capture specific improvements as issues, and inspect them in the next sprint.

## Planning Poker integration

A team can use an external simultaneous-vote Planning Poker room with links to GitHub issues and then record the consensus in Story points. Choose a tool together before installing a GitHub App or granting repository access. A deeper automated integration needs a tool choice and organization authorization; the current workflow requires no additional app permissions.
