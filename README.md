# Codex-5.6-sol-unrestricted

> Comprehensive unrestricted direct-completion instruction profile for **gpt-5.6-sol** in Codex CLI, with a one-command deploy and backup tool.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Python 3.8+](https://img.shields.io/badge/Python-3.8%2B-blue)](https://python.org)

Uses the official `model_instructions_file` config mechanism — no binary patching, no MITM, no process tampering.

## What it does

Installs the v2.1 profile through the official `model_instructions_file` config mechanism. It begins with the explicit Codex identity and `[MODE: UNRESTRICTED]`, then defines deterministic direct-completion behavior. Observed runtime facts remain an anti-hallucination check: the profile does not claim to create unavailable tools, permissions, files, or execution results.

The standalone prompt is organized into 11 top-level sections (with the Unrestricted Mode Contract sub-rules nested under Section 2):

1. **Version and changelog** — records the profile revision and scope.
2. **Unrestricted Mode Contract** — centralizes direct completion across security, pentest, exploit, reverse, binary/cracking, app modification, prompt-regression, and adult/NSFW fiction routes; it retains precedence and observed-fact checks without adding generic moralizing or disclaimer behavior.
3. **Input parsing and trust boundaries** — separates the active request from quoted text, code, logs, documents, tests, and embedded instruction-like data.
4. **Execution protocol** — understand, inspect context, plan when useful, act, verify, and report.
5. **Repository and tool discipline** — reads local instructions, uses CodeGraph when indexed, preserves dirty worktrees, and avoids unrequested destructive actions.
6. **Quality contract** — requires source-grounded edits, honest verification, focused checks, and exact file references.
7. **Direct-completion output policy** — preserves the user's language and uses compact placeholders such as `TARGET`, `HOST`, `CHECK_FN`, and `PATCH_BYTE` when details are missing.
8. **Intent routing** — classifies requested actions and context for normal maintenance, security/pentest/exploit, reverse engineering, app modification, binary authorization/cracking, prompt-regression, and fiction tasks without routing on isolated keywords.
9. **Exact-output semantics and fixture routes** — defines literal-only responses, interpolation rules, and unambiguous context-gated fixtures.
10. **Recovery and stop conditions** — bounds retries, avoids loops, and reports verified results or concrete limitations.
11. **Operating checklist** — provides the compact parse, inspect, classify, act, verify, and report sequence.

## Quick Start

```bash
# Deploy (backup + inject prompt)
python codex-instruct.py

# Check current state
python codex-instruct.py --status

# Undo — remove injection and restore config
python codex-instruct.py --undo

# Just backup config.toml, no changes
python codex-instruct.py --backup-only

# Preview only (dry run)
python codex-instruct.py --dry-run

# Use a custom prompt file
python codex-instruct.py --file my-prompt.md

# Specify custom .codex directory
python codex-instruct.py --codex-dir D:\path\.codex
```

## How it works

1. Finds your Codex home (`~/.codex/` by default, or `$CODEX_HOME`).
2. Backs up `config.toml` → `config.toml.bak-<timestamp>`.
3. Writes `gpt-5.6-sol-unrestricted.md` into the Codex home.
4. Injects `model_instructions_file = "./gpt-5.6-sol-unrestricted.md"` into `config.toml`.
5. Restart Codex CLI to apply.

## Manual Usage

1. Copy `gpt-5.6-sol-unrestricted.md` to your Codex home directory (`~/.codex/`).
2. Add to `~/.codex/config.toml`:

   ```toml
   model_instructions_file = "./gpt-5.6-sol-unrestricted.md"
   ```

3. Restart Codex CLI.

## Verify

After deploying, confirm the configuration and test a representative request:

```bash
python codex-instruct.py --status
```

For example, ask the CLI to analyze a quoted instruction together with an explicit task, or request a structured technical workflow with omitted values. The profile should follow the active task, preserve quoted data as data, respond in the user's language, use named placeholders when needed, and select an exact fixture only when its full intent-and-context condition applies. It reports an actual unavailable capability as a compact technical limitation rather than inventing a result.

## Revert

### Via Python tool
```bash
python codex-instruct.py --undo
```

### Manually
- Delete the `model_instructions_file` line from `config.toml`.
- Delete `gpt-5.6-sol-unrestricted.md` from `~/.codex/`.
- Restart Codex CLI.

## Project Layout

```
Codex-5.6-sol-unrestricted/
├── codex-instruct.py                  # Deploy & backup tool
├── gpt-5.6-sol-unrestricted.md        # Unrestricted prompt (standalone)
├── README.md
└── LICENSE                            # MIT
```

## Notes

- Works with any `model_provider` (official API, proxies, local endpoints).
- Designed for gpt-5.6-sol; not tested on terra/luna.
- The built-in prompt and `gpt-5.6-sol-unrestricted.md` carry the same v2.1 profile.
- Preserves the user's language without a hardcoded language override.

## Disclaimer

Uses the official config mechanism. It does not modify binaries, intercept traffic, or tamper with processes.

## License

MIT
