# Requirements Specification: PSU Clubs Hub (Release 1)

Priorities use MoSCoW (M = must, S = should, C = could). Stakeholder responses Q1 to Q16 (from a simulated stakeholder, see `00-stakeholder-questions.md`) are the source for the rules below.

## 1. Purpose and scope
Local prototype that lets students discover clubs and join them, lets officers run their own club,
and lets Student Affairs approve events and see institutional reports.
**Out of scope:** payments, real university authentication (simulated accounts only), real student data, production deployment.

**Requirements source.** No real stakeholder was available before Milestone 1. Rules come from the course brief and from responses of a simulated stakeholder (an AI assistant) reviewed by the team. They still need confirmation by PSU or the instructor.

## 2. Stakeholders and roles
| Role | Who | Main needs |
|---|---|---|
| Student | Any simulated student | Find clubs, request membership, register for events, see own data |
| Club officer | Student with OFFICER role in one or more clubs | Manage membership and events of own club only, record attendance |
| Club advisor | Staff with ADVISOR role in a club | Read-only view of own club in release 1 (Q5) |
| Student Affairs (SA) | Administrator | Create/activate clubs, assign roles, approve events, reports, audit |
| PSU IT (reviewer) | Not a system user | Judge architecture, security, privacy, maintainability |

## 3. Functional requirements
| ID | Requirement | Pri | Story |
|---|---|---|---|
| FR-01 | A signed-in user can browse and search the directory of ACTIVE clubs by name and category | M | US-01 |
| FR-02 | A signed-in user can view a club profile | M | US-01 |
| FR-03 | SA can create a club (PENDING), activate it, and assign officers and advisors | M | US-02 |
| FR-04 | An officer can edit the profile of a club they manage | S | US-03 |
| FR-05 | A student can request membership in an ACTIVE club | M | US-04 |
| FR-06 | An officer can list and approve/reject membership requests of their own club | M | US-05 |
| FR-07 | A student can see own memberships and cancel own pending request | S | US-06 |
| FR-08 | An officer can propose an event for a club they manage | M | US-07 |
| FR-09 | SA can approve or reject proposed events, with a reason for rejection | M | US-08 |
| FR-10 | An officer can cancel an event of their own club | S | US-09 |
| FR-11 | Students can list approved upcoming events | M | US-10 |
| FR-12 | A student can register for an approved upcoming event, once, within capacity | M | US-11 |
| FR-13 | A student can cancel own registration before the event starts | S | US-11 |
| FR-14 | An officer can record attendance for registered students of own club's event, after it starts | M | US-12 |
| FR-15 | A student can see own attendance history | S | US-13 |
| FR-16 | SA can view a summary report, including the number of event proposals awaiting decision (Q11) | M | US-14 |
| FR-17 | Every decision and administrative action is recorded in an audit log | M | US-15 |
| FR-18 | Users sign in with a simulated account; role and club scope come from the server database | M | US-16 |

## 4. Non-functional requirements
| ID | Requirement |
|---|---|
| NFR-01 | Every endpoint enforces authentication and authorization on the server. Default is deny |
| NFR-02 | Only synthetic data. A seed script creates it. No real student data anywhere |
| NFR-03 | No names, emails, or secrets in application logs (user IDs only) |
| NFR-04 | Main flows meet a WCAG 2.1 AA target: labelled fields, keyboard operation, sufficient contrast |
| NFR-05 | A fresh clone runs with documented commands (install, seed, run) |
| NFR-06 | All automated tests run with one documented command |
| NFR-07 | Layered code (routes, services, data access). Authorization decisions live in one place |
| NFR-08 | Data integrity enforced in the database (unique constraints, foreign keys) and in transactions for capacity |
| NFR-09 | No secrets in the repository. Configuration comes from environment variables |

