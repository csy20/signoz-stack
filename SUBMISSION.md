# Submission form answers

## Track
**Track 1: AI & Agent Observability**

## Project description (copy/paste)

Token-efficient AI router agent with full OpenTelemetry observability in SigNoz, plus a terminal SRE sidekick.

**router-agent** classifies tasks (regex) and escalates free solvers → local Ollama self-consistency → at most one Fireworks call. We instrument the whole path with OTel spans (`task.process`, `task.classify`, `task.route` stages free_solver/local_llm/fireworks, `llm.local_generate`, `llm.fireworks_call` including skip events for the ≤1-call rule). Traces export OTLP gRPC to SigNoz so each task shows a waterfall of the escalation path — the hackathon’s token-efficiency story is visible live.

**rem-cli `/observe`** (SRE Sidekick) talks to the self-hosted **SigNoz MCP** server (Foundry `mcp.enabled`), pulls real span JSON for `service.name=router-agent`, and feeds it into the active LLM so answers cite stage/token attributes instead of guessing.

**Deploy:** Foundry `casting.yaml` + `casting.yaml.lock` in this repo (SigNoz + MCP). Agent: https://github.com/csy20/router-agent · Sidekick: https://github.com/csy20/rem-cli

## GitHub link to project
https://github.com/csy20/signoz-stack
(primary — includes casting.yaml + casting.yaml.lock)

Also reference in description:
- https://github.com/csy20/router-agent
- https://github.com/csy20/rem-cli

## Deployed link
http://YOUR_HOST:3301   # SigNoz UI (our env used 3301 because host 8080 was occupied)
# or default Foundry http://YOUR_HOST:8080

## Demo Video
https://drive.google.com/file/d/1U3ODt5gB48p6jgsJP-F2hQlD9ze3X9dy/view?usp=sharing

