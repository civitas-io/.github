# Civitas

**The production runtime for Python agents — and the toolchain around it.**

Civitas brings Erlang's battle-tested fault-tolerance model to Python agent systems: supervision trees that restart crashed agents automatically, transport-agnostic message passing that scales from a single script to a distributed cluster, and first-class observability with zero instrumentation code. Around that runtime, the org builds three real, live pillars that talk to each other over real REST+mTLS today: **Civitas** (runtime), **Presidium** (governance), and **Fabrica** (context layer) — plus a set of standalone, agent-native dev tools.

---

## Repos

| Repo | What it is | Who it's for | Latest release |
|---|---|---|---|
| [python-civitas](https://github.com/civitas-io/python-civitas) | The core runtime — `AgentProcess`, `Supervisor`, `MessageBus`, transports, HTTP/gRPC gateway, OTEL tracing | Everyone building Python agents | [`civitas` v0.11.3](https://github.com/civitas-io/python-civitas/releases/tag/v0.11.3) · 2026-08-23 |
| [presidium](https://github.com/civitas-io/presidium) | Governed agent platform, built natively on Civitas — policy engine, agent registry, trust scoring, credential vault, a real self-hostable REST+mTLS server (M7) | Teams running agents in production with compliance requirements | [`presidium` v0.3.0](https://github.com/civitas-io/presidium/releases/tag/v0.3.0) · 2026-08-24 · [`presidium-contrib` v0.6.0](https://github.com/civitas-io/presidium/releases/tag/contrib-v0.6.0) · 2026-08-24 |
| [fabrica](https://github.com/civitas-io/fabrica) | The context layer — tools-as-code, a tiered sandbox (subprocess → OS-isolated → Firecracker microVM), skills, memory, prompts. Governed by Presidium over real REST+mTLS | Anyone building agents that need to run untrusted, model-generated code safely | [`fabrica-context` v0.2.0](https://github.com/civitas-io/fabrica/releases/tag/v0.2.0) · 2026-08-24 |
| [prx](https://github.com/civitas-io/prx) (Praxis) | Agent-native Unix tools — single Rust binary replacing `grep`/`cat`/`find`/`sed`/`diff` with ranked, token-budgeted JSON and built-in semantic search | Anyone running AI coding agents that need to read less and act faster | [`prx` v0.6.4](https://github.com/civitas-io/prx/releases/tag/v0.6.4) · 2026-06-04 |
| [tessera](https://github.com/civitas-io/tessera) (`tsr`) | Agent-blind credential broker — agents *use* secrets via `tsr exec`/`http`/`proxy`, they never see the plaintext | Anyone letting an agent run commands that need real credentials | **Private repo — not yet public.** In active development. |
| [civitas-contrib](https://github.com/civitas-io/civitas-contrib) | Legacy/community extras repo — framework adapters, provider plugins, state stores. Its own former `fabrica` package is **superseded** by the real, standalone [fabrica](https://github.com/civitas-io/fabrica) repo above | Contributors and integration authors | No independent release — see individual package READMEs |
| [presidium-examples](https://github.com/civitas-io/presidium-examples) | Governed agent demos — HR assistant, support triage, SOC automation | Evaluators and new contributors | Reference examples, not versioned |
| [promptshrink](https://github.com/civitas-io/promptshrink) | Prompt compression — 30–50% token reduction, one-line integration, built on Civitas | Anyone paying LLM API bills | **Spec complete, implementation not yet started.** Not released. |

---

## Install

**Python packages, live on PyPI today:**

```bash
pip install civitas                       # core runtime
pip install presidium                     # governance: policy engine, registry, trust, credentials
pip install presidium-contrib             # governance: real network server (M7), OPA/OpenBao/Slack/Postgres adapters
pip install fabrica-context               # context layer -- import fabrica
pip install fabrica-context[presidium]    # + RestPresidiumClient (real REST+mTLS governance client)
```

**Standalone tools (Rust binaries — no Python dependency):**

```bash
# prx — agent-native replacement for grep/cat/find/sed/diff
brew install civitas-io/tap/prx           # or: cargo install prx
```

`tessera` is not yet public — its repo and releases are private while it's in active development.
`promptshrink` and `civitas-contrib`'s own `fabrica` package are not released; use
[fabrica-context](https://github.com/civitas-io/fabrica) for the real, current context layer.

---

## Philosophy

**Civitas is infrastructure, not a framework.** It does not define how agents reason, what prompts they use, or how they call LLMs. Those decisions live in your `handle()` method. Civitas handles the hard parts: process lifecycle, fault tolerance, message routing, and distributed tracing.

**Governance is architectural, not bolt-on.** Presidium builds on Civitas directly — policies are supervisor constraints, not external interceptors. The runtime and the governance layer share the same process model, registry, and observability pipeline, and now talk to each other over a real, self-hosted REST+mTLS server, not just in-process.

**The context layer is a separate concern from the runtime.** Fabrica decides what an agent sees (tools, skills, memory, prompts) and where its generated code actually runs (a tiered, pluggable sandbox) — governed by Presidium, run by Civitas, neither of which it reimplements.

**The runtime is boring on purpose.** Civitas follows the Erlang/OTP philosophy: a stable, conservative core that changes slowly and breaks nothing. Integrations and extras live in civitas-contrib where iteration is faster.

---

## Contributing

- **Runtime bugs and core features** → [python-civitas](https://github.com/civitas-io/python-civitas/blob/main/CONTRIBUTING.md)
- **Governance and enterprise features** → [presidium](https://github.com/civitas-io/presidium)
- **Context layer, sandboxing, tools/skills/memory** → [fabrica](https://github.com/civitas-io/fabrica)
- **Integrations, adapters, plugins** → [civitas-contrib](https://github.com/civitas-io/civitas-contrib)
- **Agent-native dev tooling** → [prx](https://github.com/civitas-io/prx)

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
2. https://raw.githubusercontent.com/civitas-io/presidium/main/README.md
3. https://raw.githubusercontent.com/civitas-io/presidium/main/docs/vision/roadmap.md
4. https://raw.githubusercontent.com/civitas-io/fabrica/main/README.md
5. https://raw.githubusercontent.com/civitas-io/fabrica/main/HANDOFF.md
6. https://raw.githubusercontent.com/civitas-io/presidium-examples/main/README.md
7. https://raw.githubusercontent.com/civitas-io/prx/main/README.md

Be specific and concrete. Treat this as a technical briefing, not a marketing summary.
```
