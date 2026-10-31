# Architecture

Proposed allocation of responsibilities. Revalidate provider capabilities and maturity before implementation.

User channels → main interaction agent → scoped specialist jobs → independent verification → policy-controlled release/report.

Persist trusted state; discard untrusted execution environments. Cloudflare Computer provides workspace capabilities, the harness provides the agent loop, and a Linux sandbox provides isolated execution.

## Workers + Durable Objects

Layer: Trusted runtime

Design status: Candidate

Main-agent identity, durable state, request routing, scheduling, and coordination.

Caveat: Do not equate durable availability with a continuously running process.

[Source](https://developers.cloudflare.com/agents/)

## Agents SDK + Pi Durable

Layer: Agent loop

Design status: Evaluate

Evaluate as the main-agent harness. Keep the CLI coding worker a distinct integration.

Caveat: Pi Durable is experimental; pin compatible package versions and test recovery.

[Source](https://developers.cloudflare.com/agents/harnesses/pi/)

## Cloudflare Computer

Layer: Durable workspace

Design status: Candidate

Plans, notes, small working files, task briefs, and filesystem tools for the coordinator.

Caveat: Core and JavaScript backend are stable in current repository docs; ContainerBackend and sync remain experimental.

[Source](https://github.com/cloudflare/computer/blob/main/packages/computer/README.md)

## Container-backed Sandboxes

Layer: Untrusted execution

Design status: Candidate

Fresh Linux environment per coding or verification job; native checkout and temporary dependencies.

Caveat: MicroVM boundary; everything inside a sandbox shares its trust zone. Check beta limits and task compatibility.

[Source](https://developers.cloudflare.com/sandbox/)

## Browser Run

Layer: Browser automation

Design status: Candidate

Task-scoped Chrome, screenshots, user-journey tests, optional live inspection.

Caveat: Separate environment; route app access deliberately. Fresh sessions and synthetic accounts.

[Source](https://developers.cloudflare.com/agents/tools/browser/)

## Workflows

Layer: Deterministic process

Design status: Candidate

Durable execution → verification → release sequence with bounded retries and waits.

Caveat: Use idempotency keys for side effects; model output must not rewrite policy.

[Source](https://developers.cloudflare.com/workflows/)

## AI Gateway / model APIs

Layer: Model access

Design status: Evaluate

Route provider requests and isolate credentials in trusted services.

Caveat: Choose provider data policies, retention, spend limits, and logging settings explicitly.

[Source](https://developers.cloudflare.com/ai-gateway/)

## R2 + metadata database

Layer: Artifacts & catalog

Design status: Evaluate

Patches, screenshots, recordings, documents, and indexable metadata with retention rules.

Caveat: R2 is object storage, not by itself an access policy, backup plan, or searchable personal memory.

[Source](https://developers.cloudflare.com/r2/)

## AI Search / Vectorize

Layer: Optional retrieval

Design status: Later

Add when a growing wiki or artifact catalog requires semantic search.

Caveat: Begin with explicit records and provenance; retrieval is not an authorization boundary.

[Source](https://developers.cloudflare.com/ai-search/)

## Access + scoped secrets + outbound handlers

Layer: Security

Design status: Required

Authenticate devices and services; keep credentials outside untrusted jobs.

Caveat: Every broker checks user, task, resource, operation, and expiry.

[Source](https://developers.cloudflare.com/sandbox/concepts/security/)

## Queues

Layer: Optional dispatch

Design status: Later

Buffer asynchronous work and control dispatch as scale grows.

Caveat: Consumers must tolerate duplicate delivery and enforce concurrency limits.

[Source](https://developers.cloudflare.com/queues/)

## Web / mobile / app integrations

Layer: User surface

Design status: Open

One interaction identity across clients; T3 optional for coding-oriented supervision.

Caveat: Client continuity, notifications, offline capture, and app permissions require product design.

[Source](https://developers.cloudflare.com/agents/)


## Shared core and native platform adapters

Chosen direction: platform-agnostic core, with macOS native integration first. Target macOS, Windows and Linux over time.

The shared domain core owns conversation/task state, tool contracts, capability routing, cancellation, result provenance and policy decisions. Cloudflare-specific hosting code belongs behind service boundaries; the existing cloud direction remains unchanged. Local-versus-cloud placement is still open.

Native adapters implement accessibility inspection/actions/events, screen capture, input, audio devices and desktop integration. Begin with macOS; later add Windows and Linux implementations. The shared core must not depend on native element objects, framework widgets or OS permission APIs.

Expose capability availability and permission state explicitly. Use scoped, short-lived element references and distinguish unsupported operations, denied permissions, stale references and transient errors. Preserve platform-specific semantics rather than promising identical behavior. Recheck authorization at the local execution boundary.

Keep real-time audio work independent of UI repainting. A separate native helper process is a proposal to evaluate, not a confirmed requirement. The GUI consumes core state and invokes capability contracts; the UI framework and core language are not selected.

## Offline-first clients and cloud authority

Confirmed in voice: clients should remain usable without internet, with cloud state as the source of truth and eager synchronization when connected. Local persistence, pending operations and reconnection handling are required design areas. Exact offline capabilities, local inference, reconciliation/conflict rules and data upload scope remain open. Distinguish provisional local changes from cloud-accepted state; do not silently discard offline work.

Initial offline scope clarified: typed chat as a request queue; no live voice conversation or local-model requirement. Show queued work distinctly from executing or completed work. Reconnect behavior and saved-artifact availability remain open.
