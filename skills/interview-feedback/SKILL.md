---
name: interview-feedback
description: Turn the user's impressions after an interview into a RolePark scorecard (ratings 1–5, recommendation, strengths, weaknesses, notes), show it and submit it only after the user confirms; also shows the feedback colleagues already left, and can reschedule or cancel an interview with the user's confirmation. Use when the user wants to leave or submit interview feedback, rate a candidate after an interview, see the team's scorecards, or move or cancel an interview, for example "внеси оцінку після співбесіди", "які відгуки інтерв'юерів", "перенеси інтерв'ю", "oceń kandydata po rozmowie".
---

# Interview feedback and scorecards

Help the user record a fair, evidence-based scorecard for an interview they took part in, read the team's feedback, and change an interview's time or cancel it — each change only after the user confirms.

## Ground rules

- **Language.** Reply in the language the user writes in. Write the scorecard text in the same language unless the user asks otherwise.
- **The user's own words.** A scorecard records the user's judgement. Draft it from what the user tells you and from RolePark facts; never invent strengths, weaknesses or ratings. If the user gives no rating for a criterion, leave it empty.
- **Fair evaluation.** Only job-related evidence: skills shown, answers, problem solving, communication, experience relevance. Never mention or infer age, gender, ethnicity, nationality, religion, disability, health, family status, accent or appearance. If the user's notes contain such remarks, leave them out and say why.
- **The user's own access.** Interviewers can rate only interviews assigned to them; hiring managers see only their own scorecards. A 403 means the role can't; say so.
- **Anonymized candidates.** Keep "Candidate #XXXX" if that's what RolePark shows.
- **Changes only after a yes.** `submit_scorecard`, `reschedule_interview` and `cancel_interview` run only after the user confirmed exactly what you showed. Rescheduling and cancelling email the candidate and the interviewers (or update their calendars) and can't be recalled.
- **The user's explicit request comes first.** Follow the user's format; the fairness and confirmation rules still apply.

## Steps — scorecard

1. **Find the interview.** Call `list_my_interviews` with `includePast: true` and pick the one the user means (candidate, vacancy, date). If unclear, ask.
2. **Read the context.** Call `get_vacancy` for the requirements and `get_interview_feedback` for the candidate and vacancy: earlier scorecards, and `canEvaluate` for this interview. If the user already submitted one, say so: RolePark keeps one scorecard per person per interview.
3. **Draft the scorecard** from the user's notes:
   - ratings 1–5 for technical skills, communication, culture fit, experience relevance and problem solving (only those the user can judge);
   - recommendation: `strong_hire`, `hire`, `no_hire` or `strong_no_hire`;
   - strengths and weaknesses — specific, with evidence from the interview;
   - notes — open questions, things to verify next.
4. **Show it** (template below) and ask "Submit? (yes / change …)".
5. **On an explicit yes**, call `submit_scorecard`. An interview that hasn't happened yet or was cancelled can't take a submitted scorecard. Don't save drafts from here: a draft can't be finished through the connector, and RolePark then refuses a second scorecard for the same interview (`SCORECARD_DRAFT_EXISTS`) — if that happens, tell the user to finish the draft in RolePark.
6. **Report** what was saved, with the candidate link.

## Steps — team feedback

Call `get_interview_feedback` and summarise per interview: who evaluated, ratings, recommendation, the main strengths and concerns, and where evaluators disagree. Don't average away disagreement; point it out.

## Steps — reschedule or cancel

- **Reschedule:** agree the new start with a time zone offset (for example `2026-10-14T15:00:00+03:00`) and, optionally, the duration (30, 45, 60 or 90 minutes). Only a scheduled interview that hasn't started and has no submitted scorecards can be moved, and not more than a year ahead; for others, offer to schedule a new interview. Show old → new time and who will be notified, then call `reschedule_interview` after a yes. If an interviewer is busy, nothing changes and RolePark lists the conflicts — propose another time instead of retrying.
- **Cancel:** show the interview and that the candidate and interviewers will be told, then call `cancel_interview` after a yes. The application's stage doesn't change. An interview whose start time has passed can't be cancelled from here: its outcome is recorded in RolePark.

## Output

```markdown
**Scorecard — [Maya Chen](https://rolepark.com/candidates/…), technical interview, 14 Oct**

| Criterion | Rating |
|---|---|
| Technical skills | 4 |
| Problem solving | 4 |
| Communication | 5 |
| Experience relevance | 3 |

Recommendation: **hire**
Strengths: designed an API test suite from scratch in the exercise; clear reasoning about flaky tests.
Weaknesses: limited load-testing experience (only JMeter basics).
Notes: check Playwright depth in the final round.

Submit? (yes / change …)
```

## Gotchas

- `MAIL_DAILY_CAP` in a reply means the company's daily email limit is reached and the notices weren't sent. Tell the user when it resets and don't retry.

- Ratings are whole numbers 1–5; at least one rating or the recommendation is needed for a submitted scorecard.
- Interviews booked by the candidate in Calendly can't be moved from RolePark.
- No RolePark tools available means RolePark isn't connected. Tell the user to connect RolePark from the plugin (in Claude: the plugin's Connectors tab; in ChatGPT or Codex: the RolePark plugin in Plugins).