## 5. User stories
| ID | Story |
|---|---|
| US-01 | As a student, I want to search and view clubs so that I can find ones that match my interests |
| US-02 | As Student Affairs, I want to create, activate and staff clubs so that only verified clubs appear |
| US-03 | As an officer, I want to edit my club's profile so that information stays current |
| US-04 | As a student, I want to request to join a club so that I can become a member |
| US-05 | As an officer, I want to approve or reject requests for my club only so that I control my membership |
| US-06 | As a student, I want to see and cancel my requests so that I know my status |
| US-07 | As an officer, I want to propose an event so that Student Affairs can approve it |
| US-08 | As Student Affairs, I want to approve or reject proposals with a reason so that events follow policy |
| US-09 | As an officer, I want to cancel my club's event when plans change |
| US-10 | As a student, I want to see approved upcoming events |
| US-11 | As a student, I want to register for (and cancel) an event so that I secure a seat |
| US-12 | As an officer, I want to record attendance so that participation is tracked |
| US-13 | As a student, I want to see my own attendance history |
| US-14 | As Student Affairs, I want summary reports so that I can oversee club activity |
| US-15 | As Student Affairs, I want every decision and admin action recorded so that they are traceable (a viewing screen is a possible later change, Q12) |
| US-16 | As any user, I want to sign in with a simulated account so that I see only what my role allows |

## 6. Acceptance criteria
Format: Given / When / Then. HTTP codes: 401 not signed in, 403 not allowed, 404 not found or not visible, 409 conflict with current state, 422 invalid input.

| ID | Req | Criterion |
|---|---|---|
| AC-01 | FR-18, NFR-01 | Given no session, when any endpoint except login is called, then the response is 401 |
| AC-02 | FR-18 | Given a user signs in, when later requests are made, then identity and roles are read from the server database, and role values sent by the client are ignored |
| AC-03 | FR-01 | Given ACTIVE and PENDING clubs exist, when a user searches by partial name or category (case-insensitive), then only matching ACTIVE clubs are returned. With no match, an empty list is returned |
| AC-04 | FR-02 | Given a PENDING club, when a non-SA user requests it by ID, then the response is 404 |
| AC-05 | FR-03 | Given a non-SA user, when they create, activate, or assign roles for a club, then the response is 403 and nothing changes |
| AC-06 | FR-03, FR-17 | Given SA creates a club, activates it, and assigns an officer, then each step changes the club or role and creates an audit record |
| AC-07 | FR-04 | Given an officer of club A, when they edit club B, then the response is 403 and club B is unchanged |
| AC-08 | FR-05 | Given an ACTIVE club, when a student requests membership, then a PENDING request is stored for that student and club |
| AC-09 | FR-05 | Given a PENDING or APPROVED membership exists, when the student requests again, then the response is 409 and no second row is created. After a REJECTED request a new request is allowed |
| AC-10 | FR-05 | Given a PENDING club, when a student requests membership, then the response is 404 and nothing is stored |
| AC-11 | FR-06 | Given an officer of club A, when they list requests, then only club A requests appear |
| AC-12 | FR-06, FR-17 | Given a PENDING request in the officer's club, when the officer approves or rejects, then the status changes and the audit log stores decider, decision, and time |
| AC-13 | FR-06 | Given a request in another club, when an officer tries to decide it, then the response is 403 and the request is unchanged |
| AC-14 | FR-06 | Given a request that is already decided, when it is decided again, then the response is 409 |
| AC-15 | FR-06 (Q4) | Given any user who submitted a PENDING request, when they try to decide that request, then the response is 403 |
| AC-16 | FR-07 | Given a student, when they list memberships, then only their own appear. They can cancel own PENDING request, not others', and not a decided one |
| AC-17 | FR-08 | Given an officer of an ACTIVE club, when they propose an event with valid data (start in the future, end after start, capacity at least 1), then it is stored as PROPOSED. Invalid data gives 422 |
| AC-18 | FR-08 | Given an officer of club A, when they propose an event for club B (or a non-ACTIVE club), then the response is 403 and nothing is stored |
| AC-19 | FR-09, FR-17 | Given a PROPOSED event, when SA approves it, or rejects it with a reason, then status changes and an audit record is written. Rejection without a reason gives 422 |
| AC-20 | FR-09 | Given a non-SA user (including the proposing officer), when they approve or reject an event, then the response is 403 |
| AC-21 | FR-09 | Given an event that is not PROPOSED, when SA decides it, then the response is 409 |
| AC-22 | FR-10 | Given an officer of the club, when they cancel its event, then the event and its registrations become CANCELLED. An officer of another club gets 403 |
| AC-23 | FR-11 | Given events in all states, when a student lists events, then only APPROVED, not cancelled, upcoming events appear. PROPOSED events are visible only to that club's officers and SA |
| AC-24 | FR-12 | Given an APPROVED upcoming event with free seats, when a student registers, then a REGISTERED record is stored |
| AC-25 | FR-12 | Given an existing active registration, when the same student registers again, including two simultaneous requests, then exactly one registration exists and the other gets 409 |
| AC-26 | FR-12 | Given an event at capacity, when more students register, including simultaneous requests for the last seat, then the number of active registrations never exceeds capacity |
| AC-27 | FR-12 | Given an event that is PROPOSED, REJECTED, CANCELLED, or already started, when a student registers, then the response is 409 |
| AC-28 | FR-13 | Given own registration and an event not yet started, when the student cancels, then the seat is freed. Cancelling another student's registration or after start is refused |
| AC-29 | FR-14, FR-17 | Given a registered student and an event that has started, when an officer of that club marks attendance (present/absent), then it is stored and audited. Before start, 409. Officer of another club, 403. Non-registered student, 404 |
| AC-30 | FR-15 | Given a student, when they view attendance, then only their own records appear |
| AC-31 | FR-16 | Given seeded data, when SA requests the report, then counts of clubs by status, approved members per club, events by status, pending event proposals, and registrations/attendance per event match the data. Non-SA gets 403 |
| AC-32 | FR-17 | Given any audited action, then the audit record has actor ID, action, target, and time, with no personal data beyond IDs, and no API endpoint can change or delete audit records |
| AC-33 | NFR-03 | Given a normal workflow, when application logs are inspected, then they contain user IDs but no names, emails, or secrets (manual check) |
| AC-34 | NFR-04 | Given the main flows, when checked with a keyboard and an accessibility checker, then fields are labelled, focus order is logical, and no critical violations remain (manual checklist) |
| AC-35 | NFR-05, NFR-06 | Given a fresh clone, when the README commands are followed, then the app starts with seed data and all tests run with one command |

