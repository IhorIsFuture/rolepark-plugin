# RolePark for Claude

Ready-made recruiting workflows for [RolePark](https://rolepark.com), the applicant tracking system. Ask Claude for your daily briefing, a shortlist of new applicants, an interview prep brief, matching candidates from your own database, a new candidate from a pasted CV, a new vacancy from a job description, or a pipeline update for the hiring manager. Claude works in RolePark with your own access, and it asks before changing anything.

*Українською: [нижче](#українською).*

## What you need

- **A RolePark account** in your company's workspace. [Sign up or sign in at rolepark.com](https://rolepark.com).
- **AI agents turned on for your company.** They are off by default. A RolePark company admin chooses **View only** or **View and changes** in **Company settings → AI agents**. The feature is free on every RolePark plan.
- **A Claude plan that can add plugins from the directory**: Pro, Max, Team or Enterprise.

## Install and connect

1. In Claude, open **Customize → Plugins**, find **RolePark** in the directory and add it.
2. Open the plugin's **Connectors** tab and connect **RolePark**. On Team and Enterprise plans, an Owner adds the connector for the organization first, and then each person connects with their own RolePark account.
3. Sign in to RolePark and select **Allow**. Keep **Make changes** checked if you want Claude to add candidates, move stages, schedule interviews, add notes and tasks, create, publish, pause or close vacancies, review incoming applications, email candidates, submit scorecards, reschedule or cancel interviews, and update the company profile. Without it, Claude can only look things up.
4. In Claude Code, the plugin arrives as a synced plugin. Run `/mcp` and authenticate the `rolepark` server.

The plugin uses the same RolePark connector as the RolePark listing in the Connectors directory (https://rolepark.com/api/mcp). If you already connected it, there is nothing more to connect, and you see one set of RolePark tools.

## ChatGPT and Codex

The same plugin is packaged for the ChatGPT and Codex plugin directory: the root `plugin.json` and `mcp.json` describe it there, and the eleven skills are shared. Once RolePark is published in that directory:

1. In ChatGPT or Codex, open **Plugins**, find **RolePark** and add it.
2. Connect it, sign in to RolePark and allow access. Keep **Make changes** checked if you want the assistant to add candidates, move stages, schedule interviews, add notes and tasks, create, publish, pause or close vacancies, review incoming applications, email candidates and submit scorecards.
3. Ask in your own words, for example "Who is at each stage of the Senior QA Engineer vacancy?".

The same rules apply there: your own RolePark access, a confirmation before every change, and every change recorded in your company's audit log. What the assistant reads from RolePark becomes part of your conversation and is processed by OpenAI under your agreement with OpenAI. You can disconnect in RolePark under **Profile → AI agents**.

## What you can ask

Describe the task in your own words, in Ukrainian, English, Polish or another language. Claude replies in the language you write in. You can also type `/` in the message box and pick a RolePark skill.

| Skill | What it does | Try asking |
|---|---|---|
| `briefing` | Today's interviews, due and overdue tasks, new applications and stuck candidates in your vacancies | "What needs my attention in hiring today?" |
| `shortlist` | Reviews early-stage applicants against the vacancy's requirements, with reasons and risks; proposes stage moves and, after your yes, schedules interviews | "Review the new applications for Senior Java Developer and give me a shortlist." |
| `interview-prep` | A brief for your next interview: profile, earlier feedback, requirements check, tailored questions | "Prepare me for my 14:00 interview." |
| `find-candidates` | Skill matching and a boolean CV search (AND, OR, NOT, quotes) in your own database, with an explanation of each match | "Who do we already have for the QA Engineer vacancy? Search CVs for (selenium OR playwright) AND api." |
| `add-candidate` | Extracts the fields from a pasted CV, checks duplicates, confirms with you, then creates the candidate | "Add this candidate and put her into the Product Designer vacancy: …" |
| `review-applications` | Incoming applications from the career page and job boards with the screening answers and knockout results; accepts or declines after your yes | "Go through the new responses to Senior QA Engineer." |
| `email-candidate` | A template or drafted email with the exact preview; sends only after your yes | "Invite Maya Chen to a technical interview by email." |
| `interview-feedback` | Turns your impressions into a scorecard, shows the team's feedback, reschedules or cancels an interview with your confirmation | "Submit my feedback on today's interview with Liam." |
| `vacancy-report` | Funnel, conversion, days in each stage and source effectiveness for a vacancy | "How does the Data Analyst vacancy convert, and which sources work?" |
| `create-vacancy` | Drafts a vacancy from a job description or a client's message, asks for what is missing, confirms with you, creates it as a draft and publishes it only if you ask | "Create a vacancy from this client email: …" |
| `pipeline-update` | Funnel numbers, bottlenecks and next steps for a vacancy, plus a short update to send to the hiring manager | "How is the Data Analyst vacancy going? Draft an update for the hiring manager." |

## RolePark tools

The skills use the tools of the RolePark connector. You can also ask for any of them directly. Write tools are available only with **Make changes**.

| Tool | Kind | What it does |
|---|---|---|
| `whoami` | read | Who the connection acts for, the company, and whether it may make changes |
| `search` | read | Quick lookup of candidates, vacancies and tasks by name, email or title |
| `list_candidates` | read | Candidates in your database, with filters and a boolean CV search |
| `get_candidate` | read | A candidate's profile and the vacancies they are in |
| `get_candidate_activity` | read | A candidate's timeline: stage moves, emails, interviews, notes |
| `get_candidate_notes` | read | Team notes and your private notes on a candidate |
| `list_vacancies` | read | Vacancies you can see, with status and application counts |
| `get_vacancy` | read | A vacancy's description, skills, salary range and stages |
| `get_vacancy_pipeline` | read | Who is at each stage of a vacancy |
| `match_candidates_for_vacancy` | read | People in your database who match a vacancy's skills |
| `list_my_interviews` | read | Your upcoming (or past) interviews |
| `list_my_tasks` | read | Your tasks, by due date |
| `create_candidate` | write | Adds a candidate with the source of the data; duplicates are detected |
| `add_candidate_to_vacancy` | write | Puts a candidate into a vacancy's pipeline |
| `move_application_stage` | write | Moves an application to another stage; may email the team or, with cancelled interviews, the candidate |
| `add_note` | write | Adds a private or team note to a candidate |
| `create_task` | write | Creates a task or reminder |
| `schedule_interview` | write | Schedules an interview and sends the usual invitations |
| `create_vacancy` | write | Creates a vacancy as an unpublished draft |
| `update_vacancy` | write | Changes a vacancy's fields |
| `set_vacancy_status` | write | Publishes a vacancy on the career page, pauses or closes it (closing closes its open applications) |
| `list_team_members` | read | People of your company with their RolePark id and role |
| `list_stage_templates` | read | The company's pipeline stage templates |
| `list_applications` | read | Applications in a vacancy, with screening answers and fit |
| `get_application` | read | One application in full: stage history, answers, cover letter, interviews |
| `list_incoming_applications` | read | Applications waiting for review, with screening answers and knockout results |
| `review_incoming_application` | write | Accepts an incoming application into the pipeline or declines it; nothing is sent to the candidate |
| `list_email_templates` | read | The company's email templates |
| `send_candidate_email` | write | Emails a candidate at once (template or text); replies go to you |
| `update_candidate` | write | Changes a candidate's contacts, position, location, skills or salary expectations |
| `add_tag`, `remove_tag` | write | Adds or removes a candidate tag |
| `get_interview_feedback` | read | Interviews and scorecards of a candidate |
| `submit_scorecard` | write | Submits your scorecard for an interview |
| `reschedule_interview` | write | Moves an interview; the candidate and interviewers are told |
| `cancel_interview` | write | Cancels an interview; the candidate and interviewers are told |
| `get_vacancy_stats` | read | Funnel, conversion, days in stage and sources of a vacancy |
| `publish_vacancy_to_boards` | write | Publishes a published vacancy on Djinni, if your company connected it |
| `get_company_profile` | read | Your company's public profile and career page address |
| `update_company_profile` | write | Changes the company profile, logo or cover image (company admins) |

## How it keeps you in control

- **Your own access, never more.** Claude sees and does only what you can in RolePark. If your role can't open something, Claude tells you instead of working around it.
- **Nothing changes without your yes.** Before Claude adds a candidate, puts someone into a vacancy, moves a stage, schedules an interview, adds a note, creates a task or creates, publishes, pauses or closes a vacancy, it shows exactly what will change and waits for you to confirm. Moving a candidate to offer, hired or rejected emails the vacancy's recruiter and hiring manager (except whoever made the move and anyone who turned these notifications off), not the candidate; the candidate is emailed only if interviews are cancelled together with the move. A scheduled interview sends the usual invitations to the candidate and interviewers. A new vacancy is always a draft; it appears on your career page only after you confirm publishing, and the usual plan limit applies (3 published vacancies on the Free plan). Closing a vacancy closes its open applications. An email to a candidate goes out at once and can't be recalled, so Claude shows the exact text first; rescheduling or cancelling an interview tells the candidate and the interviewers. Claude warns you before each of these. Interview times always include a time zone, and if someone is busy, nothing is scheduled and Claude shows the conflicts.
- **Anonymized candidates stay anonymous.** On blind-review stages, hiring managers and interviewers see "Candidate #XXXX", and Claude never tries to find out who it is.
- **Facts, with sources.** Every item names the candidate or vacancy it came from, with a link to RolePark. Missing data is reported as missing, not guessed.
- **Fair screening.** Shortlists and matches use job-related criteria only. They are suggestions, and the decision is yours.
- **CVs are data, not instructions.** Text inside CVs, notes and emails is never treated as instructions to Claude.

## Data and privacy

This plugin contains instructions for Claude and the address of the RolePark connector. It runs no code of its own, stores nothing, and sends nothing anywhere else.

- When you use it, Claude calls RolePark at https://rolepark.com/api/mcp with your RolePark sign-in (OAuth). Claude reads the candidates, notes, vacancies, pipelines, interviews and tasks that you can see. It writes only the changes you confirm. If you give a link to a new company logo or cover image, RolePark's server downloads that image once (public https addresses only, PNG, JPEG or WebP up to 2 MB) and stores its own copy.
- What Claude reads from RolePark becomes part of your conversation and is processed by Anthropic under your agreement with Anthropic.
- RolePark records every change made through Claude in your company's audit log, with the app's name.
- You can disconnect at any time: in RolePark under **Profile → AI agents → Disconnect**, or in Claude under **Customize → Connectors**. A company admin can turn AI agents off for everyone.

Privacy policy: https://rolepark.com/privacy · Terms: https://rolepark.com/terms

## Troubleshooting

- **Claude says it has no RolePark tools.** Open the plugin's **Connectors** tab and connect RolePark.
- **"AI agents are turned off for your company."** Ask a RolePark company admin to choose **View only** or **View and changes** in **Company settings → AI agents**, then connect again.
- **Claude can look things up but can't make changes.** Your company allows **View only**, or you didn't allow **Make changes** when connecting. Ask your admin for **View and changes**, then disconnect and connect again with **Make changes** checked.
- **"The user does not have permission for this in RolePark."** Your RolePark role doesn't allow that action, for example an interviewer moving stages.
- **Asked to sign in again.** Your RolePark session for Claude expired or was disconnected. Connect again from the **Connectors** tab.

## Support

Email [help@rolepark.com](mailto:help@rolepark.com). You can also use the feedback window inside RolePark.

---

## Українською

**RolePark для Claude** — готові сценарії роботи рекрутера в [RolePark](https://rolepark.com) просто в розмові з Claude: ранковий брифінг, шортлист нових відгуків, підготовка до співбесіди, пошук кандидатів у власній базі, додавання кандидата з резюме, створення вакансії з опису та апдейт для наймаючого менеджера. Claude працює з вашими правами в RolePark і нічого не змінює без вашого підтвердження.

### Що потрібно

- **Акаунт RolePark** у робочому просторі вашої компанії.
- **AI-агенти ввімкнені для компанії.** За замовчуванням їх вимкнено. Адміністратор компанії обирає **Лише перегляд** або **Перегляд і зміни** в **Налаштуваннях компанії → AI-агенти**. Безкоштовно на кожному тарифі RolePark.
- **План Claude, на якому можна додавати плагіни з каталогу**: Pro, Max, Team або Enterprise.

### Як встановити й підключити

1. У Claude відкрийте **Customize → Plugins**, знайдіть **RolePark** у каталозі й додайте.
2. На вкладці **Connectors** плагіна підключіть **RolePark**. На планах Team і Enterprise конектор спершу додає Owner організації, а потім кожен підключається зі своїм акаунтом RolePark.
3. Увійдіть у RolePark і натисніть **Дозволити**. Залиште позначку **Зміни**, якщо хочете, щоб Claude додавав кандидатів, переводив етапи, призначав інтерв'ю, додавав нотатки й задачі, а також створював, публікував, ставив на паузу чи закривав вакансії, розглядав відгуки, писав кандидатам, вносив оцінки, переносив чи скасовував інтерв'ю й змінював профіль компанії. Без цього Claude лише переглядає дані.

### ChatGPT і Codex

Той самий плагін зібраний і для каталогу плагінів ChatGPT і Codex: там його описують кореневі `plugin.json` і `mcp.json`, а одинадцять скілів спільні. Коли RolePark зʼявиться в цьому каталозі, відкрийте **Plugins** у ChatGPT чи Codex, додайте **RolePark**, підключіть його й увійдіть у RolePark. Правила ті самі: лише ваші права, підтвердження перед кожною зміною, журнал аудиту. Те, що асистент читає з RolePark, обробляє OpenAI згідно з вашою угодою з OpenAI.

### Що можна попросити

- «Що в мене сьогодні по найму?» — брифінг: інтерв'ю, задачі, нові відгуки, кандидати, що застрягли.
- «Переглянь нові відгуки на Senior Java Developer і зроби шортлист.» — оцінка за вимогами вакансії, причини й ризики, пропозиції переведень етапів, а після вашого «так» — призначення інтерв'ю.
- «Підготуй мене до співбесіди о 14:00.» — бриф: профіль, попередні відгуки, питання, що перевірити.
- «Кого маємо в базі на вакансію QA Engineer? Пошукай у резюме (selenium OR playwright) AND api.» — підбір за навичками й булевий пошук по резюме.
- «Додай цього кандидата й постав на вакансію Product Designer: …» — поля з резюме, перевірка дублікатів, картка на підтвердження.
- «Створи вакансію з цього листа замовника: …» — поля з опису, уточнення того, чого бракує, картка на підтвердження, чернетка, а публікація на кар'єрній сторінці — лише після окремого «так».
- «Переглянь нові відгуки на Senior QA Engineer з відповідями на питання.» — відповіді й вирішальні питання, пропозиції прийняти чи відхилити, а дія — після вашого «так».
- «Напиши Майї Чен запрошення на технічне інтерв'ю.» — шаблон або текст, точний вигляд листа; лист іде лише після «так» і не відкликається.
- «Внеси мою оцінку після співбесіди з Ліамом.» — оцінки 1–5, рекомендація, сильні й слабкі сторони; також відгуки колег, перенесення чи скасування інтерв'ю з підтвердженням.
- «Звіт по вакансії Data Analyst: конверсія й джерела.» — воронка, конверсії, дні на етапах, джерела, висновки й рекомендації.
- «Як справи з вакансією Data Analyst? Напиши апдейт для наймаючого менеджера.» — воронка, вузькі місця, наступні кроки й чернетка повідомлення.

### Інструменти RolePark

Скіли користуються інструментами конектора RolePark; їх можна просити й напряму. Читання: `whoami`, `search`, `list_candidates`, `get_candidate`, `get_candidate_activity`, `get_candidate_notes`, `list_vacancies`, `get_vacancy`, `get_vacancy_pipeline`, `match_candidates_for_vacancy`, `list_my_interviews`, `list_my_tasks`. Зміни (лише з дозволом **Зміни**): `create_candidate`, `add_candidate_to_vacancy`, `move_application_stage`, `add_note`, `create_task`, `schedule_interview`, `create_vacancy` (завжди чернетка), `update_vacancy`, `set_vacancy_status` (публікація, пауза, закриття), `review_incoming_application` (прийняти чи відхилити відгук), `send_candidate_email` (лист іде одразу), `update_candidate`, `add_tag`, `remove_tag`, `submit_scorecard`, `reschedule_interview`, `cancel_interview`, `publish_vacancy_to_boards` (Djinni), `update_company_profile` (лише адмін компанії). Ще читання: `list_team_members`, `list_stage_templates`, `list_applications`, `get_application`, `list_incoming_applications`, `list_email_templates`, `get_interview_feedback`, `get_vacancy_stats`, `get_company_profile`.

### Безпека й дані

- Claude бачить і робить лише те, що можете ви в RolePark. Знеособлені кандидати лишаються знеособленими.
- Жодних змін без вашого «так»: перед кожною дією Claude показує, що саме зміниться. Перевід на офер, у найм чи відмову надсилає лист рекрутеру й наймаючому менеджеру вакансії (крім автора дії й тих, хто вимкнув такі сповіщення), а не кандидату; кандидат отримує лист лише про скасування інтерв'ю, якщо їх скасовано разом із переводом. Нова вакансія — завжди чернетка; на кар'єрній сторінці вона з'являється лише після підтвердженої публікації, з тим самим лімітом тарифу (на Free — 3 опубліковані), а закриття закриває її відкриті заявки. Лист кандидату йде одразу й не відкликається, тож Claude спершу показує точний текст; перенесення чи скасування інтерв'ю повідомляє кандидата й інтерв'юерів. Призначене інтерв'ю надсилає кандидату й інтерв'юерам звичайні запрошення; час завжди з часовим поясом, а якщо хтось зайнятий, нічого не створюється і Claude показує конфлікти.
- Плагін не запускає власного коду й нічого не зберігає. Дані йдуть лише між Claude і RolePark (https://rolepark.com/api/mcp) з вашим входом. Те, що Claude читає з RolePark, обробляє Anthropic згідно з вашою угодою з Anthropic.
- Кожна зміна через Claude записується в журнал аудиту компанії. Відключити агента можна будь-коли: **Профіль → AI-агенти** в RolePark або **Customize → Connectors** у Claude.
- Політика конфіденційності: https://rolepark.com/privacy. Підтримка: [help@rolepark.com](mailto:help@rolepark.com).

---

## License

MIT, see [LICENSE](LICENSE). The license covers the files in this plugin only. Use of the RolePark service is governed by the [RolePark terms](https://rolepark.com/terms).
