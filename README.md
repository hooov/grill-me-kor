# grill-me (Codex skill)

Plans one new feature at a time on an existing project. Scans the repo, asks simple bilingual (Korean/English) questions, then writes/updates `AGENTS.md`, `OVERVIEW.md`, and `KANBAN.md` (Korean), and offers to implement.

## Use
Say `grill me` (or "plan a feature") inside a project. Codex will scan the repo, ask a few simple questions, write the planning docs, and ask whether to start building.

## Files
- `SKILL.md` — the workflow Codex follows.
- `agents/openai.yaml` — UI metadata.
- `references/*.template.md` — Korean templates for the three docs.
