# Orchestrator

A skill for handling large goals with a small, capable team of agents. One manager keeps
the whole goal in view; each helper gets a focused job and the information needed to do it.
This package mirrors the orchestrator in [andres-skills](https://github.com/seeko-codes/andres-skills).

## How it works

First map the whole result, then narrow down the work. Give related decisions to one owner,
make the pieces easy to replace, and check that together they cover everything you asked for.
The technical instructions call the whole goal a **horizontal slice** and each contribution
a **vertical slice**. The mathematical analogy helps explain coverage and independence;
it does not prove the resulting software correct.

Ready, independent jobs can run together in a batch. A job that needs another's result waits
for a later batch. If helpers repeatedly need one another's unfinished decisions, reconsider
the split. The manager checks individual results and how they work together.

Each helper gets relevant requirements, files, constraints, and a way to check its result.
It makes local decisions independently and brings shared decisions back to the manager.
This gives specialization, useful parallel work, and less unrelated information in each chat.
Small tasks stay with one agent.

## Explore, then strengthen

When the arrangement is uncertain, try small experiments before investing in a full build.
Start with the uncertainty most likely to invalidate later work. Keep existing protections
and the checks needed to trust the experiment.

Once responsibilities, connections, and expected behavior make sense, strengthen the code
being kept. Check existing behavior; for new behavior and fixes, first demonstrate a failing
check, then make it pass, then clean up. This is test-driven development (TDD). For interfaces,
try actual interactions and inspect screenshots. A useful prototype is not yet production-ready.
See [implementation stages](orchestrator/doctrine/stages.md).

## Your choices

The manager uses the strongest available model and maximum supported reasoning effort.
Helpers may use the same capability or less, depending on the job. The manager recommends
helper effort with reasons and tradeoffs; you approve it before launch. Approval can cover
a batch or stated policy and persists within that scope. Uncovered changes return to you.
Unavailable settings are reported honestly.

| Option | Default | What it means |
|---|---|---|
| `max_context_per_agent` | `100000` tokens | Working-context ceiling for every agent. Tokens are units of model-processed text. |
| `context_warning_fraction` | `0.8` | Save progress and replan at 80% of the ceiling. |
| `wayfinder` | `false` | Add a coordinator for a longer sequence of manager sessions. |

Set options in your request or project instructions. Context includes instructions, inputs,
history, and space for the answer, not cumulative billed usage. Crossing the ceiling means
the job was too large for its budget: preserve progress and narrow the remaining work.
Usage is labeled measured, estimated, or unknown. The skill does not install monitoring.

Optional **Wayfinder** manages orchestrators, which manage helpers. Without it, there is one
manager and helpers cannot delegate. Automatic handoffs and extra management depth depend on
the running application's capabilities. The human owns the highest-level direction and
consequential uncertain choices. When purpose, scope, or priorities are unclear, use the
optional `grill-with-docs` companion to examine one decision at a time. The agent investigates
and recommends; the human decides. `wait-what` remains an optional way to request a clearer
explanation.

## Follow the work

Expect one readable view of the goal, current batch, each agent's job and purpose, model,
effort, context usage, dependencies, and progress. Updates explain what is happening and why,
including blockers, changed decisions, checks, and handoffs.

Agent instructions and technical records retain standard method names. Human explanations
describe the underlying action and purpose without requiring you to know the vocabulary.
The [reference shelf](orchestrator/REFERENCES.md) links to original design methods and relevant
guidance. It is consulted for a specific unresolved question, not loaded automatically.
Authoritative references improve grounding; they do not guarantee correct reasoning.

## Install

```bash
git clone https://github.com/seeko-codes/orchestrator-skill.git
mkdir -p ~/.claude/skills
cp -R orchestrator-skill/orchestrator ~/.claude/skills/
```

Back up an existing same-named skill before copying. For other runners use their supported skill
directory. Start at [orchestrator/SKILL.md](orchestrator/SKILL.md). Supporting files are conditional:
[briefs](orchestrator/BRIEFS.md), [context](orchestrator/CONTEXT.md),
[Wayfinder](orchestrator/WAYFINDER.md), [visibility](orchestrator/VISIBILITY.md),
and [runtime adapters](orchestrator/SUBAGENTS.md).

Optional companions `model-strategy`, `lean-quality`, `grill-with-docs`, and `wait-what` are in
[andres-skills](https://github.com/seeko-codes/andres-skills). The standalone skill includes
fallback selection and verification guidance when they are absent. Native tools, permissions,
model availability, nesting, and context telemetry remain runtime constraints.

## License

MIT — see [LICENSE](LICENSE).
