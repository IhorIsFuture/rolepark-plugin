# Changelog

All notable changes to the RolePark plugin for Claude are listed here. The version matches `version` in `.claude-plugin/plugin.json`; raise both with every release.

## [1.0.0] - 2026-10-02

### Added

- RolePark connector reference (https://rolepark.com/api/mcp, OAuth). It is the same server as the RolePark listing in the Connectors directory, so people who have both see one set of tools.
- `briefing` skill: today's interviews, due and overdue tasks, new applications and stuck candidates, with what to do first.
- `shortlist` skill: reviews early-stage applications against the vacancy's requirements, gives reasons and risks, and proposes stage moves that run only after confirmation.
- `interview-prep` skill: an interview brief with a requirements check, earlier feedback, tailored questions and things to verify.
- `find-candidates` skill: skill matching plus a boolean CV search in the company's own database, with an explanation of each match.
- `add-candidate` skill: creates a candidate from a pasted CV or text after a duplicate check and a confirmation card, and can add them to a vacancy.
- `pipeline-update` skill: funnel numbers, bottlenecks and next steps for a vacancy, plus a short update for the hiring manager.
