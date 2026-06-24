# Awesome AI Agent Governance [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

> A curated list of frameworks, tools, standards, and research for governing and authorizing autonomous AI agents.

As AI agents move from chat to *action* — opening pull requests, sending money, calling APIs, deploying code — the question stops being "what can the model say?" and becomes "what is the agent *allowed to do*, who said so, and can you prove it?" This list collects the projects, standards, and writing that try to answer that.

This list is vendor-neutral. Entries are included on technical merit, and maintainers' own projects are labeled as such.

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

## Standards & Frameworks

- [OWASP Top 10 for Agentic Applications](https://genai.owasp.org/) - The OWASP Gen AI Security Project's threat taxonomy for agentic systems (ASI01–ASI10), published December 2025. The reference framework for agent-specific risk.
- [NIST AI Risk Management Framework](https://www.nist.gov/itl/ai-risk-management-framework) - Voluntary framework whose Govern/Map/Measure/Manage functions apply directly to agent oversight.
- [EU AI Act](https://artificialintelligenceact.eu/) - Article 14 ("human oversight") is the regulatory backbone for human-in-the-loop requirements on high-risk AI.
- [MITRE ATLAS](https://atlas.mitre.org/) - Adversarial threat landscape for AI systems; useful for threat-modeling agent attack paths.

## Policy & Authorization Engines

Deterministic "can this action happen?" decision engines — the allow/deny half of governance.

- [Open Policy Agent (OPA)](https://www.openpolicyagent.org/) - CNCF policy engine using Rego policies for fine-grained authorization, increasingly applied to agent tool calls.
- [Cedar](https://www.cedarpolicy.com/) - AWS's open-source authorization policy language and engine.
- [Permit.io](https://www.permit.io/) - Authorization-as-a-service with published patterns for gating AI agent actions.
- [Oso](https://www.osohq.com/) - Authorization framework and library for application-level access control.

## Human-in-the-Loop & Approval Layers

The "who approved this, and prove it" half — escalating consequential actions to a named human.

- [Permission Protocol](https://permissionprotocol.com) - Enforcement layer that routes consequential agent actions to a named human signer and produces an immutable receipt per action, including a GitHub Action that gates AI-generated pull requests and an MCP proxy that enforces policy on tool calls. *(maintainer project)*
- [HumanLayer](https://www.humanlayer.dev/) - API and SDK to add human approval and human-as-a-tool steps to AI agents.
- [LangGraph human-in-the-loop](https://langchain-ai.github.io/langgraph/concepts/human_in_the_loop/) - Interrupt and approve primitives for pausing an agent graph for human review.

## Identity & Attestation

- [SPIFFE / SPIRE](https://spiffe.io/) - CNCF standard and runtime for issuing cryptographic workload identity; foundation for attesting which agent is acting.
- [in-toto](https://in-toto.io/) - Framework for cryptographically verifying software supply-chain integrity; provenance patterns transferable to agent action chains.

## Audit Trails, Receipts & Provenance
- [Nobulex](https://github.com/arian-gogani/nobulex) — Ed25519-signed, JCS-canonical (RFC 8785) bilateral receipts for AI agent actions. Pre-execution admission + post-execution outcome, hash-chained, independently verifiable. `action_ref = SHA-256(JCS({agent_id, action_type, scope, timestamp_ms}))`. EU AI Act Article 12 compliance. MIT licensed.

- [OpenTelemetry GenAI semantic conventions](https://opentelemetry.io/docs/specs/semconv/gen-ai/) - Emerging standard for instrumenting LLM and agent traces; the observability layer beneath audit.
- [Sigstore](https://www.sigstore.dev/) - Keyless signing and transparency logs; the signing primitives under tamper-evident action records.

## MCP & Tool-Call Security

- [Model Context Protocol](https://modelcontextprotocol.io/) - The protocol spec connecting agents to tools and data; its security guidance is essential reading for tool-call risk.

## Sandboxing & Isolation

- [gVisor](https://gvisor.dev/) - Application kernel for sandboxing untrusted code; relevant for isolating agent code execution.
- [Firecracker](https://firecracker-microvm.github.io/) - MicroVMs for fast, isolated execution environments.
- [E2B](https://e2b.dev/) - Cloud sandboxes purpose-built for running AI-generated code.

## Research & Papers

- [A Survey on Trustworthy LLM Agents: Threats and Countermeasures](https://arxiv.org/abs/2503.09648) - Comprehensive survey mapping the threat surface of LLM agents and the defenses proposed against them.
- [Constitutional AI](https://arxiv.org/abs/2212.08073) - Anthropic's approach to value-aligned model behavior; complementary to external enforcement.

## Articles & Guides

- [Permission Protocol × OWASP Agentic Top 10 mapping](https://permissionprotocol.com/compliance/owasp) - Honest control-by-control mapping (6 direct, 3 partial, 1 paired) of the human-approval and named-signer half of the OWASP framework.

## Contributing

Contributions are welcome. Keep entries factual and one line, place them in the most specific category, and label your own projects. See [the contributing guide](CONTRIBUTING.md) for details.
