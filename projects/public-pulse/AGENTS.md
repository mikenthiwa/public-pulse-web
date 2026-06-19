# Setup

- Use Node.js LTS and npm for this Angular workspace.
- Install dependencies with `npm install`.
- Run Angular CLI commands from the workspace root:
  `puplic-pulse-workspace`.
- Build the primary app with `npm run build -- public-pulse`.
- Keep the workspace multi-project friendly so future applications and shared
  libraries can be added under `projects/` when needed.
- Do not add extra libraries unless a future feature clearly requires them and
  the tradeoff is documented.

# Architecture

- This workspace contains one Angular application: `public-pulse`.
- `public-pulse` is the primary citizen portal for reporting and tracking public
  infrastructure issues.
- Keep the setup phase minimal: no authentication, routing, API integration,
  services, state management, feature modules, or custom UI workflows.
- Prefer standalone Angular APIs and strict TypeScript for future application
  code.
- Use SCSS for application and component styles.
- Keep future app-wide providers and cross-cutting Angular setup close to the
  application bootstrap until there is enough real complexity to justify a
  larger structure.
- When features begin, keep citizen-facing workflows clear, accessible, and
  aligned with the Public Pulse backend contract.

# Testing

- This setup phase intentionally does not include tests.
- Add or update focused tests when future work introduces meaningful behavior.
- Prefer tests that cover externally observable citizen-portal behavior instead
  of implementation details.
- Use Angular testing utilities for Angular services, components, guards, and
  other framework-integrated code when those artifacts are introduced.
- Run relevant build and test commands before marking future behavior changes
  complete.

# Style

- Prefer TypeScript and Angular standalone components.
- Preserve the selector prefix `puplic-pulse-org`.
- Keep names clear and domain-oriented; use Public Pulse language such as
  reports, categories, confirmations, statuses, counties, and roads when those
  features are implemented.
- Keep functions small, behavior explicit, and abstractions justified by real
  duplication or complexity.
- Do not introduce routing, API clients, services, state containers, feature
  folders, or UI systems before the corresponding feature work is approved.
- Keep SCSS readable and local to the component or application surface it
  styles.
- Avoid hardcoded secrets, production URLs, tokens, or user-specific paths.

# Review

- Before finishing, review `git diff` for focused scope and unintended edits.
- Run the relevant checks for the changed scope; for setup-only changes, run
  `npm run build -- public-pulse`.
- Call out any checks that were skipped and why.
- Check for behavior regressions, missing tests for meaningful behavior,
  unnecessary complexity, hardcoded secrets, and convention drift.
- Keep `CAPSTONE.md`, `AGENTS.md`, and README files current when setup commands,
  project structure, or development workflows change.
