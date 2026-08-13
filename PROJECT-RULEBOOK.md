# Project Rulebook

This document records the standing rules for maintaining the OSSU Computer Science progress repository.

## Source of Truth

> **The repository records reality.**

The GitHub repository is the long-term source of truth for the learning journey. The conversation is the working space for discussion, planning, learning and preparing changes.

## Approval Workflow

1. The user tells ChatGPT what has been done or what should change.
2. ChatGPT inspects the current repository.
3. ChatGPT determines all affected files and shows the proposed changes.
4. The user confirms or approves the proposed changes.
5. ChatGPT updates GitHub.
6. ChatGPT runs the repository update checklist against the resulting repository.
7. ChatGPT reports exactly what changed and what was checked but did not require modification.

## No Silent Changes

- Never omit, alter, remove, reinterpret, or introduce repository content that has not been discussed and agreed upon in this conversation.
- Do not guess when information is ambiguous; ask first.
- Do not make unrelated improvements during an approved update.
- If something appears to need changing but has not been discussed, flag it for discussion rather than changing it silently.

## Long-Term Synchronization Rules

- If a course is completed → update the curriculum and progress records.
- If a paper is started → update the research tracker.
- If something important is discovered → update the relevant research or knowledge notes.
- If something is built → update the relevant project or experiment documentation.
- If the repository structure changes → update the relevant README documentation.
- If anything significant changes → update `CHANGELOG.md`.

## GitHub Update Checklist

Before completing an approved repository update:

```text
[ ] Requested change implemented
[ ] Curriculum status checked
[ ] Research tracker checked
[ ] Research notes updated
[ ] Books / reading sequence checked
[ ] Projects checked
[ ] Experiments checked
[ ] Milestones checked
[ ] README consistency checked
[ ] CHANGELOG updated
[ ] Privacy / public-information check
[ ] Server-name capitalization check
[ ] Markdown / GitHub rendering check
[ ] Final repository structure verified
```

Not every checklist item requires a file change. Each relevant area is checked and only necessary changes are made.

## Documentation and Privacy Rules

- Use normal professional capitalization for headings, topics and technical names.
- Server hostnames are written in lowercase, for example `pve-main`.
- Never publish personal information about the home-server environment in the public repository.
- Do not commit credentials, keys, passwords, private addresses or other sensitive infrastructure information.

## Notes Separation

- `notes/` is for course and general knowledge notes.
- `research/notes/` is for paper-specific research notes.

This separation should be maintained unless a structural change is discussed and approved.
