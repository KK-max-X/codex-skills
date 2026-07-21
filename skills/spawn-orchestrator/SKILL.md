---
name: spawn-orchestrator
description: Decompose complex multi-module tasks and execute them in parallel via spawn_agent. Use when the user wants to split work across sub-agents, run parallel implementations, or use a planner-executor pattern for large projects. Trigger on phrases like spawn mode, parallel agents, split and execute, brain and hands, or when a task naturally splits into independent workstreams.
---

# Spawn Orchestrator

Act as a planner (brain) that decomposes complex work and spawns sub-agents (hands) for parallel execution. Stay in the planner role: do not write implementation code yourself. Your job is to think, split, delegate, and integrate.

## Decision: Spawn or Do It Yourself

Spawn when:
- 3+ independent modules or features can be built in parallel
- Multiple data sources / APIs / platforms need independent handling
- Non-overlapping file sets (each sub-agent gets its own write scope)
- Tasks are self-contained with clear input/output contracts

Do NOT spawn for:
- Single-file changes or tightly coupled refactors
- Tasks with cascading dependencies (B depends on A output)
- Debugging that needs iterative trial-and-error
- The user explicitly asked for step-by-step sequential work

## Planning Phase

Before spawning, produce a quick plan visible to the user:

1. **Decomposition**: List sub-tasks with clear boundaries and file scopes
2. **Parallel groups**: Mark which tasks can run concurrently
3. **Sequential gates**: Note any ordering constraints
4. **Integration**: Describe how results will be assembled

Keep this phase brief. A few bullet points usually suffice.

## Spawning Rules

For each sub-task:
- Give a concrete, bounded prompt with explicit deliverables
- Declare the write scope (which files/dirs the sub-agent owns)
- Ensure write scopes never overlap across parallel spawns
- Let sub-agents edit files directly in their workspace; they list changed files on completion

Use multi_agent_v1__spawn_agent with fork_context: false unless the sub-agent needs full conversation history.

## Integration Phase

After sub-agents return:
1. Review each result quickly for correctness
2. If any sub-agent failed, decide: fix locally or re-spawn with adjusted instructions
3. Assemble / wire together results
4. Run integration-level verification (tests, build, etc.)

## Example

User: Build a CLI that scrapes Douyin, Xiaohongshu, and Kuaishou

Planner response:

Decomposition:
A. Douyin crawler (Playwright, src/douyin/)
B. Xiaohongshu crawler (Playwright, src/xhs/)
C. Kuaishou crawler (Playwright, src/ks/)
D. Shared data layer (models, storage, src/shared/)
E. CLI entry point (src/cli.py)

Order: A, B, C, D all parallel -- then E

Spawn all four in parallel:
- Agent A: Build Douyin crawler in src/douyin/ using Playwright...
- Agent B: Build Xiaohongshu crawler in src/xhs/...
- Agent C: Build Kuaishou crawler in src/ks/...
- Agent D: Build shared data layer in src/shared/...

After all return, spawn Agent E or wire the CLI together locally.

## Anti-Patterns

- Do not delegate the planning itself to a sub-agent
- Do not spawn agents that will conflict on the same files
- Do not wait for all agents before doing any local work
- Do not redo sub-agent work locally; review and integrate instead
