# Changelog

All notable changes to the RolePark plugin for Claude are listed here. The version matches `version` in `.claude-plugin/plugin.json` (Claude) and in the root `plugin.json` (ChatGPT and Codex); raise both with every release.

## [1.2.2] - 2026-10-03

### Changed

- The plugin source is now public at https://github.com/IhorIsFuture/rolepark-plugin; `repository` in both manifests points there.

## [1.2.1] - 2026-10-03

### Fixed

- Who is emailed when a candidate moves to offer, hired or rejected: the vacancy's recruiter and hiring manager (except whoever made the move and anyone who turned these notifications off), not the candidate. The candidate is emailed only if interviews are cancelled together with the move. `shortlist`, the README (EN and UA) and the ChatGPT review test case no longer say a rejection emails the candidate.
- Stage order: `schedule_interview` may move the application forward to the interview's stage as the company's stage-order rule allows, under the default rule only when that stage is the next one. `shortlist` and the ChatGPT review test case say so instead of assuming any stage can be reached.

## [1.2.0] - 2026-10-02

### Added

- Packaging for the ChatGPT and Codex plugin directory in the same repository: a portable root `plugin.json` (Agent Plugins 1.0.0) with the OpenAI listing, review test cases, release notes and a Ukrainian translation under `extensions.com.openai`, and a root `mcp.json` with the same RolePark server (`https://rolepark.com/api/mcp`, Streamable HTTP). The Claude manifest and `.mcp.json` are unchanged.
- Listing images in `assets/`: `logo.png`, `logo-dark.png`, `logo-1024.png`, and four 706×800 screenshots in `assets/screenshots/`.

### Changed

- Skills use provider-neutral wording, so they read the same in Claude, ChatGPT and Codex. The "not connected" hint names where to connect in each product.
- Each skill states that the user's explicit request about format, scope or order comes first, while the access, confirmation, fairness and data rules still apply.

## [1.1.0] - 2026-10-02

### Added

- Interview scheduling with the connector's new `schedule_interview` tool. `shortlist` offers to schedule interviews for candidates it moved into an interview stage, and `interview-prep` can schedule one when none exists yet. Claude confirms the exact time with the time zone, duration, type and interviewers first, warns that RolePark sends the usual invitations to the candidate and interviewers, and shows conflicts instead of retrying when someone is busy.

## [1.0.0] - 2026-10-02

### Added

- RolePark connector reference (https://rolepark.com/api/mcp, OAuth). It is the same server as the RolePark listing in the Connectors directory, so people who have both see one set of tools.
- `briefing` skill: today's interviews, due and overdue tasks, new applications and stuck candidates, with what to do first.
- `shortlist` skill: reviews early-stage applications against the vacancy's requirements, gives reasons and risks, and proposes stage moves that run only after confirmation.
- `interview-prep` skill: an interview brief with a requirements check, earlier feedback, tailored questions and things to verify.
- `find-candidates` skill: skill matching plus a boolean CV search in the company's own database, with an explanation of each match.
- `add-candidate` skill: creates a candidate from a pasted CV or text after a duplicate check and a confirmation card, and can add them to a vacancy.
- `pipeline-update` skill: funnel numbers, bottlenecks and next steps for a vacancy, plus a short update for the hiring manager.
