# Personal Claude Code skills

Skills available to every project, on every machine.

This repo *is* `~/.claude/skills/`. Each top-level directory is one skill
containing a `SKILL.md`. The `synced/` directory is managed by claude.ai
account sync and is gitignored — it is not part of this repo.

## Setup on a new machine

`~/.claude/skills/` usually already exists (account-synced skills live in
`synced/`), so adopt the directory rather than cloning over it:

```sh
mkdir -p ~/.claude/skills && cd ~/.claude/skills
git init -b main
git remote add origin git@github.com:yitzhach/skills.git
git fetch origin
git reset --hard origin/main   # safe: synced/ is gitignored and untouched
```

If `~/.claude/skills/` does not exist yet, a plain clone also works:

```sh
git clone git@github.com:yitzhach/skills.git ~/.claude/skills
```

Restart Claude Code afterwards — skills are loaded at session start.

## Day to day

```sh
cd ~/.claude/skills
git pull            # pick up changes made on another machine
git add -A && git commit -m "Add x skill" && git push
```

Edits take effect on the next Claude Code session. No install step.

## Adding a skill

```
~/.claude/skills/my-skill/SKILL.md
```

```markdown
---
name: my-skill
description: What it does, and explicitly when to use it.
---

# My skill

Instructions go here.
```

Two rules worth respecting:

- `name` must match the directory name.
- `description` is the only text the model sees when deciding whether to
  load the skill. Write it as a trigger, not a summary: say when to use it
  and name the words a request would actually contain.

Supporting files (scripts, references, templates) can sit alongside
`SKILL.md` in the skill's directory and be referenced by relative path.

## Scope

Keep project-specific skills in that project's own `.claude/skills/`, where
they are versioned with the code and shared with contributors. This repo is
for skills that apply everywhere, regardless of what you are working on.
