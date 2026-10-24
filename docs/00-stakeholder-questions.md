# Stakeholder Questions and Assumptions

The brief is incomplete. Questions below are to be sent **through the instructor** (course rule).
Until answered, the team works with the stated default assumption. Status: `OPEN` / `ANSWERED` / `ASSUMED`.

| ID | Question | Why it matters | Default assumption | Status |
|---|---|---|---|---|
| Q1 | Who creates clubs: only Student Affairs, or can students propose new clubs? | Club lifecycle | A1: Only Student Affairs creates clubs (as PENDING) and activates them | OPEN |
| Q2 | Can one student belong to several clubs at once? | Uniqueness rules on memberships | A2: Yes, many clubs. One open (pending/approved) membership per student per club | OPEN |
| Q3 | Can one person be an officer of several clubs, and an ordinary member of others? | Role model | A3: Yes. Officer/advisor roles are scoped per club | OPEN |
| Q4 | May an officer decide their own membership request? | Conflict of interest | A4: No. A user can never decide their own request | OPEN |
| Q5 | Is event approval one stage (Student Affairs) or two (advisor, then Student Affairs)? | Workflow and state machine | A5: One stage, Student Affairs only. Advisor is read-only in release 1 | OPEN |
| Q6 | Are events open to all students or to club members only? | Registration rule | A6: Open to all signed-in students | OPEN |
| Q7 | Do events have a capacity, and is there a waiting list? | Registration rule, concurrency risk | A7: Capacity is required. No waiting list | OPEN |
| Q8 | Who records attendance, when, and can it be corrected? | Attendance rule and audit | A8: Club officers only, after event start; corrections allowed and audited | OPEN |
| Q9 | What happens to registrations when an event is cancelled? | Data consistency | A9: Event becomes CANCELLED and its registrations become CANCELLED | OPEN |
| Q10 | After a rejected request, may the student ask again? May an approved member leave? | Membership state machine | A10: Re-request allowed after rejection. Leaving a club is out of release 1 | OPEN |
| Q11 | Which administrative report metrics does Student Affairs need? | Report scope | A11: Clubs by status, members per club, events by status, registrations and attendance per event | OPEN |
| Q12 | Which actions must be audited, who may view the audit history, and for how long is it kept? | Audit design | A12: All state-changing decisions and admin actions are recorded. Student Affairs may view. No retention rule in the prototype | OPEN |
| Q13 | Language and accessibility targets (English only? Arabic/right-to-left?) | UI scope | A13: English only, WCAG 2.1 AA as a target for the main flows | OPEN |
| Q14 | Rules for event timing (minimum notice, overlap in the same location)? | Validation rules | A14: Start must be in the future and end after start. No overlap or notice rule | OPEN |
| Q15 | Are club categories a fixed list or free text? | Search and data model | A15: Fixed seeded list | OPEN |
| Q16 | May a club be deactivated or paused, and what happens then? | Possible change request | A16: Not in release 1. The club `status` field is designed to allow more values later | OPEN |

## Unresolved assumptions carried into Milestone 2
All items marked OPEN above. Update the status column when the instructor answers, and record any
requirement that changed because of an answer in the change history of `docs/01-requirements.md`.
