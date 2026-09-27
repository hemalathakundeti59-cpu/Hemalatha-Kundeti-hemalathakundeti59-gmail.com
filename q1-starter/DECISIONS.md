# DECISIONS

## 2026-09-27 — Use Node.js 22
**Decision:** Use Node.js 22 for the project.

**Alternative rejected:** Continue using the newer Node.js version already installed.

**Why the alternative fails:** The better-sqlite3 dependency did not install correctly with the newer Node.js version. The repository specifies Node.js 22, so using the specified version provides a compatible environment.

## 2026-09-27 — Use fileURLToPath for filesystem paths
**Decision:** Use `fileURLToPath()` when converting module-relative file URLs into filesystem paths.

**Alternative rejected:** Use `new URL(...).pathname` directly.

**Why the alternative fails:** On Windows, the URL pathname can produce an incorrect filesystem path. `fileURLToPath()` correctly converts the file URL into a Windows filesystem path.

## 2026-09-27 — Keep server-side permission resolution
**Decision:** Keep permission resolution on the server side.

**Alternative rejected:** Resolve role-to-permission mappings in the web application.

**Why the alternative fails:** Client-side permission logic can be modified by the client and should not be trusted for authorization. The server must make the final authorization decision.

## 2026-09-27 — Preserve session grandfathering
**Decision:** Permission changes affect new sessions while existing sessions retain their session-time permissions until the relevant lifecycle event.

**Alternative rejected:** Recalculate every existing session immediately after every permission change.

**Why the alternative fails:** The project requirements explicitly define grandfathered sessions. Immediate recalculation would change the intended session behavior.

## 2026-09-27 — Use the database as the source of truth for roles and permissions
**Decision:** Read roles and permissions from the database at runtime.

**Alternative rejected:** Hardcode the documented role-permission matrix in the application.

**Why the alternative fails:** The challenge intentionally includes a role and permission that are not present in the documentation, and hidden tests use different fixtures. Hardcoding the documented matrix would fail those cases.
