# Awesome AI Agent Governance [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

> A curated list of frameworks, tools, standards, and research for **governing and authorizing autonomous AI agents** — controlling what an agent is allowed to do, who approves consequential actions, and how those decisions are recorded.

As AI agents move from chat to *action* — opening pull requests, sending money, calling APIs, deploying code — the open question stops being "what can the model say?" and becomes "what is the agent *allowed to do*, who said so, and can you prove it?" This list collects the projects, standards, and writing that try to answer that.

Contributions welcome — see [Contributing](#contributing). This list is vendor-neutral; entries are included on technical merit, and maintainers' own projects are labeled as such.

## Contents

- [Standards & Frameworks](#standards--frameworks)
- [Policy & Authorization Engines](#policy--authorization-engines)
- [Human-in-the-Loop & Approval Layers](#human-in-the-loop--approval-layers)
- [Identity & Attestation](#identity--attestation)
- [Audit Trails, Receipts & Provenance](#audit-trails-receipts--provenance)
- [MCP & Tool-Call Security](#mcp--tool-call-security)
- [Sandboxing & Isolation](#sandboxing--isolation)
- [Research & Papers](#research--papers)
- [Articles & Guides](#articles--guides)
- [Contributing](#contributing)

## Standards & Frameworks

- [OWASP Top 10 for Agentic Applications (2026)](https://genai.owasp.org/) — The OWASP Gen AI Security Project's threat taxonomy for agentic systems (ASI01–ASI10), published December 2025. The reference framework for agent-specific risk.
- [NIST AI Risk Management Framework](https://www.nist.gov/itl/ai-risk-management-framework) — Voluntary framework for managing risks of AI systems; the Govern/Map/Measure/Manage functions apply directly to agent oversight.
- [EU AI Act](https://artificialintelligenceact.eu/) — Article 14 ("human oversight") is the regulatory backbone for human-in-the-loop requirements on high-risk AI.
- [MITRE ATLAS](https://atlas.mitre.org/) — Adversarial threat landscape for AI systems; useful for threat-modeling agent attack paths.

## Policy & Authorization Engines

Deterministic "can this action happen?" decision engines — the allow/deny half of governance.

- [Open Policy Agent (OPA)](https://www.openpolicyagent.org/) — CNCF policy engine; Rego policies for fine-grained authorization, increasingly applied to agent tool calls.
- [Cedar](https://www.cedarpolicy.com/) — AWS's open-source authorization policy language and engine.
- [Permit.io](https://www.permit.io/) — Authorization-as-a-service; has published patterns for gating AI agent actions.
- [Oso](https://www.osohq.com/) — Authorization framework/library for application-level access control.
- Microsoft Agent governance tooling — Microsoft's deterministic policy approach to agent action governance (track via [Microsoft Security](https://www.microsoft.com/security)).

## Human-in-the-Loop & Approval Layers

The "who approved this, and prove it" half — escalating consequential actions to a named human.

- [Permission Protocol](https://permissionprotocol.com) *(maintainer project)* — Enforcement layer that routes consequential agent actions to a named human signer and produces an immutable, tamper-evident receipt per action. Includes a [GitHub Action deploy gate](https://github.com/marketplace/actions) for gating AI-generated PRs. See the [OWASP Agentic Top 10 mapping](resources/owasp-agentic-top-10-mapping.md).
- [HumanLayer](https://www.humanlayer.dev/) — API/SDK to add human approval and human-as-a-tool steps to AI agents.
- [LangGraph human-in-the-loop](https://langchain-ai.github.io/langgraph/concepts/human_in_the_loop/) — Interrupt/approve primitives for pausing an agent graph for human review.
- [LangChain HITL patterns](https://python.langchain.com/docs/) — Documentation patterns for inserting human approval into agent/tool execution.

## Identity & Attestation

- [SPIFFE / SPIRE](https://spiffe.io/) — CNCF standard and runtime for issuing cryptographic workload identity; foundation for attesting *which* agent is acting.
- [Agent identity & inter-agent trust](https://genai.owasp.org/) — see OWASP ASI07 (Insecure Inter-Agent Communication) for the threat model these address.

## Audit Trails, Receipts & Provenance

- [Permission Protocol receipts](https://permissionprotocol.com) *(maintainer project)* — Per-action immutable receipts (signer, policy, intent, timestamp) designed to be auditor-readable and map to SR 11-7 / EU AI Act Article 14 evidence needs.
- [OpenTelemetry GenAI semantic conventions](https://opentelemetry.io/docs/specs/semconv/gen-ai/) — Emerging standard for instrumenting LLM/agent traces; the observability layer beneath audit.
- [in-toto](https://in-toto.io/) — Framework for cryptographically verifying the integrity of a software supply chain; provenance patterns transferable to agent action chains.

## MCP & Tool-Call Security

- [Model Context Protocol (MCP)](https://modelcontextprotocol.io/) — The protocol spec itself; the [security section](https://modelcontextprotocol.io/docs/concepts/transports) is essential reading.
- [Permission Protocol MCP Guard](https://permissionprotocol.com) *(maintainer project)* — Stdio proxy that enforces policy on MCP tool invocations before they execute.

## Sandboxing & Isolation

- [gVisor](https://gvisor.dev/) — Application kernel for sandboxing untrusted code; relevant for isolating agent code execution.
- [Firecracker](https://firecracker-microvm.github.io/) — MicroVMs for fast, isolated execution environments.
- [E2B](https://e2b.dev/) — Cloud sandboxes purpose-built for running AI-generated code.

## Research & Papers

- [Toward Trustworthy AI Agents (survey literature)](https://arxiv.org/) — search arXiv for recent surveys on agent safety, oversight, and authorization (cs.AI / cs.CR).
- [Constitutional AI](https://www.anthropic.com/research) — Anthropic's approach to value-aligned model behavior; complementary to external enforcement.

> Have a paper that belongs here? Open a PR with a one-line summary of its governance relevance.

## Articles & Guides

- [Permission Protocol × OWASP Agentic Top 10 mapping](resources/owasp-agentic-top-10-mapping.md) — Honest control-by-control mapping (6 direct / 3 partial / 1 paired) of the human-approval and named-signer half of the OWASP framework.
- [Governance vs. self-policing](https://permissionprotocol.com) — Why agent oversight must be external to the agent.

> Add your guide via PR. We favor specific, technical writing over thought-leadership.

## Contributing

PRs welcome. Please:
1. Keep entries factual and one line — what it is, why it's relevant to agent governance.
2. Place entries in the most specific category.
3. Label your own project with *(maintainer project)* or note your affiliation in the PR.
4. No marketing copy. If an entry reads like an ad, it'll be edited or declined.

See [CONTRIBUTING.md](CONTRIBUTING.md) for details.

## License

[![CC0](https://licensebuttons.net/p/zero/1.0/88x31.png)](LICENSE)

To the extent possible under law, contributors have waived all copyright and related rights to this work.
