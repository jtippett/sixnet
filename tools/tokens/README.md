# Token usage tally

`tally.py` scans local Claude Code transcripts in `~/.claude/projects/*/*.jsonl`
and Codex transcripts under `~/.codex/sessions/`, deduplicates repeated usage
updates, and aggregates tokens by local calendar date. Output always identifies the
`claude` or `codex` source and can be split by project, model, or both.

Codex reports cached input as part of `input_tokens`; the tally separates that
subset into `cache-read` so `total` does not double-count it. Codex has no matching
cache-write field, so its value is zero.

```sh
# All available daily totals, aligned plain text
python3 tools/tokens/tally.py

# One day's per-model totals as a Markdown table
python3 tools/tokens/tally.py --day 2026-07-19 --by-model --md

# An inclusive range, broken down by project and model
./tools/tokens/tally.py --since 2026-07-01 --until 2026-07-19 \
  --by-project --by-model
```
