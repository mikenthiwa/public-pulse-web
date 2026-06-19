# Capstone spec — Public Pulse Angular Frontend

## Problem statement

Public Pulse Angular Frontend will provide the citizen-facing experience for a
civic reporting platform where people can report public infrastructure issues
such as damaged roads. The frontend will eventually turn the Public Pulse
backend API into clear workflows for creating, viewing, confirming, and tracking
reports so civic issues can become structured and visible.

## What success looks like

- [ ] A visitor can understand what Public Pulse does from the landing page.
- [ ] A user can register and log in with an email and password.
- [ ] The frontend stores the returned JWT for authenticated API requests.
- [ ] A citizen can create an infrastructure report with description, category,
      photo metadata, county, and road name.
- [ ] Users can browse a public list of reported issues.
- [ ] Users can view full details for a single report.
- [ ] Users can anonymously confirm/upvote an existing issue.
- [ ] The authenticated report creator can update a report status from
      `Reported` to `InProgress` to `Resolved`.
- [ ] Unauthenticated users cannot create reports or update report status.
- [ ] Frontend checks pass with `npm run build`.

## Current frontend state

- A new Angular workspace exists at `puplic-pulse-workspace`.
- The `public-pulse` Angular application exists under `projects/public-pulse`.
- The setup phase intentionally contains no product features yet.
- Authentication, routing, API integration, state management, UI pages, feature
  modules, and application workflows are out of scope for this phase.

## Architecture sketch

- A multi-project Angular workspace that can support future applications and
  shared libraries if needed.
- A primary Angular application named `public-pulse`.
- TypeScript with Angular strict mode enabled.
- SCSS for application styles.
- Standalone Angular application bootstrapping.
- Future app code should keep citizen-portal workflows clear, accessible, and
  aligned with backend API contracts.

## Tech stack

- Framework: Angular
- Language: TypeScript
- Styling: SCSS
- Package manager: npm
- Application: `public-pulse`
- Workspace: `puplic-pulse-workspace`
- Selector prefix: `puplic-pulse-org`
- API: Public Pulse backend REST API, when integration begins in a later phase

## Backend API contract summary

The frontend should eventually consume the implemented Public Pulse backend MVP
endpoints. This setup phase does not implement API integration.

| Flow | Endpoint | Auth | Future frontend use |
| --- | --- | --- | --- |
| Register | `POST /api/Auth/register` | Public | Create a local account and receive a JWT. |
| Login | `POST /api/Auth/login` | Public | Authenticate and receive a JWT. |
| Categories | `GET /api/Categories` | Public | Populate the report category selector. |
| Create report | `POST /api/Reports` | Bearer token | Submit a new infrastructure report. |
| List reports | `GET /api/Reports` | Public | Show public report summaries. |
| Report details | `GET /api/Reports/{id}` | Public | Show the full report detail view. |
| Confirm report | `POST /api/Reports/{id}/confirmations` | Public | Increment the report confirmation count. |
| Update status | `PUT /api/Reports/{id}/status` | Bearer token | Let the report creator update status. |

Backend responses use the shared wrapper shape:

```ts
type ApiResponse<T> = {
  success: boolean;
  message: string;
  data: T;
};
```

Important backend models for future frontend typing:

- `RegisterRequest`: `email`, `password`
- `LoginRequest`: `email`, `password`
- `AuthResponse`: `userId`, `email`, `token`, `expiresAtUtc`
- `CategoryResponse`: `id`, `name`, `description`
- `CreateReportRequest`: `description`, `categoryId`, image metadata,
  `county`, `roadName`
- `ReportListItemResponse`: `id`, `categoryId`, `categoryName`, `county`,
  `roadName`, `status`, `confirmationCount`, `created`
- `ReportResponse`: list item fields plus `description`, image metadata, and
  `lastModified`
- `ConfirmReportResponse`: `reportId`, `confirmationCount`
- `ReportStatus`: `Reported`, `InProgress`, `Resolved`

## Frontend task list

1. [x] Create the public GitHub repository `public-pulse-web`.
2. [x] Create the Angular workspace `puplic-pulse-workspace`.
3. [x] Generate the Angular application `public-pulse`.
4. [x] Add project guidance in `projects/public-pulse/AGENTS.md`.
5. [x] Add this capstone specification in `projects/public-pulse/CAPSTONE.md`.
6. [x] Confirm the Angular app builds with `npm run build -- public-pulse`.
7. [ ] Define environment configuration once API integration begins.
8. [ ] Add endpoint-specific TypeScript request and response types.
9. [ ] Add API helpers for auth, categories, reports, confirmations, and status
       updates.
10. [ ] Add authentication UI for register and login.
11. [ ] Store the JWT and attach it to authenticated requests.
12. [ ] Add a public reports list view.
13. [ ] Add a report detail view.
14. [ ] Add a report creation form using backend categories.
15. [ ] Add an anonymous confirm/upvote action on report details.
16. [ ] Add status update controls for authenticated report creators.
17. [ ] Add loading, empty, success, and error states for core flows.
18. [ ] Validate required form fields before submitting to the API.
19. [ ] Keep report responses public and avoid exposing creator identity.
20. [ ] Update README if setup, environment variables, scripts, or workflows
       change.

## Manual acceptance scenarios

- The Angular workspace can be installed with `npm install`.
- The generated `public-pulse` application builds successfully.
- The setup contains no implemented product workflows.
- No authentication, routing, API integration, state management, feature modules,
  or custom UI pages have been added.
- Future agents can understand the project scope from `CAPSTONE.md` and
  development expectations from `AGENTS.md`.

## Verification

Run setup checks before marking this phase complete:

```bash
npm run build -- public-pulse
git status --short
find . -maxdepth 4 -type f | sort
```

When future application features are added, run the relevant Angular checks and
manual smoke tests for the changed behavior.

## Out of scope for setup phase

- Authentication and authorization.
- Routing and route guards.
- API integration.
- Services, interceptors, or state management.
- UI pages, feature modules, or application workflows.
- Real photo upload storage.
- Maps and geospatial search.
- Advanced admin dashboard.
- Real-time notifications.
- SMS/USSD integration.
- AI image analysis.
- Payment or donation features.
- Production deployment hardening.

## Open questions

- Should future API configuration use Angular environment files, runtime
  configuration, or another deployment-specific mechanism?
- Should JWT auth state be stored in local storage, session storage, or a cookie?
- Should anonymous confirmations be limited per browser/session in the frontend?
- Should report creation require image metadata for MVP demos, or allow it to be
  optional until upload support exists?
- Should the first report list be a simple card grid, table, or map-ready list?
