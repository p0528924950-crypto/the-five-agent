# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Vault Workflow (Mandatory)

At the **start of every task**, invoke the `obsidian-vault-workflow` skill:
- Identify the task topic, locate the matching topic file in `vault/`, read its Overview + Session Log.
- Also read the 2–3 most recent entries in `vault/Meeting Notes/`.

At the **end of every task**, append a dated session log entry to the topic file (create the file if it doesn't exist) and update `_index.md`.

Skip only for pure read-only questions that touch zero files and produce zero decisions.

See full protocol: `skills/obsidian-vault-workflow/SKILL.md`