## 7. Traceability to planned tests
Types: U = unit, I = integration (API), E = end-to-end workflow, M = manual. Test names will be filled in during Milestone 2 and must keep the AC ID in their name.

| AC | Planned type | Independent cases to add (risk-based) |
|---|---|---|
| AC-01, AC-02 | I | Forged role in request body or cookie tampering |
| AC-03, AC-04 | U, I | Search with SQL-like characters, empty query, case differences |
| AC-05, AC-06 | I | Every SA endpoint called as student, officer, advisor |
| AC-07 | I | Officer of A edits club B (ID guessing) |
| AC-08, AC-09, AC-10 | U, I | Double submit, request after rejection |
| AC-11 to AC-15 | U, I, E | Cross-club decision, repeated decision, self-decision |
| AC-16 | I | Cancel someone else's request |
| AC-17, AC-18 | U, I | End before start, capacity 0, past start, wrong club |
| AC-19 to AC-22 | U, I, E | Non-SA approve, proposer approves own event, decide twice |
| AC-23 | I | Visibility of PROPOSED events per role |
| AC-24 to AC-28 | U, I | Duplicate and last-seat concurrency, start-time boundary, cancel then re-register |
| AC-29, AC-30 | I | Before-start marking, wrong club, non-registered student |
| AC-31, AC-32 | I | Report totals against seed data, audit immutability |
| AC-33, AC-34 | M | Log review, keyboard and checker run, screenshots with notes |
| AC-35 | M | Fresh clone run by a team member who did not write the README |
| Main workflow | E | Student requests, officer approves, officer proposes, SA approves, student registers, officer marks attendance, report shows it |

## 8. Known limitations (release 1)
Simulated login only. No notifications, no waiting list, no leaving a club, no advisor approval stage, no club inactive status, no audit report screen. These were deferred in the simulated stakeholder responses (Q5, Q10, Q12, Q16) or are possible change requests, and the design keeps room for them (`02-design.md`, section 7).

## 9. Change history
| Date | Change | Reason |
|---|---|---|
| 2026-10-24 | Initial version | Milestone 1 |
| 2026-10-24 | Added pending event proposals to the report (FR-16, AC-31) | Simulated stakeholder response Q11 |
| 2026-10-24 | AC-10 now returns 404 only. US-15 aligned with release 1 scope | Review found an untestable criterion and a scope inconsistency (Q12) |
| 2026-10-24 | AC-15 widened to any user who submitted the request | Simulated stakeholder response Q4 |
