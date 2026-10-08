---
name: vacancy-report
description: Build an analytics report for one RolePark vacancy from its hiring funnel, covering applications at each stage, conversion between stages, average days in each stage, where candidates come from and which sources lead to hires, and incoming applications waiting for review, with conclusions and recommendations. Use when the user asks for vacancy analytics, conversion, time to hire, source effectiveness or a report on how a vacancy performs, for example "звіт по вакансії", "конверсія по етапах", "звідки йдуть кандидати", "raport z rekrutacji". For a quick status update to the hiring manager, the pipeline-update workflow is the better fit.
---

# Vacancy analytics report

Explain how one vacancy performs with real numbers from RolePark: the funnel, conversions, time in stage and sources, then what to change.

## Ground rules

- **Language.** Reply in the language the user writes in.
- **Numbers from RolePark only.** Use what `get_vacancy_stats` returns. Don't extrapolate trends from a handful of applications: with fewer than ~10 applications, say the sample is small.
- **Read-only.** This workflow changes nothing in RolePark.
- **The user's own access.** The report needs ATS access and the analytics permission (admins, recruiters, recruiting leads; not hiring managers). A 403 means the role can't see it; say so.
- **People, not just numbers.** When naming stuck candidates, link them; for anonymized ones keep "Candidate #XXXX".
- **The user's explicit request comes first.** Follow the user's format and scope.

## Steps

1. **Pick the vacancy** with `list_vacancies` (`query`) or `search`; if several match, ask. Ask for a period only if the user mentions one (`from`, `to`).
2. **Get the numbers.** Call `get_vacancy_stats`:
   - `stages`: `now` (applications at the stage), `reached` (ever reached it), `conversionFromPrevious`, `conversionFromTop`;
   - `avgDaysInStage` with `samples`;
   - `sources` with applications and hires (over the latest 500 applications);
   - `incomingPending`, `withdrawn`, `totalApplications`.
3. **Add context** if useful: `get_vacancy` (opened date, headcount, requirements) and `get_vacancy_pipeline` to name the candidates behind a bottleneck.
4. **Find the story.**
   - The biggest drop in conversion and the slowest stage (most days, enough samples).
   - Sources that bring volume versus sources that bring hires.
   - Incoming applications waiting for review.
5. **Write the report** (template below): headline, funnel table, time in stage, sources, 3 conclusions, 3 recommendations with an owner each.

## Output

```markdown
**[Senior QA Engineer](https://rolepark.com/vacancies/…)** — 42 applications, 1 hired, 3 withdrawn, 5 incoming waiting

| Stage | Now | Reached | From previous | From top |
|---|---|---|---|---|
| New | 9 | 42 | 100% | 100% |
| Screening | 6 | 21 | 50% | 50% |
| Tech interview | 3 | 8 | 38% | 19% |
| Offer | 1 | 2 | 25% | 5% |
| Hired | 1 | 1 | 50% | 2% |

Time in stage: New 4.2 days (35 apps) · Screening 6.8 days (19) · Tech interview 11.5 days (7)

Sources: LinkedIn 20 → 1 hire · career page 14 → 0 · referral 5 → 0 · Djinni 3 → 0

**Conclusions**
1. The biggest drop is screening → tech interview (38%): the must-haves filter late.
2. Tech interview is the slowest stage (11.5 days): feedback waits.
3. LinkedIn brings the only hire; the career page brings volume but no one past screening yet.

**Recommendations**
1. Recruiter: add a deciding screening question for test automation.
2. Hiring manager: feedback within 2 days after each tech interview.
3. Recruiter: review the 5 waiting incoming applications this week.
```

## Gotchas

- `reached` counts applications that ever reached a stage, so it can be larger than `now`.
- Custom stages are counted in `otherStages`, not in the standard rows: say so, and take their counts from `get_vacancy_pipeline` if the user needs them.
- No RolePark tools available means RolePark isn't connected. Tell the user to connect RolePark from the plugin (in Claude: the plugin's Connectors tab; in ChatGPT or Codex: the RolePark plugin in Plugins).
