# Civitas

**The production runtime for Python agents — and the toolchain around it.**

Civitas brings Erlang's battle-tested fault-tolerance model to Python agent systems: supervision trees that restart crashed agents automatically, transport-agnostic message passing that scales from a single script to a distributed cluster, and first-class observability with zero instrumentation code. Around that runtime, the org also builds the tools an AI agent (or the human running one) needs day to day — governed execution, context-efficient code search, and credential handling that never puts a secret in front of the model.

---

## Repos

| Repo | What it is | Who it's for |
|---|---|---|
| [python-civitas](https://github.com/civitas-io/python-civitas) | The core runtime — `AgentProcess`, `Supervisor`, `MessageBus`, transports, OTEL tracing | Everyone building Python agents |
| [civitas-contrib](https://github.com/civitas-io/civitas-contrib) | Community extras — Fabrica (MCP tools gateway), framework adapters, provider plugins | Contributors and integration authors |
| [presidium](https://github.com/civitas-io/presidium) | Governed agent platform — policy engine, registry, audit, credential vault | Teams running agents in production with compliance requirements |
| [prx](https://github.com/civitas-io/prx) (Praxis) | Agent-native Unix tools — single Rust binary replacing `grep`/`cat`/`find`/`sed`/`diff` with ranked, token-budgeted JSON and built-in semantic search | Anyone running AI coding agents that need to read less and act faster |
| [tessera](https://github.com/civitas-io/tessera) (`tsr`) | Agent-blind credential broker — agents *use* secrets via `tsr exec`/`http`/`proxy`, they never see the plaintext (alpha) | Anyone letting an agent run commands that need real credentials |
| [promptshrink](https://github.com/civitas-io/promptshrink) | Prompt compression — 30–50% token reduction, one-line integration, built on Civitas | Anyone paying LLM API bills |
| [presidium-examples](https://github.com/civitas-io/presidium-examples) | Governed agent demos — HR assistant, support triage, SOC automation | Evaluators and new contributors |

---

## Install

**Python packages:**

```bash
pip install civitas                       # core runtime
pip install civitas-contrib[fabrica]      # + MCP tools gateway
pip install presidium                     # + enterprise governance
pip install promptshrink                  # + prompt compression (30–50% cost reduction)
```

**Standalone tools (Rust binaries — no Python dependency):**

```bash
# prx — agent-native replacement for grep/cat/find/sed/diff
brew install civitas-io/tap/prx           # or: cargo install prx

# tessera — agent-blind credential broker
gh release download --repo civitas-io/tessera --pattern 'tsr-aarch64-apple-darwin.tar.gz'
tar -xzf tsr-*.tar.gz && sudo mv tsr /usr/local/bin/
```

---

## Philosophy

**Civitas is infrastructure, not a framework.** It does not define how agents reason, what prompts they use, or how they call LLMs. Those decisions live in your `handle()` method. Civitas handles the hard parts: process lifecycle, fault tolerance, message routing, and distributed tracing.

**Governance is architectural, not bolt-on.** Presidium builds on Civitas directly — policies are supervisor constraints, not external interceptors. The runtime and the governance layer share the same process model, registry, and observability pipeline.

**The runtime is boring on purpose.** Civitas follows the Erlang/OTP philosophy: a stable, conservative core that changes slowly and breaks nothing. Integrations and extras live in civitas-contrib where iteration is faster.

---

## Contributing

- **Runtime bugs and core features** → [python-civitas](https://github.com/civitas-io/python-civitas/blob/main/CONTRIBUTING.md)
- **Integrations, adapters, plugins** → [civitas-contrib](https://github.com/civitas-io/civitas-contrib)
- **Governance and enterprise features** → [presidium](https://github.com/civitas-io/presidium)
- **Agent-native dev tooling** → [prx](https://github.com/civitas-io/prx)
- **Credential brokering for agents** → [tessera](https://github.com/civitas-io/tessera)

---

## New Here? Get a Full Briefing in 60 Seconds

**Using Claude Code:** Open this link and Claude will read the repos and brief you on everything —
vision, architecture, current state, and where to start contributing.

> **[Open Onboarding Guide in Claude Code](https://claude.ai/claude-code/onboard/n5GkhCyQNmM6)**

**Using any other LLM (ChatGPT, Gemini, etc.):** Copy and paste the prompt below:

```
You are helping me onboard to the civitas-io open source project.
Please read the following files and give me an executive briefing covering:
what we're building, why it matters, how the pieces fit together, the current
state of each repo, and where I should start contributing.

Read these in order:
1. https://raw.githubusercontent.com/civitas-io/python-civitas/main/AGENTS.md
2. https://raw.githubusercontent.com/civitas-io/presidium/main/docs/vision/prd.md
3. https://raw.githubusercontent.com/civitas-io/presidium/main/docs/architecture/overview.md
4. https://raw.githubusercontent.com/civitas-io/presidium/main/docs/design/agent-registry.md
5. https://raw.githubusercontent.com/civitas-io/presidium/main/docs/design/policy-engine.md
6. https://raw.githubusercontent.com/civitas-io/presidium-examples/main/README.md
7. https://raw.githubusercontent.com/civitas-io/prx/main/README.md
8. https://raw.githubusercontent.com/civitas-io/tessera/main/README.md

Be specific and concrete. Treat this as a technical briefing, not a marketing summary.
```
