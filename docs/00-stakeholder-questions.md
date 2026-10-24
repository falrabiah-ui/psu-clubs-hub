# Stakeholder Questions and Responses

## How this document was produced
No real PSU stakeholder (Student Affairs, officers, advisors, PSU IT) was available before Milestone 1.
The team therefore prepared questions Q1 to Q16 with proposed defaults and put them to **Claude (an AI assistant) acting as a simulated stakeholder**.
The responses were reviewed by the team (Faisal Alrabiah). Each response states whether it confirmed the default, changed it, or clarified it.

**Limits of this evidence.** The responses are simulated. They are not confirmed by PSU, Student Affairs, or the instructor.
The same AI proposed the defaults and then answered, so a "confirmed" answer is weak independent evidence. The most impactful answers (Q4, Q5, Q12) should be validated by a real stakeholder or in instructor feedback.

Status values: `ANSWERED (simulated)` means the simulated stakeholder responded. Response type is `CONFIRMED`, `CHANGED`, or `CLARIFIED`.

| ID | Question | Proposed default | Simulated stakeholder response | Effect on requirements |
|---|---|---|---|---|
| Q1 | Who creates clubs? | Only Student Affairs creates (PENDING) and activates clubs | CONFIRMED. Student club proposals are out of scope | FR-03, AC-05, AC-06 |
| Q2 | Can a student belong to several clubs? | Yes. One open membership per student per club | CONFIRMED | FR-05, AC-09 |
| Q3 | Can one person be officer of several clubs and member of others? | Yes. Officer and advisor roles are per club | CONFIRMED | `club_roles` table, AC-07, AC-13 |
| Q4 | May an officer decide their own membership request? | No | CONFIRMED and extended: nobody may decide a request they submitted | AC-15 |
| Q5 | One or two event approval stages? | One stage (Student Affairs). Advisor is read-only | CONFIRMED for release 1. An advisor stage is likely later | `02-design.md` section 7 |
| Q6 | Events open to all students or members only? | All signed-in students | CONFIRMED | FR-12, AC-24 |
| Q7 | Capacity and waiting list? | Capacity required. No waiting list | CONFIRMED | AC-24 to AC-26 |
| Q8 | Who records attendance, can it be corrected? | Officers only, after start, corrections audited | CONFIRMED | FR-14, AC-29 |
| Q9 | Registrations when an event is cancelled? | Registrations become CANCELLED | CONFIRMED | AC-22 |
| Q10 | Re-request after rejection? Leaving a club? | Re-request allowed. Leaving out of scope | CONFIRMED | AC-09 |
| Q11 | Which report metrics? | Clubs by status, members per club, events by status, registrations and attendance per event | **CHANGED**: also show the number of event proposals waiting for a decision | FR-16, AC-31 |
| Q12 | Which actions are audited, who sees them? | All decisions and admin actions. Student Affairs views | **CLARIFIED**: all actions must be recorded. No viewing screen is required in release 1, but data must allow a later audit report. Records are never editable through the API | US-15, AC-32, section 8 of requirements |
| Q13 | Language and accessibility? | English only, WCAG 2.1 AA target | CONFIRMED. Arabic/right-to-left is a future requirement, not tested now | NFR-04 |
| Q14 | Event timing rules? | Start in future, end after start. No overlap rule | CONFIRMED | AC-17 |
| Q15 | Club categories fixed or free text? | Fixed seeded list | CONFIRMED | AC-03 |
| Q16 | Deactivating or pausing clubs? | Not in release 1 | CONFIRMED. `status` field kept extensible | `02-design.md` section 7 |

Status of all questions: `ANSWERED (simulated)`.

## Remaining validation (carried into Milestone 2)
1. Validate Q4, Q5 and Q12 with the instructor or a real stakeholder when possible.
2. If instructor feedback on Milestone 1 contradicts any response above, record the change in the change history of `01-requirements.md` and update the affected tests.
