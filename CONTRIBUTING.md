# Development Workflow & Git Conventions

A standards guide to maintain a consistent workflow, facilitate collaboration, and ensure traceability between tickets, branches, commits, and Pull Requests.

## 1. Purpose

This document defines the conventions the team must follow when working with Git, developing new features, fixing bugs, or maintaining the project.

The main rule is that every change must have an identifiable purpose, an associated ticket, a dedicated branch, descriptive commits, and a Pull Request that can be reviewed before being merged.

## 2. General Conventions

| Element | Convention | Language |
|---|---|---|
| Tickets | `TYPE-123: Short description` | English recommended |
| Git branches | `prefix/TYPE-123-short-description` | English |
| Commits | Conventional Commits | English |
| Pull Requests | `[TYPE-123] Short description` | English |
| Programming classes | `PascalCase` | English |
| CSS/HTML class names | `kebab-case` | English |
| Methods and variables | `camelCase` | English |

## 3. Branch Naming

### Format

```text
prefix/TICKET-ID-short-description
```

Example:

```text
feature/PROJ-123-user-authentication
```

### Allowed prefixes

| Prefix | Purpose | Example |
|---|---|---|
| `feature/` | New feature | `feature/PROJ-123-user-profile` |
| `bugfix/` | Non-urgent bug fix | `bugfix/PROJ-124-invalid-email` |
| `hotfix/` | Critical production fix | `hotfix/PROJ-125-payment-failure` |
| `refactor/` | Internal restructuring with no intended functional changes | `refactor/PROJ-126-auth-service` |
| `test/` | Add or fix tests | `test/PROJ-127-user-service-tests` |
| `docs/` | Documentation | `docs/PROJ-128-api-documentation` |
| `chore/` | Maintenance, dependencies, or configuration | `chore/PROJ-129-update-dependencies` |
| `perf/` | Performance improvements | `perf/PROJ-130-optimize-query` |
| `build/` | Build or packaging changes | `build/PROJ-131-update-build-config` |
| `ci/` | CI/CD pipelines and automation | `ci/PROJ-132-github-actions` |
| `revert/` | Revert previously merged changes | `revert/PROJ-133-remove-payment-change` |

### Rules

1. Use a valid prefix from the table.
2. Include the ticket identifier.
3. Write the description in English.
4. Use `kebab-case`: lowercase words separated by hyphens.
5. Do not use spaces, accents, or special characters.
6. Keep each branch linked to a single work ticket.
7. Create the branch from the base branch required by the project's workflow.

**Correct:**

```text
feature/PROJ-245-password-reset
```

**Incorrect:**

```text
newFeaturePassword
PROJ-245
feature/password reset
fix/245
```

Use `bugfix/` for regular bug fixes; reserve `hotfix/` for critical production issues.

### Base branch

- `main`: stable code or code ready for production.
- `develop`: feature integration, if the project uses this branch.
- `feature/*`, `bugfix/*`, etc.: temporary working branches.

If the team uses GitHub Flow, it can work directly from `main` without maintaining a `develop` branch. Hotfixes must branch off the branch representing the production version affected by the issue.

## 4. Tickets

Each ticket must represent a clear, verifiable, and sufficiently scoped objective so it can be developed and reviewed.

### Ticket template

```markdown
# [TYPE-123] Short and descriptive title

## Type
Feature / Bug / Refactor / Task / Documentation / Technical Debt

## Summary
Briefly describe what needs to be implemented or corrected and why.

## Context
Explain the business or technical context behind the request.

## User Story
As a [user or role],
I want [functionality],
so that [expected benefit].

## Scope
- Describe what is included.
- Describe the expected behavior.
- Identify relevant modules or services.

## Acceptance Criteria
- Given [initial context], when [action], then [expected result].
- Given [initial context], when [action], then [expected result].
- Relevant error scenarios are handled.
- Automated tests are added or updated where applicable.

## Technical Notes
- Relevant architecture or implementation details.
- Dependencies, API contracts, or database changes.
- Security, performance, and compatibility considerations.

## Out of Scope
- Explicitly list what this ticket will not cover.

## Dependencies
- Related tickets, services, or external requirements.

## Definition of Done
- [ ] Implementation completed.
- [ ] Automated tests pass.
- [ ] Code follows project conventions.
- [ ] Pull Request approved.
- [ ] CI checks pass.
- [ ] Documentation updated when necessary.
```

### Ticket rules

- A ticket must have a single objective; do not combine unrelated features.
- The title must describe the expected outcome.
- Acceptance criteria must be verifiable.
- Every ticket must have a unique identifier, for example, `PROJ-123`.
- Specify what is out of scope.
- Indicate the work type and priority according to the conventions of the project management tool.

