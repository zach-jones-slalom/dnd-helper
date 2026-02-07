<!--
SYNC IMPACT REPORT
==================
Version Change: INITIAL → 1.0.0
Constitution Type: Initial ratification
Added Principles:
  1. Code Quality and Consistency
  2. Single Responsibility Principle
  3. Test-Driven Development (NON-NEGOTIABLE)
  4. Error Handling and Resilience
  5. Maintainability First
  6. Design System Adherence

Templates Status:
  ✅ Constitution created from project documentation
  ✅ .specify/templates/plan-template.md (updated Constitution Check section)
  ✅ .specify/templates/spec-template.md (verified - no changes needed)
  ✅ .specify/templates/tasks-template.md (verified - no changes needed)
  ✅ No command templates exist (skipped)
  ✅ README.md (verified - no constitution references)
  ✅ docs/coding-guidelines.md (source for principles - no updates needed)
  ✅ docs/testing-guidelines.md (source for principles - no updates needed)
  ✅ docs/ui-guidelines.md (source for principles - no updates needed)

Follow-up TODOs: None

Suggested Commit: docs: establish project constitution v1.0.0 (initial principles)
-->

# MTG Swiss Manager Constitution

## Core Principles

### I. Code Quality and Consistency
**MUST** follow established coding standards without exception:
- Use 2-space indentation for all files (JavaScript, JSON, CSS, Markdown)
- Follow naming conventions: `camelCase` for variables/functions, `PascalCase` for components/classes, `UPPER_SNAKE_CASE` for constants
- Organize imports in order: external libraries, internal modules, styles (with blank lines between groups)
- Keep lines under 100 characters for readability
- Remove all trailing whitespace and use LF line endings
- Pass all ESLint checks before committing code

**Rationale**: Consistency eliminates cognitive load, reduces merge conflicts, and enables team members to navigate and understand code instantly. Automated tooling (ESLint) catches violations early, preventing technical debt.

### II. Single Responsibility Principle
**MUST** design every module, component, and function with a single, well-defined purpose:
- Each React component handles one UI concern (e.g., `TodoCard` displays a todo, does not fetch or delete)
- Each function performs one operation with clear inputs and outputs
- No "god objects" or multi-purpose utilities that do unrelated tasks
- Extract common code into focused, reusable utilities

**Rationale**: Single responsibility makes code testable, maintainable, and debuggable. When requirements change, the blast radius is minimized. Components become composable building blocks rather than tangled dependencies.

### III. Test-Driven Development (NON-NEGOTIABLE)
**MUST** write tests as part of the development process, not after:
- Target 80%+ code coverage across all packages (frontend and backend)
- Write unit tests for individual components/functions in isolation
- Write integration tests for component interactions and API communication
- Follow Arrange-Act-Assert (AAA) pattern in all tests
- Mock external dependencies (API calls, timers, etc.) to ensure test isolation
- Run tests locally before committing; all tests must pass before creating pull requests

**Rationale**: Tests are executable documentation that describe expected behavior. TDD catches bugs early, enables confident refactoring, and ensures code is designed for testability from the start. The 80% coverage threshold is measurable and enforced via Jest coverage reports.

### IV. Error Handling and Resilience
**MUST** handle errors gracefully at every layer:
- Wrap operations that can fail (API calls, data transforms) in try-catch blocks
- Provide meaningful, actionable error messages to users (avoid generic "Error occurred")
- Log errors with sufficient context for debugging (error type, operation attempted, relevant data)
- Never leave unhandled promise rejections or silent failures
- Validate inputs at API boundaries (backend routes, component props)

**Rationale**: Unhandled errors lead to poor user experience and difficult debugging. Graceful degradation keeps the application usable even when individual operations fail. Clear error messages reduce support burden and user frustration.

### V. Maintainability First
**MUST** prioritize code readability and maintainability over cleverness:
- Apply DRY (Don't Repeat Yourself): Extract repeated code into shared functions/components
- Apply KISS (Keep It Simple): Prefer straightforward implementations over complex ones
- Write meaningful comments explaining "why" (not "what" the code does)
- Use JSDoc for public functions and components
- Keep functions small and focused (ideally under 50 lines)
- Avoid premature optimization; write clear code first, optimize only when necessary with data

**Rationale**: Code is read far more often than written. Maintainable code reduces onboarding time, enables faster feature development, and minimizes bugs introduced during changes. Simple code is easier to test and debug.

### VI. Design System Adherence
**MUST** follow the established design system for all UI work:
- Use defined color palette (light mode and dark mode variants) from ui-guidelines.md
- Apply 8px grid system for all spacing (xs: 8px, sm: 16px, md: 24px, lg: 32px, xl: 48px)
- Use system font stack with defined typography scale (28px headings, 16px body, etc.)
- Apply consistent card styling (8px border radius, subtle shadows, defined padding)
- Support both light and dark modes with appropriate color tokens
- Maintain single-column layout with 600px max width on larger screens

**Rationale**: Design consistency creates a professional, polished user experience. A documented design system enables parallel development without UI conflicts. Adherence to spacing/typography scales ensures visual harmony and accessibility.

## Technical Stack

**MUST** use the following technologies:
- **Frontend**: React 19 with JavaScript (Vite build tool), CSS for styling, Jest + React Testing Library for tests
- **Backend**: Node.js with Express.js, Jest for tests
- **Architecture**: Monorepo structure using npm workspaces (`packages/frontend`, `packages/backend`)
- **Persistence**: Backend API with Express.js (RESTful endpoints)
- **Development**: ESLint for linting, npm scripts for build/test/start

**Rationale**: Standardizing the stack ensures tooling consistency, reduces decision fatigue, and leverages team expertise. The monorepo structure with npm workspaces simplifies dependency management and enables atomic cross-package changes.

## Development Workflow

**MUST** follow these practices:
1. **Commit Standards**: Use atomic commits (one logical change per commit) with descriptive messages explaining "why" (e.g., `feat: add player removal with tournament reset`)
2. **Branching**: Use feature branches for new work (e.g., `feature/player-management`), merge via pull requests
3. **Code Review**: All code must be reviewed before merging; reviewer verifies principle compliance (tests present, error handling, naming conventions, etc.)
4. **Testing Gate**: All tests must pass locally before creating a pull request; CI/CD (if configured) must pass before merge
5. **Linting**: Run `npm run lint` or equivalent before committing; fix all errors and warnings
6. **Test Coverage**: New code must maintain or improve the 80% coverage target; coverage reports are generated via `npm test -- --coverage`

**Rationale**: Structured workflows prevent defects from reaching production, ensure knowledge sharing via code review, and maintain quality standards through automated gates (tests, linting).

## Governance

This constitution supersedes all other development practices and serves as the authoritative source for project standards. All pull requests and code reviews **MUST** verify compliance with these principles.

- **Amendment Process**: Proposals for changes must document the rationale, impact on existing code, and migration plan (if applicable). Amendments require team consensus and documentation update.
- **Versioning Policy**: 
  - **MAJOR**: Backward-incompatible changes (principle removal/redefinition)
  - **MINOR**: New principles or materially expanded guidance
  - **PATCH**: Clarifications, wording improvements, typo fixes
- **Compliance Review**: Periodic audits (quarterly or per release) verify adherence; violations must be addressed in a timely manner
- **Runtime Guidance**: For development-time workflow guidance (beyond these principles), refer to documentation in `docs/` directory (coding-guidelines.md, testing-guidelines.md, ui-guidelines.md, functional-requirements.md)

**Version**: 1.0.0 | **Ratified**: 2026-02-07 | **Last Amended**: 2026-02-07
