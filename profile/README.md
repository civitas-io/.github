# Civitas

**The production runtime for Python agents.**

Civitas brings Erlang's battle-tested fault-tolerance model to Python agent systems: supervision trees that restart crashed agents automatically, transport-agnostic message passing that scales from a single script to a distributed cluster, and first-class observability with zero instrumentation code.

---

## Repos

| Repo | What it is | Who it's for |
|---|---|---|
| [python-civitas](https://github.com/civitas-io/python-civitas) | The core runtime — `AgentProcess`, `Supervisor`, `MessageBus`, transports, OTEL tracing | Everyone building Python agents |
| [civitas-contrib](https://github.com/civitas-io/civitas-contrib) | Community extras — Fabrica (MCP tools gateway), framework adapters, provider plugins | Contributors and integration authors |
| [presidium](https://github.com/civitas-io/presidium) | Governed agent platform — policy engine, registry, audit, credential vault | Teams running agents in production with compliance requirements |

---

## Install

```bash
pip install civitas                       # core runtime
pip install civitas-contrib[fabrica]      # + MCP tools gateway
pip install presidium                     # + enterprise governance
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

New here? Start with the [Getting Started guide](https://civitas-io.github.io/python-civitas/getting-started/).
