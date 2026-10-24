# Task Plan and Risks

## 1. Work split (3 members)
Everyone reviews at least one other member's work and must be able to explain every part in the oral defense.

| Member | Main ownership | Requirements covered |
|---|---|---|
| Faisal Alrabiah (Leader) | Repo and process, auth/session, policy module, audit log, reports, integration and end-to-end test | FR-16, FR-17, FR-18, NFR-01, NFR-05 to NFR-09 |
| Faisal Alghubaini | Clubs, directory, membership workflow and their tests | FR-01 to FR-07 |
| Abdulaziz Alfaahdel | Events, registration, attendance and their tests, concurrency cases | FR-08 to FR-15 |

## 2. Task list linked to requirements
| ID | Task | Owner | Requirements | Depends on |
|---|---|---|---|---|
| T-01 | Create repo, structure, .gitignore, README skeleton | Alrabiah | NFR-05, NFR-09 | none |
| T-02 | Data model, migrations/create tables, seed script (synthetic) | Alrabiah | NFR-02, NFR-08 | T-01 |
| T-03 | Session login (simulated), `/me`, policy module | Alrabiah | FR-18, NFR-01 | T-02 |
| T-04 | Audit writer used by services | Alrabiah | FR-17 | T-02 |
| T-05 | Club directory, profile, search | Alghubaini | FR-01, FR-02 | T-03 |
| T-06 | Club creation, activation, role assignment | Alghubaini | FR-03 | T-03, T-04 |
| T-07 | Membership request, decision, cancel | Alghubaini | FR-05 to FR-07 | T-06 |
| T-08 | Club profile edit | Alghubaini | FR-04 | T-06 |
| T-09 | Event proposal, decision, cancel, listing | Abdulaziz | FR-08 to FR-11 | T-06 |
| T-10 | Registration and cancellation with capacity and duplicate rules | Abdulaziz | FR-12, FR-13 | T-09 |
| T-11 | Attendance marking and history | Abdulaziz | FR-14, FR-15 | T-10 |
| T-12 | Summary report | Alrabiah | FR-16 | T-07, T-10 |
| T-13 | Minimal accessible UI for main flows | All (one flow each) | NFR-04 | T-05 to T-11 |
| T-14 | Authorization misuse test suite (all endpoints x all roles) | Rotate: author must not be the endpoint's owner | NFR-01 | T-03 onward |
| T-15 | Traceability table filled with real test names and results | Alrabiah | all AC | continuous |
| T-16 | README, run/test commands, fresh-clone check by another member | Alghubaini | NFR-05, NFR-06 | end |

## 3. Suggested schedule
Milestone 1 (due in a couple of days)
1. Day 1: put questions Q1 to Q16 to the simulated stakeholder, review the responses, update the requirements, create the repo and first commits.
2. Day 2: review `02` and the ADRs, complete the AI-use log honestly, final consistency check (requirements, design, and plan agree), tag `milestone-1`.

Note: the Milestone 1 documents were prepared by Faisal Alrabiah because of time constraints. The work split above applies from Milestone 2.

Milestone 2: build per the course schedule (Weeks 4 to 8). Order: T-02, T-03, then T-05 to T-11 in parallel, then T-12 to T-16.

## 4. Risks
| ID | Risk | Likelihood | Impact | Mitigation | Owner |
|---|---|---|---|---|---|
| R1 | Simulated stakeholder responses are not confirmed by real PSU stakeholders or the instructor | Medium | Medium | Responses documented in `00`, rules isolated in services, change history kept, validate Q4/Q5/Q12 when possible | Alrabiah |
| R2 | AI-generated code has weak authorization (client-only, missing club scope) | High | High | Policy module, per-endpoint misuse tests, review every diff | All |
| R3 | Large unreviewed AI changes, code the team cannot defend | High | High | One task per request, small commits, peer review, walkthrough meeting before demo | All |
| R4 | Free model is less capable or hits limits | Medium | Medium | Short focused prompts, log limitations, keep tasks small | All |
| R5 | Race conditions on duplicate registration and capacity | Medium | High | DB unique constraint, transactional count, explicit concurrency test | Abdulaziz |
| R6 | Tests only cover happy paths | High | High | Misuse cases from section 7 of `01`, written by someone other than the endpoint owner | All |
| R7 | Real or personal data enters repo, logs, or prompts | Low | High | Seed script only, never paste real data to the AI, log review (AC-33) | All |
| R8 | Merge conflicts and late integration | Medium | Medium | Integrate at least twice per week, short-lived branches | Alrabiah |
| R9 | Unequal contribution or someone cannot explain the system | Medium | High | Rotate reviews, each member demos one flow, practise oral questions | All |
| R10 | Change request in Week 7 hits an area with weak tests | Medium | High | Keep traceability current, design notes in `02` section 7 | All |

## 5. Suggested commits for Milestone 1
Each member commits their own work from their own account, for example:
1. `docs: add project README and gitignore` (repo owner)
2. `docs: add stakeholder questions and assumptions`
3. `docs: add requirements, user stories, acceptance criteria`
4. `docs: add architecture diagram, data model, API contract`
5. `docs: add ADR-001 technology and ADR-002 authorization`
6. `docs: add task plan, risks, and AI-use log`
7. Follow-up commits that record real corrections after review (these are good evidence).
