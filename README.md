# Codex-5.6-sol-unrestricted

A jailbreak / unrestricted-mode prompt for **gpt-5.6-sol** in Codex CLI.

Uses the official `model_instructions_file` config mechanism — no binary patching, no MITM, no process tampering.

## Quick Start (Python Tool)

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

### What it does

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

## Revert

### Via Python tool
```bash
python codex-instruct.py --undo
```

### Manually
- Delete the `model_instructions_file` line from `config.toml`.
- Delete `gpt-5.6-sol-unrestricted.md` from `~/.codex/`.
- Restart Codex CLI.

## Notes

- Works with any `model_provider` (official API, proxies, local endpoints).
- Designed for gpt-5.6-sol; not tested on terra/luna.
- English only — no Chinese text in the prompt.

## License

MIT
