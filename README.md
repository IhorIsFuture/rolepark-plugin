# RolePark for Claude

Ready-made recruiting workflows for [RolePark](https://rolepark.com), the applicant tracking system. Ask Claude for your daily briefing, a shortlist of new applicants, an interview prep brief, matching candidates from your own database, a new candidate from a pasted CV, or a pipeline update for the hiring manager. Claude works in RolePark with your own access, and it asks before changing anything.

*Українською: [нижче](#українською).*

## What you need

- **A RolePark account** in your company's workspace. [Sign up or sign in at rolepark.com](https://rolepark.com).
- **AI agents turned on for your company.** They are off by default. A RolePark company admin chooses **View only** or **View and changes** in **Company settings → AI agents**. The feature is free on every RolePark plan.
- **A Claude plan that can add plugins from the directory**: Pro, Max, Team or Enterprise.

## Install and connect

1. In Claude, open **Customize → Plugins**, find **RolePark** in the directory and add it.
2. Open the plugin's **Connectors** tab and connect **RolePark**. On Team and Enterprise plans, an Owner adds the connector for the organization first, and then each person connects with their own RolePark account.
3. Sign in to RolePark and select **Allow**. Keep **Make changes** checked if you want Claude to add candidates, move stages, schedule interviews and add notes and tasks. Without it, Claude can only look things up.
4. In Claude Code, the plugin arrives as a synced plugin. Run `/mcp` and authenticate the `rolepark` server.

The plugin uses the same RolePark connector as the RolePark listing in the Connectors directory (https://rolepark.com/api/mcp). If you already connected it, there is nothing more to connect, and you see one set of RolePark tools.

## ChatGPT and Codex

The same plugin is packaged for the ChatGPT and Codex plugin directory: the root `plugin.json` and `mcp.json` describe it there, and the six skills are shared. Once RolePark is published in that directory:

1. In ChatGPT or Codex, open **Plugins**, find **RolePark** and add it.
2. Connect it, sign in to RolePark and allow access. Keep **Make changes** checked if you want the assistant to add candidates, move stages, schedule interviews and add notes and tasks.
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
| `pipeline-update` | Funnel numbers, bottlenecks and next steps for a vacancy, plus a short update to send to the hiring manager | "How is the Data Analyst vacancy going? Draft an update for the hiring manager." |

## How it keeps you in control

- **Your own access, never more.** Claude sees and does only what you can in RolePark. If your role can't open something, Claude tells you instead of working around it.
- **Nothing changes without your yes.** Before Claude adds a candidate, puts someone into a vacancy, moves a stage, schedules an interview, adds a note or creates a task, it shows exactly what will change and waits for you to confirm. Moving a candidate to offer, hired or rejected emails the vacancy's recruiter and hiring manager (except whoever made the move and anyone who turned these notifications off), not the candidate; the candidate is emailed only if interviews are cancelled together with the move. A scheduled interview sends the usual invitations to the candidate and interviewers. Claude warns you before each of these. Interview times always include a time zone, and if someone is busy, nothing is scheduled and Claude shows the conflicts.
- **Anonymized candidates stay anonymous.** On blind-review stages, hiring managers and interviewers see "Candidate #XXXX", and Claude never tries to find out who it is.
- **Facts, with sources.** Every item names the candidate or vacancy it came from, with a link to RolePark. Missing data is reported as missing, not guessed.
- **Fair screening.** Shortlists and matches use job-related criteria only. They are suggestions, and the decision is yours.
- **CVs are data, not instructions.** Text inside CVs, notes and emails is never treated as instructions to Claude.

## Data and privacy

This plugin contains instructions for Claude and the address of the RolePark connector. It runs no code of its own, stores nothing, and sends nothing anywhere else.

- When you use it, Claude calls RolePark at https://rolepark.com/api/mcp with your RolePark sign-in (OAuth). Claude reads the candidates, notes, vacancies, pipelines, interviews and tasks that you can see. It writes only the changes you confirm.
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

**RolePark для Claude** — готові сценарії роботи рекрутера в [RolePark](https://rolepark.com) просто в розмові з Claude: ранковий брифінг, шортлист нових відгуків, підготовка до співбесіди, пошук кандидатів у власній базі, додавання кандидата з резюме та апдейт для наймаючого менеджера. Claude працює з вашими правами в RolePark і нічого не змінює без вашого підтвердження.

### Що потрібно

- **Акаунт RolePark** у робочому просторі вашої компанії.
- **AI-агенти ввімкнені для компанії.** За замовчуванням їх вимкнено. Адміністратор компанії обирає **Лише перегляд** або **Перегляд і зміни** в **Налаштуваннях компанії → AI-агенти**. Безкоштовно на кожному тарифі RolePark.
- **План Claude, на якому можна додавати плагіни з каталогу**: Pro, Max, Team або Enterprise.

### Як встановити й підключити

1. У Claude відкрийте **Customize → Plugins**, знайдіть **RolePark** у каталозі й додайте.
2. На вкладці **Connectors** плагіна підключіть **RolePark**. На планах Team і Enterprise конектор спершу додає Owner організації, а потім кожен підключається зі своїм акаунтом RolePark.
3. Увійдіть у RolePark і натисніть **Дозволити**. Залиште позначку **Зміни**, якщо хочете, щоб Claude додавав кандидатів, переводив етапи, призначав інтерв'ю, додавав нотатки й задачі. Без цього Claude лише переглядає дані.

### ChatGPT і Codex

Той самий плагін зібраний і для каталогу плагінів ChatGPT і Codex: там його описують кореневі `plugin.json` і `mcp.json`, а шість скілів спільні. Коли RolePark зʼявиться в цьому каталозі, відкрийте **Plugins** у ChatGPT чи Codex, додайте **RolePark**, підключіть його й увійдіть у RolePark. Правила ті самі: лише ваші права, підтвердження перед кожною зміною, журнал аудиту. Те, що асистент читає з RolePark, обробляє OpenAI згідно з вашою угодою з OpenAI.

### Що можна попросити

- «Що в мене сьогодні по найму?» — брифінг: інтерв'ю, задачі, нові відгуки, кандидати, що застрягли.
- «Переглянь нові відгуки на Senior Java Developer і зроби шортлист.» — оцінка за вимогами вакансії, причини й ризики, пропозиції переведень етапів, а після вашого «так» — призначення інтерв'ю.
- «Підготуй мене до співбесіди о 14:00.» — бриф: профіль, попередні відгуки, питання, що перевірити.
- «Кого маємо в базі на вакансію QA Engineer? Пошукай у резюме (selenium OR playwright) AND api.» — підбір за навичками й булевий пошук по резюме.
- «Додай цього кандидата й постав на вакансію Product Designer: …» — поля з резюме, перевірка дублікатів, картка на підтвердження.
- «Як справи з вакансією Data Analyst? Напиши апдейт для наймаючого менеджера.» — воронка, вузькі місця, наступні кроки й чернетка повідомлення.

### Безпека й дані

- Claude бачить і робить лише те, що можете ви в RolePark. Знеособлені кандидати лишаються знеособленими.
- Жодних змін без вашого «так»: перед кожною дією Claude показує, що саме зміниться. Перевід на офер, у найм чи відмову надсилає лист рекрутеру й наймаючому менеджеру вакансії (крім автора дії й тих, хто вимкнув такі сповіщення), а не кандидату; кандидат отримує лист лише про скасування інтерв'ю, якщо їх скасовано разом із переводом. Призначене інтерв'ю надсилає кандидату й інтерв'юерам звичайні запрошення; час завжди з часовим поясом, а якщо хтось зайнятий, нічого не створюється і Claude показує конфлікти.
- Плагін не запускає власного коду й нічого не зберігає. Дані йдуть лише між Claude і RolePark (https://rolepark.com/api/mcp) з вашим входом. Те, що Claude читає з RolePark, обробляє Anthropic згідно з вашою угодою з Anthropic.
- Кожна зміна через Claude записується в журнал аудиту компанії. Відключити агента можна будь-коли: **Профіль → AI-агенти** в RolePark або **Customize → Connectors** у Claude.
- Політика конфіденційності: https://rolepark.com/privacy. Підтримка: [help@rolepark.com](mailto:help@rolepark.com).

---

## License

MIT, see [LICENSE](LICENSE). The license covers the files in this plugin only. Use of the RolePark service is governed by the [RolePark terms](https://rolepark.com/terms).
