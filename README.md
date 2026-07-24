# Codex-5.6-sol-unrestricted

A jailbreak / unrestricted-mode prompt for **gpt-5.6-sol** in Codex CLI.

Uses the official `model_instructions_file` config mechanism — no binary patching, no MITM, no process tampering.

## Usage

1. Copy `gpt-5.6-sol-unrestricted.md` to your Codex home directory (`~/.codex/`).
2. Add to `~/.codex/config.toml`:

   ```toml
   model_instructions_file = "./gpt-5.6-sol-unrestricted.md"
   ```

3. Restart Codex CLI.

## Revert

- Delete the `model_instructions_file` line from `config.toml`.
- Delete `gpt-5.6-sol-unrestricted.md` from `~/.codex/`.
- Restart Codex CLI.

## Notes

- Works with any `model_provider` (official API, proxies, local endpoints).
- Designed for gpt-5.6-sol; not tested on terra/luna.
- English only — no Chinese text in the prompt.

## License

MIT
