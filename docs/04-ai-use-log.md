# AI-Use Evidence Log

Record important interactions, not every message. Be honest: this log is assessed on honest examples of use, correction, and limitations.
Fields marked `TODO(team)` must be filled in by the team after genuinely reviewing the output. Do not leave invented entries.

## 1. Model disclosure
| Item | Value |
|---|---|
| Tools used | Claude (Anthropic) in the claude.ai chat interface for drafting requirements and design. OpenCode: TODO(team) which model/provider, and for which tasks |
| Provider and model name | Claude: TODO(team) confirm model name shown in the interface. OpenCode model: TODO(team) |
| Change of model during the project | TODO(team) |
| Approximate cost | TODO(team) (state "free" if no paid plan) |
| Limitations that affected our work | TODO(team) (for example: limits, context length, errors observed) |
| Data sent to AI | Only course documents and project text. No real student or PSU confidential data |

## 2. Log (Milestone 1 entries)
| # | Phase | Objective and approach | What the AI contributed | Verification and decision |
|---|---|---|---|---|
| 1 | Requirements | Uploaded the course project slides and asked what information was missing before starting | Listed 12 clarifying questions (team, stack, model, login, event approval, attendance, and others) | TODO(team): which questions were kept, which were dropped and why |
| 2 | Requirements | Asked for stakeholder questions with default assumptions | Drafted 16 questions Q1 to Q16 with assumptions A1 to A16, including the conflict-of-interest case (officer deciding own request) | TODO(team): which assumptions you changed or rejected, and which you sent to the instructor |
| 3 | Requirements | Asked for functional and non-functional requirements, user stories, acceptance criteria | Drafted FR-01 to FR-18, NFR-01 to NFR-09, US-01 to US-16, AC-01 to AC-35 and a traceability table | TODO(team): record at least one acceptance criterion you rewrote or removed, and why. Check every AC is testable |
| 4 | Requirements | Asked for a role and permission view | Proposed club-scoped officer/advisor roles and Student Affairs as global admin | TODO(team): note whether you agreed with the advisor being read-only in release 1 |
| 5 | Design | Asked for architecture, data model, API contract | Proposed FastAPI + SQLite modular monolith, ER model, endpoint table | TODO(team): what you changed (for example endpoints, table fields, state machines) |
| 6 | Design | Asked for decision records | Drafted ADR-001 and ADR-002 with alternatives and consequences | TODO(team): record one AI proposal you rejected or corrected (the rubric asks for this evidence) |
| 7 | Planning | Asked for work split and risks | Drafted task list T-01 to T-16 and risks R1 to R10 | TODO(team): record whether the split was adjusted to real skills and availability |

## 3. Failed approaches and recoveries
TODO(team): record real examples as they happen (an AI answer that was wrong, how it was found, how the team recovered).

## 4. Rejected or corrected AI proposals (required evidence)
| Proposal | Why rejected or corrected | Result |
|---|---|---|
| TODO(team) | TODO(team) | TODO(team) |

## 5. Notes for later phases
Implementation, testing, and change-request entries are added in Milestone 2, using the prompt pattern Context, Goal, Constraints, Verification.
