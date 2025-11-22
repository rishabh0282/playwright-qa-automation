# Cursor agent prompt

## Goal
Build an automation agent that logs in to events.webmobi.com, creates an event, and validates the result using Playwright.

## Environment
- **Base URL:**
  - https://events.webmobi.com
- **Credentials (env vars):**
  - LOGIN_EMAIL
  - LOGIN_PASSWORD
- **Runtime:**
  - Node.js + Playwright
  - Headless by default

## Tasks
1. **Authenticate**
   - Navigate to the login page.
   - Fill email and password from environment variables.
   - Submit and wait for a post-login indicator (e.g., dashboard selector).

2. **Create event**
   - Open the event creation flow/page.
   - Fill required fields:
     - Title: unique value (timestamp-based).
     - Date/time: valid future datetime.
     - Description: short text.
   - Submit and wait for success notification or redirect.

3. **Validate**
   - Navigate to the events list or detail page.
   - Assert the newly created event title is present and visible.
   - Optionally verify via API/response if accessible.

4. **Evidence capture**
   - Enable Playwright trace/video/screenshot on failure.
   - Generate an HTML test report.
   - Log key steps (auth start, event title, validation selector).

5. **CI/CD**
   - Provide a GitHub Actions workflow to:
     - Install dependencies and run tests headlessly.
     - Upload artifacts (HTML report, trace, videos).
     - Publish the HTML report to GitHub Pages.

## Success criteria
- **Login succeeds** and the dashboard element is visible.
- **Event is created** with a unique title.
- **Event appears** in the list with correct title.
- **Artifacts available**: HTML report, trace/video, logs.
- **CI pipeline passes** and publishes the report.

## Output
- **Playwright test files** (e.g., tests/auth.spec.ts, tests/event.spec.ts).
- **Config** (playwright.config.[ts|js]) with reporter and tracing.
- **Workflow** (.github/workflows/ci.yml) for artifacts and Pages.
- **README** with setup, env var usage, and links to the live report.