Examples:

- `[PROJ-123] Implement password reset flow`
- `[PROJ-124] Fix invalid email validation`
- `[PROJ-125] Refactor authentication service`

## 5. Relationship Between Tickets and Branches

The general convention is **one development ticket per main working branch**.

Example of traceability:

```text
Ticket:
PROJ-123 — Implement password reset

Branch:
feature/PROJ-123-password-reset

Commits:
One or more commits related to the ticket

Pull Request:
[PROJ-123] Implement password reset

Merge:
Integration into the corresponding base branch
```

Rules:

- Each implementation ticket has a dedicated branch.
- The branch must not contain changes unrelated to the ticket.
- A branch can contain multiple commits.
- The standard workflow expects one Pull Request per ticket.
- Do not create multiple parallel branches for the same objective unless there is a technical justification.

### Exceptions

Exceptions are allowed when:

- A task is split into subtasks with independent deliverables.
- A feature requires coordinated changes across multiple repositories.
- A parent ticket groups several technical tasks.
- A temporary integration branch is needed.

Whenever possible, create specific tickets for each deliverable and link them to the parent ticket. Each implementation ticket keeps its own branch.

## 6. Conventional Commits

All commit messages must be written in English and follow this format:

```text
type(scope): imperative description
```

Example:

```text
feat(auth): add password reset endpoint
```

### Commit types

| Type | Purpose | Example |
|---|---|---|
| `feat` | New feature | `feat(users): add profile endpoint` |
| `fix` | Bug fix | `fix(auth): handle expired tokens` |
| `refactor` | Restructuring with no intentional functional changes | `refactor(users): extract validation logic` |
| `test` | Tests | `test(auth): add login unit tests` |
| `docs` | Documentation | `docs(api): document error responses` |
| `style` | Formatting with no functional changes | `style(users): format service methods` |
| `perf` | Performance optimization | `perf(db): reduce query count` |
| `build` | Build and dependency changes | `build(deps): update framework version` |
| `ci` | Continuous integration | `ci(pipeline): add test coverage check` |
| `chore` | General maintenance | `chore(config): remove unused settings` |
| `revert` | Revert changes | `revert: revert user profile endpoint` |

### Best practices

1. Write commit messages in English.
2. Use the imperative mood: `add`, `fix`, `remove`, `update`, `implement`.
3. Describe the change made, not the time spent.
4. Keep each commit focused on one logical change.
5. Avoid generic messages such as `changes`, `fix`, `update code`, or `final version`.
6. Include the ticket identifier in the commit body when useful for traceability.

Example with a body:

```text
feat(auth): add password reset endpoint

- Add password reset request handler
- Validate reset token expiration
- Add unit tests for invalid tokens

Refs: PROJ-123
```

The `feature/` prefix identifies the branch type; `feat` classifies the change recorded in the commit. They are not interchangeable.

## 7. Pull Requests

### Title format

```text
[TICKET-ID] Short description
```

Examples:

```text
[PROJ-123] Implement password reset
[PROJ-124] Fix invalid email validation
[PROJ-125] Refactor authentication service
```

The team may choose to use Conventional Commits in PR titles, for example, `feat(auth): implement password reset`, but it must choose one format and apply it consistently.

### Pull Request template

```markdown
# [PROJ-123] Implement password reset

## Summary
Briefly describe the changes introduced by this Pull Request.

## Related Ticket
- PROJ-123

## Changes Made
- Describe the main implementation changes.
- List relevant modules, services, or components modified.
- Mention API, database, or configuration changes.

## Motivation
Explain why these changes are needed and what problem they solve.

## Testing
- [ ] Unit tests added or updated.
- [ ] Integration tests added or updated where applicable.
- [ ] Manual testing completed where necessary.
- [ ] All relevant tests pass locally.

## Screenshots / API Examples
Include screenshots, request/response examples, or other evidence when relevant.

## Breaking Changes
- [ ] No breaking changes.
- [ ] Breaking changes are documented below.

Details:
Describe any incompatible changes and required migration steps.

## Checklist
- [ ] The PR is linked to the corresponding ticket.
- [ ] The implementation follows project conventions.
- [ ] No unrelated changes are included.
- [ ] Tests and CI checks pass.
- [ ] Documentation is updated when necessary.
- [ ] The PR is ready for review.

## Reviewer Notes
Highlight areas that require special attention from reviewers.
```

### Pull Request rules

- A PR must address the objective of one ticket.
- The title must include the ticket identifier.
- Explain what changed, why it changed, and how it was tested.
- Do not mix unrelated refactoring with new features.
- Meet the repository's required approvals and automated checks.
- Delete the branch after merging if the team's workflow allows it.
- Mark PRs as Draft if they are not yet ready for review.

