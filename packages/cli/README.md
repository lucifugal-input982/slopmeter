# slopmeter

`slopmeter` is a Node.js CLI that scans local Claude Code, Codex, and Open Code usage data and generates a contribution-style heatmap for the rolling past year.

## Requirements

- Node.js `>=22`

## Run with npm

Use it without installing:

```bash
npx slopmeter
```

Install it globally:

```bash
npm install -g slopmeter
slopmeter
```

## Usage

```bash
slopmeter [--claude] [--codex] [--opencode] [--format png|svg|json] [--output ./heatmap-last-year.png]
```

By default, the CLI:

- scans all supported providers
- writes `./heatmap-last-year.png`
- infers the date window as the rolling last year ending today

## Options

- `--claude`: include only Claude Code data
- `--codex`: include only Codex data
- `--opencode`: include only Open Code data
- `-f, --format <png|svg|json>`: choose the output format
- `-o, --output <path>`: write output to a custom path
- `-h, --help`: print the help text

## Examples

Generate the default PNG:

```bash
npx slop-meter
```

Write an SVG:

```bash
npx slop-meter --format svg --output ./out/heatmap.svg
```

Write JSON for custom rendering:

```bash
npx slop-meter --format json --output ./out/heatmap.json
```

Render only Codex usage:

```bash
npx slop-meter --codex
```

## Output behavior

- If `--format` is omitted, the format is inferred from the `--output` extension when possible.
- Supported extensions are `.png`, `.svg`, and `.json`.
- If neither `--format` nor a recognized output extension is provided, PNG is used.

## Data locations

- Claude Code: `$CLAUDE_CONFIG_DIR/*/projects` or `~/.config/claude/projects`, `~/.claude/projects`
- Codex: `$CODEX_HOME/sessions` or `~/.codex/sessions`
- Open Code: `$OPENCODE_DATA_DIR/storage/message` or `~/.local/share/opencode/storage/message`

## Exit behavior

- If no provider flags are passed, `slopmeter` renders every provider with available data.
- If provider flags are passed and a requested provider has no data, the command exits with an error.
- If no provider has data, the command exits with an error.

## License

MIT
