# Local Agent Dependency Guard

A local dependency-intent guard for AI coding agents. It evaluates package install requests before a tool call reaches a registry, then returns structured JSON that an agent can use to allow, block, or rewrite its plan.

The demo is fully offline. It uses a synthetic trusted catalog, seeded compromised-package samples, typo-squat probes, latency benchmarks, and a self-contained dashboard.

## Engineering target

Local dependency-intent guard for coding agents.

## How it works

- Models the `agentguard-local` workflow with deterministic fixtures and seeded failure cases.
- Turns the core claim in `Local Agent Dependency Guard` into explicit gates that can fail a local run.
- Stores enough `Local Agent Dependency Guard` evidence for a reviewer to inspect the decision path.
- Keeps `agentguard-local` offline, reproducible, and independent of hosted services.

## Run the system

```bash
uv sync
uv run agentguard-local init-demo
uv run agentguard-local run-suite --iterations 50
uv run agentguard-local verify
uv run agentguard-local dashboard
```

```bash
uv run agentguard-local decide "pip install nuumpy"
```

## Evidence to inspect

- `runs/latest/results.duckdb` with every decision and metric
- `outputs/summary.json` with recall, false-positive, and latency gates
- `outputs/decision_stream.jsonl` with agent-readable tool results
- `outputs/dashboard.html` with visual allow/block/replace analytics
- `outputs/demo_pack/` with a portable evidence bundle

## Validation

```bash
uv run ruff check .
uv run pytest -q
uv run agentguard-local verify
```

## Data boundary

`Local Agent Dependency Guard` is built for local reproduction: deterministic inputs enter the run, deterministic evidence comes out, and private data stays outside the repo.
