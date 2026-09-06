# Orchestrator

Context management through breadth-first planning and a small capable autonomous team.
This standalone package mirrors the orchestrator in [andres-skills](https://github.com/seeko-codes/andres-skills).

## Core model: batches as a basis

The horizontal slice is the complete goal H. Vertical slices are cohesive contributions
whose deliverables collectively cover it across all batches. Concurrent slices have disjoint
write ownership and no unresolved dependency on each other's unfinished outputs. Shared
reading is allowed. The basis analogy describes coverage and independent construction;
it is not a literal linear-algebra guarantee of behavioral correctness.

Plan breadth first: establish the whole target, shared constraints, and dependencies.
Resolve shared contracts before dependent work. Group ready independent slices into batches;
refine future batches after verified integration. Re-slice oversized work relative to its
own deliverable. Verify both individual outputs and their composition.

## Capability, context, and autonomy

The manager requests the smartest available model at maximum supported reasoning effort.
Subagents may match it or use less where sufficient. Prefer fewer capable autonomous owners
over a hierarchy of weak agents. The manager retains global responsibility and gives each
worker a locally complete contract: relevant sources, interfaces, constraints, acceptance,
and authority. Workers make local choices and escalate cross-slice decisions.

| User parameter | Default | Purpose |
|---|---|---|
| `max_context_per_agent` | `100000` tokens | Context ceiling for every agent |
| `context_warning_fraction` | `0.8` | Checkpoint before the ceiling |
| `wayfinder` | `false` | Continuity across goals and manager sessions |

The manager observes context occupancy; exceeding the ceiling means the assignment was too
large for its budget. Telemetry may be measured, estimated, or unavailable and must be labeled.
These instructions do not install monitoring or native handoff controls.

## Exploration before hardening

When arrangement is uncertain, map alternatives broadly and use focused prototypes to resolve
structural questions. Defer the full lean-quality workflow until the selected scope has coherent
responsibilities, exercised seams, and settled acceptance. Retained prototypes then enter
hardening: honest characterization tests, TDD for new behavior/fixes, integration checks, and
inspected screenshots plus interactions for UI. Prototype checkpoints are not production completion.
See [implementation stages](orchestrator/doctrine/stages.md).

## Optional Wayfinder

Wayfinder owns the larger sequence and automatic manager handoffs where the runtime supports
them. It is the sole nesting exception: Wayfinder → orchestrators → leaf workers. Ordinary
orchestrators cannot spawn managers, and workers cannot delegate. If runtime depth is insufficient,
retain Wayfinder duties in the main manager with one worker layer and explain the limitation.
The human owns highest-level direction and consequential uncertain decisions.

## Visible operation

Show the overall sequence, current batch, each assignment's purpose, model/effort, dependencies,
context/limit, and status. Explain actions and reasons at meaningful transitions and during long
work. Centralize worker updates so the human can follow the process without reading every chat.

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

Optional companions `model-strategy` and `lean-quality` are in
[andres-skills](https://github.com/seeko-codes/andres-skills). The standalone skill includes
fallback selection and verification guidance when they are absent. Native tools, permissions,
model availability, nesting, and context telemetry remain runtime constraints.

## License

MIT — see [LICENSE](LICENSE).
