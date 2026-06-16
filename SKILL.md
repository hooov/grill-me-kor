---
name: grill-me-kor
description: Plan a new feature on an existing project by interviewing the user with simple bilingual (Korean/English) questions, then writing or updating AGENTS.md, OVERVIEW.md, and KANBAN.md. Use when the user says "grill me", wants to plan a new feature, or asks Codex to scope/design work before implementing. 사용자가 무언가를 새로 만들거나 추가하고 싶다고 말할 때, 또는 "만들고 싶어", "추가하고 싶어" 같은 표현을 쓸 때 사용하세요.
---

# grill-me-kor

This skill plans **one new feature at a time** on a project that usually **already exists**.
The user is a non-technical "vibe coder". Keep every question simple and free of system-design jargon. Do the technical decomposition yourself; never ask the user to design the architecture.

Questions are asked **bilingually**: Korean first, then English. This applies to **both the question text AND every answer option**. Each option must show the Korean label followed by its English translation, e.g.

```
이 기능이 무엇을 해야 하나요? / What should this feature do?
1. 숫자 입력칸 2개 + "계산" 버튼 / Two number fields + a "Calculate" button
2. 한 줄에 입력하면 바로 결과 표시 / Enter on one line, show result instantly
```

Never show an option in only one language.

All generated files (AGENTS.md, OVERVIEW.md, KANBAN.md) are written in **Korean only**.

Follow the workflow below in order.

## 1. Scan the repo first (do not ask the user about this)

Inspect the workspace before asking anything:

- File tree and overall structure.
- `package.json` scripts; detect framework (Vite, Next.js, Remix, CRA, etc.) and test/lint tools (Vitest, Jest, Playwright, Cypress, ESLint, typecheck).
- Existing `AGENTS.md`, `OVERVIEW.md`, `KANBAN.md` at repo root — read them so you can merge, not overwrite.
- Existing features already built (e.g. a Twitch subs/bits dashboard) so OVERVIEW reflects reality.

Use this scan to fill in the technical details yourself. Only ask the user about the new feature's intent.

## 2. Grill the user about the NEW feature

Ask **one question at a time** and wait for the answer. Keep it simple. Present 2–4 concrete options for each question. **Both the question and every option must be bilingual (Korean / English).**

- If the current Codex surface exposes a structured user-input tool (e.g. Plan mode), use it so options render as a multiple-choice prompt.
- Otherwise, ask inline in chat with numbered options the user can reply to by number.

Cover only these, in plain language. Skip or merge any the scan already answers; add follow-ups only where the answer is vague:

1. Goal — 이 기능이 무엇을 해야 하나요? / What should this feature do?
2. Behavior — 사용자가 무엇을 보거나 할 수 있어야 하나요? / What should the user see or be able to do?
3. Done criteria — 언제 완성된 걸로 볼까요? / How do we know it's finished?
4. Fit — 기존 기능 중 어디에 연결되나요? / Where does it connect to what already exists?
5. Out of scope — 하지 말아야 할 것이 있나요? / Anything it should NOT do?

After each answer, acknowledge in 1 sentence, then ask the next question.

## 3. Write / merge the three files (Korean only, repo root)

If a file already exists, **merge in place and preserve existing content and history**. Never clobber prior revision logs or the CHANGELOG.

If the workspace is a git repo, ensure `AGENTS.md`, `OVERVIEW.md`, and `KANBAN.md` are listed in `.gitignore` (add them if missing).

Use the templates in `references/` as the structure:

- **AGENTS.md** (`references/AGENTS.template.md`): pointer block telling Codex to read OVERVIEW.md and KANBAN.md before planning; planning workflow; verification section.
  - Verification commands: infer from `package.json` scripts and the detected framework. Prefer existing scripts over inventing them. Separate default checks from expensive/full checks. Phrase as "run the relevant checks", not "always run everything". If a check is missing or blocked, instruct Codex to report that and say what it ran instead.
- **OVERVIEW.md** (`references/OVERVIEW.template.md`): living current-state doc. Regenerate the current-state sections (features, tech stack, mapping) from the scan plus the new feature, then append a dated entry to the revision log at the bottom describing what changed this session.
- **KANBAN.md** (`references/KANBAN.template.md`): Roadmap + ordered To Do + In Progress. Add the new feature's tasks to To Do as an ordered list (you decompose them). Keep the board clean: when a task is done it moves to the CHANGELOG section with a date.

Date format: `YYYY-MM-DD`.

## 4. Offer to implement

After writing the files, ask the user (bilingual) whether to start implementing the top To Do task now:
`지금 첫 번째 작업을 구현할까요? / Should I start the first task now?`

- If no: stop. Planning is complete.
- If yes: move that task to **In Progress** in KANBAN.md, implement it, then run the relevant verification checks. On success, move the task to the CHANGELOG with today's date and add a matching dated entry to the OVERVIEW revision log.