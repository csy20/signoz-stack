# SigNoz Track 1 — AI Agent Observability + SRE Sidekick

Hackathon submission: **Track 1: AI & Agent Observability**.

## What we built

1. **router-agent** — hybrid token-efficient task router instrumented with OpenTelemetry → SigNoz (per-task escalation waterfall: free_solver → local_llm → fireworks).
2. **rem-cli `/observe`** — SRE sidekick that queries the **SigNoz MCP** server and answers with live span data.
3. **This repo** — Foundry `casting.yaml` + lock so judges can reproduce the SigNoz + MCP deployment.

## Repos

| Component | GitHub |
|-----------|--------|
| Foundry deploy (this repo) | https://github.com/csy20/signoz-stack |
| Instrumented agent | https://github.com/csy20/router-agent |
| SRE sidekick (rem-cli) | https://github.com/csy20/rem-cli |

## Foundry (required files)

```
casting.yaml
casting.yaml.lock
pours/deployment/   # generated compose stack
```

```bash
# Install Foundry: https://signoz.io/docs/install/docker/
foundryctl cast -f casting.yaml
# UI default :8080 — this stack maps UI to host :3301 if 8080 is busy (see pours/deployment/compose.yaml)
```

MCP is **enabled** in `casting.yaml` (`mcp.spec.enabled: true`) on port **8000**.

## Demo flow

```bash
# 1) SigNoz + MCP running (Foundry cast)

# 2) Run instrumented agent
cd router-agent
export OTEL_EXPORTER_OTLP_ENDPOINT=http://127.0.0.1:4317
export OTEL_SERVICE_NAME=router-agent
# + FIREWORKS_* env
python main.py   # or docker smoke_test.sh

# 3) SigNoz UI → Traces → service.name=router-agent

# 4) rem observe
export SIGNOZ_MCP_URL=http://localhost:8000/mcp
export SIGNOZ_API_KEY=<service-account-key>
rem observe "which tasks used fireworks and why"
```

## Project description (form paste)

See `SUBMISSION.md`.
