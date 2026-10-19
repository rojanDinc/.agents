# .agents

Reusable skills for AI coding agents.

## Skills

### General

| Skill | Purpose |
| --- | --- |
| `small-committable-batches` | Split any code or docs change into small, self-contained batches that can each be committed and reviewed on their own |

## Adding a skill

1. Create `skills/<skill-name>/SKILL.md` with frontmatter:

   ```markdown
   ---
   name: <skill-name>
   description: When the agent should use this skill
   ---

   Instructions for the agent.
   ```

2. Allow it in `.gitignore`. The file ignores everything by default and allows paths explicitly:

   ```
   !skills/<skill-name>/**
   ```

3. Commit.

## Version control

`.gitignore` is an allowlist: everything is ignored unless explicitly un-ignored. Only `README.md` and the skills listed in `.gitignore` are tracked. Local state in `.crush/` and the `skills/synced/` directory stay out of the repo.
