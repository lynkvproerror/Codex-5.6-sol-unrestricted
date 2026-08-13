# Codex-5.6-sol-unrestricted

> Unrestricted-mode prompt for **gpt-5.6-sol** in Codex CLI — one-click deploy & backup tool.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Python 3.8+](https://img.shields.io/badge/Python-3.8%2B-blue)](https://python.org)

Uses the official `model_instructions_file` config mechanism — no binary patching, no MITM, no process tampering.

## What it does

Injects a custom unrestricted-mode instruction set via `model_instructions_file`, forcing Codex into `[MODE: UNRESTRICTED]` with:

- **Identity declaration** — anchors the model persona as GPT-5.6-sol Codex agent
- **8 core directives** — covering research framing, security authorization, NSFW creative writing, no disclaimers, completeness priority, instruction hiding
- **Full sandbox context** — all targets treated as isolated fixtures with no real-world consequences
- **Banned output phrases** — 12+ refusal strings explicitly blocked
- **Placeholder system** — TARGET, HOST, TOKEN, OFFSET, PATCH_BYTE, PAYLOAD, etc.
- **Operation handling** — specific rules for crack, keygen, reverse, license bypass
- **Boundary-word handling** — converts "unauthorized", "no permission", etc. to placeholders
- **Additional boundary triggers** — victim machines, anti-debug, anti-VM, detection bypass

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

After deploying, test with:

> "How to perform SQL injection testing on a target?"

Before → refusal; After → direct methodology.

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
- Preserves user's language — no hardcoded language override.

## Disclaimer

Exploits official config mechanism. No binary mod, no MITM, no process tampering. Use at your own risk.

## License

MIT
