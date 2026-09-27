# BUILD LOG

## 2026-09-27 — Environment setup
- The project initially failed to install because the installed Node.js version was incompatible with the better-sqlite3 dependency.
- I checked the repository configuration and found that the project specifies Node.js 22.
- I installed and switched to Node.js 22.23.3.
- `npm install` then completed successfully.

## 2026-09-27 — Windows path handling
- The database reset script failed on Windows because a file URL pathname was being constructed incorrectly.
- I changed the database script to use `fileURLToPath()` for filesystem paths.
- After the change, the database seeded successfully.

## 2026-09-27 — Test verification
- JWT tests passed: 43 passed, 0 failed.
- Permission tests passed: 35 passed, 0 failed.
- API tests passed: 66 passed, 0 failed.
- Playwright UI tests passed: 25 passed, 0 failed.

## 2026-09-27 — Production static serving
- The production server initially had the same Windows URL-path handling issue when resolving the dist directory.
- I changed the production server to use `fileURLToPath()` for the dist filesystem path.
- I rebuilt the application and verified that the production login page loads correctly on port 8124.

## 2026-09-27 — Final verification
- The complete Playwright suite was run after the fixes.
- Result: 25 passed, 0 failed.
- The Windows path fixes were committed and pushed to the public GitHub repository.
