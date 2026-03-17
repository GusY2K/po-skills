# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Planned
- Multi-runtime native configs (Cursor, Copilot, Windsurf)
- Demo GIF for README
- Hosted documentation

## [2.0.0] - 2026-03-17

### Added
- **`backlog-health-audit` skill** — Scans existing Azure DevOps backlog and generates a 0-100 health score. Detects 12 issue types across 4 severity levels (CRITICAL, HIGH, MEDIUM, LOW): missing acceptance criteria, orphaned tasks, stale items, duplicate titles, empty descriptions, unestimated stories, and more. Optional `--fix` for auto-fixing LOW severity issues.
- **`sprint-planner` skill** — Reads backlog and suggests optimal sprint assignments based on team velocity (auto-calculated from last 3 sprints), priority ordering, and dependency analysis. Flags oversized items, underloaded sprints, and dependency conflicts. Optional `--assign` to move items to iterations after approval.
- **`work-item-templates` skill** — 18 pre-built templates for common patterns: `api-endpoint`, `crud-feature`, `auth-flow`, `database-migration`, `frontend-page`, `dashboard`, `cicd-pipeline`, `monitoring`, `security-hardening`, `bug-fix`, and 8 more. Each generates a complete Feature → Stories → Tasks hierarchy with acceptance criteria and story points.
- GitHub SEO: 12 topic tags, keyword-rich description, npm homepage link
- Social preview image (1280x640) for link unfurling
- CHANGELOG.md following Keep a Changelog format
- `.editorconfig` and `.gitattributes` for code quality signals
- npm downloads and GitHub stars badges in README
- Pushy SKILL.md description with comprehensive trigger list for auto-detection

## [1.1.0] - 2026-03-17

### Added
- Plan review options: show in chat, save to `.md` file, or both
- `--output=<file>` flag to save backlog plan to markdown before creating in Azure DevOps
- User is asked how they want to review the plan before any items are created

### Changed
- Phase 2 (Plan) now has 3 review modes instead of chat-only display
- How it works flow updated from 6 steps to 7 (added REVIEW step)

## [1.0.0] - 2026-03-17

### Added
- `azure-devops-backlog-creator` skill — reads documents and creates full Azure DevOps backlog hierarchy
- Support for Epics, Features, User Stories, Tasks, and Bugs with parent-child relationships
- Acceptance criteria, story points, priority, and tags for all work items
- Process template support: Agile, Scrum, and Basic
- Session tagging (`backlog-creator-YYYYMMDD-HHMMSS`) for bulk querying and rollback
- `--dry-run` flag for previewing without creating
- `--org`, `--project`, `--iteration`, `--area-path`, `--assign-to`, `--tags`, `--priority` arguments
- `scripts/validate-prerequisites.sh` for checking Azure CLI setup
- `scripts/rollback.sh` for undoing a session by tag
- `references/REFERENCE.md` with complete Azure DevOps CLI field reference
- `examples/sample-prd.md` and `examples/sample-output.md`
- `npx po-skills` installer with GUSY2K ASCII banner in #00F0A0
- Multi-runtime installer support (Claude Code, Cursor, Copilot, Windsurf)
- `.claude-plugin/marketplace.json` for plugin discovery
- Apache 2.0 license

[Unreleased]: https://github.com/GusY2K/po-skills/compare/v2.0.0...HEAD
[2.0.0]: https://github.com/GusY2K/po-skills/compare/v1.1.0...v2.0.0
[1.1.0]: https://github.com/GusY2K/po-skills/compare/v1.0.0...v1.1.0
[1.0.0]: https://github.com/GusY2K/po-skills/releases/tag/v1.0.0
