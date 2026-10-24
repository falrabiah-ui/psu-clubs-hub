# ADR-002: Server-side club-scoped authorization with simulated login

Status: Proposed (team to confirm)  
Date: TODO(team)

## Context
The most important quality property is that officers can act only on their own club, and only Student Affairs can approve events. The scope allows simulated accounts and optional university authentication.

## Decision
1. Each user has a global role (STUDENT or STUDENT_AFFAIRS). Officer and advisor rights are stored per club in `club_roles`.
2. All authorization decisions are made in one policy module called by the service layer on every operation. Default is deny.
3. Login is simulated: choose a synthetic user, receive a signed session cookie. The feature is switched on only by configuration.
4. The acting user and roles are always read from the database using the session, never from request data.
5. The UI hides actions the user cannot perform, but this is never relied on.

## Alternatives considered
| Option | Why not chosen |
|---|---|
| Role stored only in the session or token | Stale or forgeable if mishandled. Database lookup is simple enough here |
| Checks in the UI/router only | Bypassable by calling the API directly, so client-only checks do not protect data |
| Global roles only (officer = one global flag) | Cannot express "only their own club", the main requirement (AC-07, AC-13) |
| Real PSU single sign-on now | Out of scope, needs credentials and review. Left as an optional later integration |
| Policy library (e.g. Casbin) | More concepts to explain than a small policy module for this size |

## Consequences
- (+) One place to review and test every permission. Each permission maps to acceptance criteria.
- (+) Role changes take effect immediately.
- (-) One extra database lookup per request. Acceptable for a prototype.
- (-) Simulated login is insecure by design. PSU IT must replace it before real use.