Small, focused PRs are preferred. If a ticket results in an excessively large PR, consider splitting it into subtasks with clear deliverables.

## 8. Code Conventions

### Naming conventions

| Element | Convention | Example |
|---|---|---|
| Class | `PascalCase` | `UserService` |
| Interface | `PascalCase` | `PaymentGateway` |
| Abstract class | `PascalCase` | `BaseRepository` |
| Exception | `PascalCase` | `InvalidTokenException` |
| DTO | `PascalCase` | `CreateUserRequestDto` |
| Entity | `PascalCase` | `UserAccount` |
| Enum | `PascalCase` | `OrderStatus` |
| Method | `camelCase` | `findUserById()` |
| Variable | `camelCase` | `userAccount` |
| Parameter | `camelCase` | `accessToken` |
| Constant | `UPPER_SNAKE_CASE` | `MAX_LOGIN_ATTEMPTS` |

### Naming rules

Use `PascalCase` for programming-language classes, interfaces, entities, and related type declarations. Use `kebab-case` for CSS class names in HTML and CSS selectors. These conventions serve different purposes and must not be confused.

**Examples:**

```html
<section class="about-us-section">
  <div class="team-member-card"></div>
</section>
```

```css
.about-us-section { /* styles */ }
.team-member-card { /* styles */ }
```

```typescript
class AboutUsService {}
```

### Example

```typescript
export class UserService {
  private readonly MAX_LOGIN_ATTEMPTS = 5;

  public findUserById(userId: string): UserAccount | null {
    // Implementation
    return null;
  }

  public resetPassword(userId: string): void {
    // Implementation
  }
}
```

The way constants and modifiers are declared must be adapted to the language and framework. In TypeScript, for example, a `static readonly` class constant is commonly written in `UPPER_SNAKE_CASE` if that is the convention selected by the team.

### Additional rules

- Class names must describe their responsibility.
- Avoid generic names such as `Manager`, `Helper`, or `Utils` when a more descriptive alternative is available.
- Class, method, variable, and file names must be in English.
- Do not add artificial prefixes such as `CUserService` or `IUserService`, unless required by the language or architecture.
- Follow framework conventions: programming classes and interfaces use `PascalCase`; CSS/HTML class names and files use `kebab-case` where applicable.

Examples:

- `AuthenticationService`
- `PaymentProcessor`
- `UserRepository`
- `CreateOrderRequest`
- `OrderStatus`
- `InvalidCredentialsException`

## 9. Project Language

English will be the standard technical language for elements that are part of the codebase and development history.

| Element | Recommended language |
|---|---|
| Tickets | English |
| Branch names | English |
| Commits | English |
| Pull Requests | English |
| Classes, methods, and variables | English |
| Code comments | English |
| Technical documentation | English |
| Internal communication | According to the language agreed upon by the team |

This does not prevent internal communication from being in Spanish. The goal is to keep technical artifacts consistent.

## 10. Workflow

1. **Create the ticket:** define the scope, acceptance criteria, and unique identifier.
2. **Create the branch:** create a dedicated branch for the ticket.
3. **Implement and commit:** develop, test, and record logical changes using English commit messages.
4. **Open the Pull Request:** link the ticket, explain the changes, and request a review.
5. **Review and merge:** complete the required approvals and automated checks before merging.
6. **Close the ticket:** verify that the merged change meets the acceptance criteria and update the ticket status.

## 11. Quick Reference

| Element | Format | Example |
|---|---|---|
| Branch | `prefix/TICKET-ID-short-description` | `feature/PROJ-123-user-profile` |
| Ticket | `TYPE-ID: Short description` | `PROJ-123: Implement user profile` |
| Commit | `type(scope): imperative description` | `feat(users): add profile endpoint` |
| Pull Request | `[TICKET-ID] Short description` | `[PROJ-123] Implement user profile` |
| Programming class | `PascalCase` | `UserProfileService` |
| CSS/HTML class | `kebab-case` | `user-profile`, `main-navbar` |
| Ticket-branch relationship | One ticket per branch | `feature/PROJ-123-user-profile` |

## 12. Repository Adoption

To ensure these rules are applied consistently, it is recommended to:

- Add this document to the repository as `README.md`, or keep it in `CONTRIBUTING.md` / `docs/development-workflow.md`.
- Create ticket and Pull Request templates.
- Configure automated validation for branch names and commit messages when the tools allow it.
- Establish branch protection rules, approval requirements, and CI checks.
- Maintain links between tickets, branches, and Pull Requests.

---

**Fundamental rule:** every change must have an identifiable purpose, an associated ticket, a dedicated branch, descriptive commit messages in English, and a Pull Request that can be reviewed before it is merged.
