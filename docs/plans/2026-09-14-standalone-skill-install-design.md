# Standalone Skill Installation Design

## Objective

Make the repository install exactly one Codex skill with one command:

```bash
mkdir -p ~/.codex/skills
git clone https://github.com/IFAKA/faka-mode.git ~/.codex/skills/faka-mode
```

## Design

Treat the repository root as the sole skill package. It contains the canonical
`SKILL.md` and `agents/openai.yaml`. Remove the nested plugin package and its
marketplace metadata so recursive discovery cannot expose a second
`faka-mode` skill.

Update the README to document only the standalone installation flow and its
verification. Plugin installation is out of scope for this repository.

## Verification

After the change, the repository must contain exactly one tracked file named
`SKILL.md`, located at the root, and the documented clone command must place
that skill at `~/.codex/skills/faka-mode/SKILL.md`.
