# Agent Starter Repo

An empty project preloaded with a complete, harness-agnostic operating system for
coding agents: one source-of-truth instruction set, entry adapters for every major
agent harness, task command-prompts, and a blank workplan template.

Fork it, drop in your project, and point your coding agent at it. From the first turn
the agent works to a strict, test-first, dependency-ordered discipline — the same rules
whether it runs in Claude Code, Codex, Copilot, or Cursor.

## What it's for

Coding agents are strong at instantiating a well-specified shape and weak at inventing
structure on the fly. This repo leans into that split:

- **The author decides.** A high-reasoning model turns a goal into a workplan that
  resolves every ambiguity into named files, types, and dependencies.
- **The implementer instantiates.** The implementing model — any model, including a
  hidden "Auto" one — follows a fixed procedure and builds proven shapes, rather than
  reasoning its way into novel, non-compliant code.

The rules are written **once** in `docs/agents/` and referenced from two views: the
workplan (what the author produces) and the command-prompts (what the implementer runs).
Nothing is duplicated, so nothing drifts.

## What's in it

```
docs/agents/                         the instruction spine — the single source of truth
  index.md                           topic index + the implementation routing matrix
  precedence, loop, discovery-halt,  Process topics: how an agent works any turn
    modes, traceability, output,
    environment, linting-proof,
    logging, fidelity
  types, composition,                Standards topics: how to build each kind of file
    dependency-injection, mocks,
    guards, tests, errors-and-returns,
    boundaries, tdd-ordering,
    workplan-structure

docs/workplans/current/
  empty-workplan.md                  blank workplan template (copy it to start)

.cursor/commands/*.prompt.md         task command-prompts — thin pointers into the spine

CLAUDE.md                            harness adapters — each one just points the agent
AGENTS.md                              at docs/agents/index.md, so every harness reads
.github/copilot-instructions.md        the same rules
.cursor/rules/rules.mdc
```

## Supported harnesses

| Harness | Auto-loaded entry file |
|---|---|
| Claude Code | `CLAUDE.md` |
| Codex / OpenAI agents | `AGENTS.md` |
| GitHub Copilot | `.github/copilot-instructions.md` |
| Cursor | `.cursor/rules/rules.mdc` (+ `.cursor/commands/` for slash commands) |

Each adapter is a three-line pointer to `docs/agents/index.md`. Any other agent that can
read a project file works too — point it at the index.

## How to use it

1. **Fork or clone** this repo and add your project into it (or start fresh here).
2. **Open it in your agent.** It auto-loads its harness adapter, which sends it to
   `docs/agents/index.md` — the topic index and the routing matrix that maps each file
   you build to the rules that govern it.
3. **Author a workplan.** Copy `docs/workplans/current/empty-workplan.md`, then use the
   `plan` or `generateNode` command-prompt. A workplan is a dependency-ordered list of
   nodes; each node is the full TDD cycle for exactly one source file.
4. **Implement node by node**, one file per turn, using the command-prompts in the fixed
   order: `interfaceTest → interface → mock → guardTest → guard → unitTest → implement →
   provide → integrate`.
5. **Diagnose and maintain** with `check` (review a finished node), `linterComplaint`,
   `testFailure`, and `useMock` (migrate hand-rolled test objects to builders).

## The discipline, in brief

- **Test-first, always.** The RED test is written before the code it covers; a failing
  compile is the proof, never something to silence.
- **One source file per node, one file per turn.** Multi-file work is a discovery — the
  agent stops and reports instead of sprawling.
- **Dependency order is immutable.** Producers before consumers; the sequence is never
  reordered or merged.
- **Read before you reason.** The agent reads the relevant rules and the existing files
  before proposing anything, so effort isn't spent on solutions that violate a rule it
  never read.
- **Resolve, don't invent.** The author names paths, symbols, and owners; the
  implementer instantiates them; when neither the node nor a deterministic search
  resolves something, the agent halts and reports rather than guessing.

Start at [docs/agents/index.md](docs/agents/index.md).
