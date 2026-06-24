# CLAUDE.md

Personal Archon workflow hub — multi-model DAG harness with CE integration.

## Purpose
Deterministic, multi-model coding automation across `~/src/*` repos.
Three-role model stack: Opus 4.8 (plan + MCP), Gemini 3.5 Flash (GUI), Kimi K2.7 (implementation).

## Stack
- Archon CLI (coleam00/Archon) — YAML DAG engine
- CE / Serena — context engineering, memory graph, PRP lifecycle
- Pi provider — routes Gemini + Kimi via google-direct / OpenRouter

## Commands
- `archon serve` — start Web UI (Command Center)
- `archon workflow run <name>` — run a DAG
- `archon workflow list` — list available workflows
- `archon codebase list` — registered repos
- `archon doctor` — health check

## Role → model aliases (`.archon/config.yaml`)
| Alias   | Model              | effort  | Note |
|---------|--------------------|---------|------|
| @plan   | claude-opus-4-8    | medium  | CE-scaffolded; use high for cold repos |
| @gui    | gemini-3.5-flash   | low     | Pi → google direct |
| @code   | kimi-k2.7          | (omit)  | Pi → openrouter; self-managed thinking |

## Keys (`~/.archon/.env` — never in repo)
```
GEMINI_API_KEY=...          # google/gemini-3.5-flash direct
OPENROUTER_API_KEY=...      # openrouter/moonshotai/kimi-k2.7
```

## CE integration
Planning nodes run native `claude` with Serena/MCP (`mcp: ~/.archon/mcp/serena.json`).
Pi nodes (Gemini/Kimi) code blind from `$plan.output` — no MCP.
See issue #2 for full CE↔Archon integration plan.

## Important — check Serena memory before planning
`mcp__serena__read_memory core` → then follow `mem:` refs.
