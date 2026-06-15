# Permission Protocol × OWASP Agentic Top 10 (2026)

*How Permission Protocol maps to the OWASP Top 10 for Agentic Applications, published December 2025 by the OWASP Gen AI Security Project (Agentic Security Initiative).*

Permission Protocol is the **human-approval and named-signer receipt layer** for autonomous agent actions. We do not claim 10/10 coverage. We cover the half of the OWASP Agentic Top 10 that requires a human decision and a durable record of that decision. The other half — deterministic policy enforcement, identity, sandboxing — pairs with engines like Microsoft AGT.

---

## Coverage at a glance

| Code | Risk | PP Coverage |
|------|------|-------------|
| ASI01 | Agent Goal Hijack | Partial — signed intent envelopes |
| ASI02 | Tool Misuse & Exploitation | **Direct** — per-action approval, signed receipts |
| ASI03 | Identity & Privilege Abuse | **Direct** — per-action authorization, HITL on escalation |
| ASI04 | Agentic Supply Chain Vulnerabilities | Partial — receipt provenance |
| ASI05 | Unexpected Code Execution (RCE) | **Direct** — human approval on elevated runs |
| ASI06 | Memory & Context Poisoning | Partial — human review hooks |
| ASI07 | Insecure Inter-Agent Communication | Pairs with AGT / identity layer |
| ASI08 | Cascading Failures | **Direct** — tamper-evident receipts, non-repudiation |
| ASI09 | Human-Agent Trust Exploitation | **Direct** — multi-step approval, immutable receipts |
| ASI10 | Rogue Agents | **Direct** — signed receipts, attestation gates |

**6 direct, 3 partial, 1 paired.** Direct controls are first-class PP product surface. Partial = PP contributes a piece. Paired = belongs to an upstream policy/identity layer.

---

## Detail mapping

### ASI01 — Agent Goal Hijack (Partial)

**OWASP mitigation:** "Require confirmation — via human approval, policy engine, or platform guardrails." Signed intent envelopes binding goals/constraints.

**PP control:** When an agent's planned action falls outside the signed intent envelope, PP routes to a named human signer. The signoff and the underlying intent are bound together in the receipt.

---

### ASI02 — Tool Misuse & Exploitation (Direct)

**OWASP mitigation:** "Action-Level Authentication and Approval." Human confirmation for destructive actions. Pre-execution dry-run/diff previews. Immutable logs of tool invocations.

**PP control:** Every wrapped tool call is gated. Destructive operations escalate to a named signer with diff preview. The receipt records the tool, the parameters, the signer, and the policy applied. Immutable by design.

---

### ASI03 — Identity & Privilege Abuse (Direct)

**OWASP mitigation:** "Mandate Per-Action Authorization." "Apply Human-in-the-Loop for Privilege Escalation." OAuth tokens bound to signed intent (subject, audience, purpose, session). Re-authentication on context switch.

**PP control:** Per-action authorization is the core PP primitive. Privilege escalations always route to a human signer. PP receipts include the signer identity, the authority chain, and the intent the action was bound to.

---

### ASI04 — Agentic Supply Chain Vulnerabilities (Partial)

**OWASP mitigation:** Signed/attested manifests, prompts, tool definitions. Continuous validation at runtime.

**PP control:** Receipts capture and link to the manifest hash and tool-definition version active at the moment of approval, providing provenance evidence at the action layer.

---

### ASI05 — Unexpected Code Execution / RCE (Direct)

**OWASP mitigation:** Human approval required for elevated runs. Allowlists under version control.

**PP control:** Elevated-permission code paths require a named human approval before execution. The receipt records the approver, the diff, and the policy that classified the action as elevated.

---

### ASI06 — Memory & Context Poisoning (Partial)

**OWASP mitigation:** Human review for high-risk actions. Rollback/quarantine support.

**PP control:** When an agent's memory or RAG context drives a high-risk action, PP gates the action for human review. Rollback signals can be tied to the receipt that authorized the original action.

---

### ASI07 — Insecure Inter-Agent Communication (Pairs)

**OWASP mitigation:** Signed agent cards, PKI-backed attestation, mTLS, continuous verification.

**PP coverage:** This belongs to the identity and protocol layer (Microsoft AGT, SPIFFE/SVID, similar). PP composes with those: a verified inter-agent message that triggers a consequential action still must clear PP before execution, and the receipt links to the verified identity of the originating agent.

---

### ASI08 — Cascading Failures (Direct)

**OWASP mitigation:** "Output validation and human gates." "Tamper-evident, time-stamped logs bound to cryptographic agent identities." Lineage metadata for forensic traceability and non-repudiation.

**PP control:** Human gates on cross-agent consequential actions. Receipts are tamper-evident, time-stamped to the millisecond, and bound to both the signing human and the originating agent. Lineage across the receipt chain provides forensic reconstruction. Non-repudiation by design.

---

### ASI09 — Human-Agent Trust Exploitation (Direct)

**OWASP mitigation:** "Explicit confirmations" and multi-step approval. Immutable, tamper-proof logs of queries and actions. Content provenance with digital signature validation.

**PP control:** Multi-step approval workflows where consequential actions require explicit confirmation, with hard policy gates that the agent cannot social-engineer past. Every approval is cryptographically signed and immutably recorded.

---

### ASI10 — Rogue Agents (Direct)

**OWASP mitigation:** Signed audit logs. Identity attestation. Signed behavioral manifests. Fresh attestation + human approval before reintegration.

**PP control:** Every PP receipt is a signed audit log. Behavioral manifests for each agent can be bound to PP policy, with re-approval required on attestation drift. A drifted agent cannot transact until a named human signs off — and the receipt records exactly that re-attestation event.

---

## Where AGT and PP fit together

Microsoft Agent Governance Toolkit (AGT) claims 10/10 OWASP Agentic Top 10 coverage as a deterministic policy engine. PP claims direct coverage of the controls that require **a named human signer and a durable, legally defensible receipt**. The two compose:

- **AGT** handles the high-volume, deterministic allow/deny decisions in software at sub-millisecond latency.
- **PP** handles the consequential decisions that require a named human signer, produces the receipt the regulator and the auditor actually need.

A mature agentic stack uses both. PP and AGT do not compete; they cover different halves of the same OWASP framework.

---

## What the auditor gets

The OWASP Agentic Top 10 is written for security teams and platform builders. The CCO, CFO, and external auditor speak a different language. PP's receipts translate OWASP-mapped controls into the artifact those audiences need:

- A named human signed this action.
- This policy applied.
- This data informed the decision.
- This is when it happened, to the millisecond.
- This is the immutable record.

Same controls. Auditor-readable output.

---

**Source:** OWASP Gen AI Security Project, Agentic Security Initiative. *OWASP Top 10 for Agentic Applications 2026*. Published December 2025. Project leads: John Sotiropoulos (Deep Cyber), Keren Katz (Tenable), Ron F. Del Rosario (SAP).
