# FAKA Mode

A Codex skill for high-SNR, answer-first, low-friction interaction.

FAKA Mode changes **how Codex works with you**. It does not add domain knowledge. It shapes output and agent behavior so Codex is more likely to:

- lead with the answer, recommendation, fix, or command;
- keep information density high;
- preserve context and prior decisions;
- do available research/tool work itself instead of delegating it back to you;
- adapt its response shape to coding, debugging, research, decisions, explanations, writing, and execution;
- challenge bad assumptions when they materially affect the outcome;
- scale depth to stakes instead of being uniformly terse or verbose.

## Mental model

```text
your request
    ↓
Codex reasoning + tools
    ↓
FAKA Mode
    ↓
a response optimized for useful information per unit of attention
```

## Example

Instead of:

> There are several factors to consider when deciding whether to build or buy...

FAKA Mode pushes toward:

> **Pay $100. You are effectively buying back 20 hours for $5/hour.** Build only if the feature is strategic, highly custom, or creates unacceptable vendor risk.

## Install

### Recommended

```bash
mkdir -p ~/.codex/skills
git clone https://github.com/IFAKA/faka-mode.git ~/.codex/skills/faka-mode
```

Restart Codex after installing.

### Verify

```bash
python3 "$(find ~/.codex -path '*/skill-creator/scripts/quick_validate.py' -print -quit)"   ~/.codex/skills/faka-mode
```

Expected:

```text
Skill is valid!
```

Then start a fresh Codex session and ask a normal question without mentioning the skill:

```text
Explain why SQLite uses a B-tree.
```

If Codex shows that it read `SKILL.md (faka-mode skill)`, implicit invocation is working.

## Implicit invocation

`agents/openai.yaml` allows implicit invocation:

```yaml
policy:
  allow_implicit_invocation: true
```

This makes FAKA Mode eligible to load automatically when Codex decides the task matches its description.

It does **not** guarantee that the skill is loaded on every turn. Skills are dynamically selected by Codex.

You can always invoke it explicitly:

```text
$faka-mode Explain virtual memory.
```

## What this skill is for

FAKA Mode is best thought of as an **interaction protocol**.

It is useful when you want Codex to:

- answer before explaining;
- avoid filler and generic recaps;
- keep the visible working set small while still doing thorough analysis;
- search, inspect files, or use tools instead of telling you to do mechanical work yourself;
- distinguish facts, estimates, inference, and speculation;
- avoid blindly optimizing a proxy such as "cheapest" or "fastest" when that would hurt the real objective.

## What this skill is not

It is not:

- a coding framework;
- a knowledge pack;
- an ADHD treatment or medical tool;
- a guarantee that every response will be shorter;
- a replacement for task-specific skills.

For deep teaching, deployment workflows, migrations, debugging frameworks, or other specialized tasks, Codex can combine FAKA Mode with more specific skills.

## Customize it

This skill was built from repeated real-world interaction preferences, so some defaults are opinionated.

Fork it and edit `SKILL.md` if you prefer different behavior. Useful things to customize:

- how aggressive recommendation-first behavior should be;
- whether Codex should challenge premises;
- preferred response length;
- how much state should be surfaced across turns;
- whether you want more or fewer explicit tradeoffs.

## Files

```text
.
├── README.md
├── SKILL.md
├── LICENSE
└── agents/
    └── openai.yaml
```

`SKILL.md` contains the actual behavior.

`agents/openai.yaml` enables implicit invocation.

## License

MIT
