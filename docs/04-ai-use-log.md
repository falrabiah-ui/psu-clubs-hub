# AI-Use Evidence Log

Record important interactions, not every message. This log is assessed on honest examples of use, correction, and limitations.
Last updated: 2026-10-24.

## 1. Model disclosure
| Item | Value |
|---|---|
| Tools used | Claude (Anthropic) in the claude.ai chat for requirements and design drafting and as a simulated stakeholder. OpenCode for planning only |
| Provider and model name | Claude: Claude Sonnet 5.5 as reported in the conversation. OpenCode: Big Pickle (free model available in OpenCode) |
| Change of model during the project | None so far |
| Approximate cost | Free. No paid plan or paid tokens |
| Limitations that affected our work | (1) The same AI proposed the assumptions and then acted as stakeholder, so its answers are not independent evidence. (2) The AI only had the course slides, not the full stakeholder brief, so some rules are assumptions. (3) The AI drafts contained inconsistencies (AC-10, US-15) that had to be found by review. (4) The chat AI could not run or test anything in our repository, so nothing in Milestone 1 is verified by execution. (5) OpenCode was used only for planning in Milestone 1, so we have no evidence yet about its code quality |
| Data sent to AI | Course documents and project text only. No real student or PSU confidential data |

## 2. Log (Milestone 1 entries)
| # | Phase | Objective and approach | What the AI contributed | Verification and decision |
|---|---|---|---|---|
| 1 | Requirements | Uploaded the course slides and asked what was missing before starting | Listed 12 clarifying questions on team, stack, model, login, approval, attendance | Team answered: three members, free model, no restriction on stack, attendance marked by an officer. Several scope choices (login, front end, event approval) were delegated to the AI. The team had no full brief and no change-request information, so those questions were dropped |
| 2 | Requirements | Asked for stakeholder questions with default assumptions | Drafted Q1 to Q16 with proposed defaults, including the self-decision conflict (Q4) | Defaults used as proposed. The team chose not to send the questions to the instructor because of time and used a simulated stakeholder instead (see section 4) |
| 3 | Requirements | Asked for requirements, stories, acceptance criteria | Drafted FR-01 to FR-18, NFR-01 to NFR-09, US-01 to US-16, AC-01 to AC-35, traceability table | Reviewed the set. AC-10 was found untestable and rewritten (see section 4) |
| 4 | Requirements | No real stakeholder was available, so Q1 to Q16 were put to Claude as a simulated stakeholder and the answers reviewed | Answered all 16: 14 confirmed, 1 changed (Q11 report metric), 1 clarified (Q12 audit view). Q4 was extended | Updated FR-16, AC-31, AC-15, US-15 and the change history. The team accepted the answers. Because the AI answered its own proposals, Q4, Q5 and Q12 are flagged for validation by the instructor or a real stakeholder |
| 5 | Requirements | Reviewed the AI's own draft for consistency | Found AC-10 allowed two outcomes ("404 or 409") and US-15 conflicted with the stated scope | Fixed both (AC-10 now 404 only; US-15 reworded) |
| 6 | Design | Asked for architecture, data model, API contract | Proposed FastAPI + SQLite modular monolith, ER model, endpoint table, role matrix | The team had delegated the stack and design choices ("you choose"), reviewed the result, and accepted it as drafted. No structural changes in Milestone 1. The team must be able to defend each choice (policy module, club-scoped roles, DB constraints) |
| 7 | Design | Asked for decision records | Drafted ADR-001 and ADR-002 with alternatives and consequences | Reviewed. Dates set to 2026-10-24 and status set by the team |
| 8 | Planning | Asked for task plan and risks. OpenCode (Big Pickle) was also used for planning | Drafted T-01 to T-16 and R1 to R10, with tasks split across the three members | Work split accepted as a starting point and will be adjusted in Milestone 2 as skills and time require |

## 3. Failed approaches and recoveries
- The first scripted creation of the repository folder structure failed because the shell did not support brace expansion in the command. The folder was recreated with plain commands and then worked.
- The AI's own draft had two inconsistencies (AC-10, US-15). They were found in a review pass and fixed (section 4).

## 4. Rejected or corrected AI proposals
| Proposal | Why corrected or rejected | Result |
|---|---|---|
| AC-10 "404 or 409" (AI draft) | A criterion with two accepted outcomes cannot be tested precisely | Changed to 404 only |
| US-15 promised an audit history viewer while limitations said none in release 1 | Inconsistent scope | Story reworded to "recorded"; viewer deferred (Q12) |
| AI recommended sending the stakeholder questions to the instructor | The team did not have time to wait for an answer | Used a simulated stakeholder instead. Consequence: answers are unconfirmed and are listed for later validation in `00-stakeholder-questions.md` |

## 5. Notes
- Authorship: the Milestone 1 documents were prepared by the whole team (Faisal Alrabiah, Faisal Alghubaini, Abdulaziz Alfaahdel), with Faisal Alrabiah as team leader and repository owner.
- Stakeholder input was simulated (see `00-stakeholder-questions.md`). It has not been confirmed by PSU or the instructor.
- Implementation, testing, and change-request entries will be added in Milestone 2 using the prompt pattern Context, Goal, Constraints, Verification.