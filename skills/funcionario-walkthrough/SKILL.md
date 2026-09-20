---
name: funcionario-walkthrough
description: 'Guide a human review of a commit, PR, file, or directory. Use when invoked by name'
---

Run the following command exactly once without changing the current working directory. Replace `{project-root}` with the absolute path to the project root and `{skill-root}` with the absolute path to this skill's directory:

```bash
uv run --no-cache "{project-root}/_funcionario/scripts/render_skill.py" --project-root "{project-root}" --skill "{skill-root}"
```

- On success, the command prints `read and follow` and an absolute path to a rendered `workflow.md`. Read that file and follow it.
- If `{project-root}/_funcionario/scripts/render_skill.py` is not found, this Funcionário Infinito installation is not set up yet: read the installed `funcionario` skill's SKILL.md (a sibling of this skill's directory) and follow its setup flow, then run the command above once more.
- On any other failure (including `uv` being unavailable), report the command output and HALT. Do not run any workflow source directly.
