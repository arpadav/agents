# claude-agents (`aav-`)

Árpád's personal [Claude Code](https://code.claude.com/docs/en/sub-agents) subagents. Every agent is namespaced with an `aav-` prefix on both its filename and its frontmatter `name:`, so it is invoked as e.g. `aav-idiomatic-rust-types` and the whole set greps as `aav-*`.

These files are intended to be **symlinked into `~/.claude/agents/`** by home-manager (this repo is consumed as a git submodule of `~/.config/home-manager`). Editing happens here; `~/.claude/agents/aav-*.md` are symlinks back to these sources.

## Agents

### Idiomatic Rust review fleet
A monolithic reviewer split into focused single-lens agents so each is exhaustive within its lens instead of triaging and dropping findings.

| Agent | Lens |
|---|---|
| `aav-idiomatic-rust-reviewer` | **orchestrator** — fans out the four lenses in parallel, then merges/dedupes/ranks into one report. Trigger: "dispatch the idiomatic rust agents". |
| `aav-idiomatic-rust-types` | type-system & state modeling (`TYPE-*`) |
| `aav-idiomatic-rust-flow` | control flow, errors, conversions (`FLOW-*`) |
| `aav-idiomatic-rust-api` | abstraction surface & API patterns (`API-*`) |
| `aav-idiomatic-rust-organization` | layout & tooling hygiene (`ORG-*`) |
| `aav-rust-perf` | performance & optimization (`PERF-*`) — orthogonal, opt-in only |
| `aav-rust-security` | security & sensitive-data safety (`SEC-*`) — orthogonal, opt-in only |

`perf` and `security` are deliberately **not** part of the default idiomatic sweep — they are different axes from "idiomatic" and are dispatched only on explicit request.

### Other
| Agent | Purpose |
|---|---|
| `aav-arpad-style` | enforces Árpád's coding-style conventions (file-doc comments, import ordering, doc comments, inline attributes). |
| `aav-semantic-architecture-reviewer` | gates implementation plans for semantic correctness / DRY / placement before they reach the user. |
| `aav-slot-game-architect` | slot-machine math modelling (RTP, paytables, reel strips, volatility) and platform implementation. |

## Shared memory
The idiomatic-rust fleet shares a knowledge base at `~/.claude/agent-memory/idiomatic-rust/`, with per-lens note prefixes (`types-`, `flow-`, `api-`, `organization-`, `perf-`, `security-`).
