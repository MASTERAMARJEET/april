# Roadmap

A proposed sequence of useful vertical slices.

## User-prioritized bootstrap — voice clarification, 31 October 2026

This sequence takes priority over interpreting the topical sections below as a fixed delivery order.

1. Establish the initial conversational experience, following the voice-first product direction. First device: Mac. Initial scope: voice-first conversation; refine concrete acceptance criteria.
   User clarification: the first client is Mac alone. Add web support after the Mac version, then native mobile support starting with Android. The timing of Windows/Linux clients and any iOS client remains open; the core remains platform-agnostic.
2. Add coding capability focused on April itself, then the ability to deploy changes to its app, agent harness and supporting infrastructure, including database-related work.
3. Use that coding capability to help extend April's features and capabilities incrementally.

Initial feature delivery: discuss big features before implementation → build and test → deploy to development → open PR with supporting artifacts → user review and approval → merge and production deployment. Specify checks, release authority and rollback before enabling the final steps.

The user intends self-extension as the development strategy. It is not permission for the current assistant to deploy infrastructure, access credentials or modify its own authority. Deployment scope, review, verification, migrations and rollback require design; existing separation of verification/release authority remains the baseline proposal.

## Foundation

- [ ] **Define offline behavior and sync** — Cloud-authoritative state, local persistence and pending operations, eager online synchronization, reconnect/conflict handling; initially typed offline requests queue; no local inference or offline voice requirement.
- [ ] **Implement the initial offline fallback** — Typed chat queues requests while disconnected; live voice is unavailable. Define reconnect dispatch, editing/cancellation and visible pending status. Local inference is outside the initial requirement.
- [ ] **Write the identity and permission model** — Who can request what, for which data, on which device?
- [ ] **Define the shared job and result contract** — IDs, acceptance criteria, scope, budget, state transitions, evidence, cancellation.
- [ ] **Select the canonical state and export formats** — Keep ownership portable and separate originals from derived records.

## First vertical slice

- [ ] **Build main-agent chat → one coding job → result** — One authenticated web client, one low-risk repository, fresh sandbox, patch output.
- [ ] **Test crash recovery, cancellation, and cost ceilings** — Deliberately disconnect clients, restart workers, and fail provider requests.
- [ ] **Add independent checks and a preview** — Verify the exact candidate in a fresh environment; show evidence.

## Knowledge

- [ ] **Build the first wiki learning path** — One topic, three depths, citations, freshness, corrections.
- [ ] **Deep-dive memory architecture later** — Study Supermemory and compare alternative memory systems. Evaluate agent-initiated retrieval, parallel memory maintenance and context enrichment, relevance, provenance, contradiction handling, latency, cost, user correction, retention/deletion and portability. Research has not yet been performed; no provider is selected.

## Capture & artifacts

- [ ] **Pilot an authorized recording upload** — Timestamped transcript, notes, corrections, and retention.
- [ ] **Index a chosen small media collection read-only** — Original preservation, metadata provenance, reversible labels.

## Controlled autonomy

- [ ] **Define and test automatic release policies** — Low-risk project first; exact-artifact checks, health monitoring, rollback.
- [ ] **Enable staged platform self-improvement** — Separate candidate, evaluator, and release authority.

## Expansion

- [ ] **Add second-device access and notification preferences** — Resume context safely and avoid duplicate interruptions.


## Desktop core and first native integration

- [ ] **Define provider-portable voice behavior** — Natural barge-in; initial OpenAI realtime provider; review current official feature set. Specify session/interruption/tool behavior, required versus optional capabilities and compatibility tests before claiming equivalent behavior from another provider.
- [ ] **Prototype Mac summon and voice states** — Configurable held-key activation; notch-originating listening/speaking wave or blob. Use the confirmed persistent session, explicit dismissal, no focus theft and active-monitor notch/non-notch presentation; tune thresholds and failure handling. Wake-word investigation is later.
- [ ] **Define artifact vaults** — User-chosen folders, default and additional vaults, active context, file ownership, sync and explicit sensitive-vault task access. Clarify whether cloud authority applies equally to all vault contents.
- [ ] **Define the portable core boundary** — Conversation/task state, capability contracts, cancellation and provenance; decide local/cloud placement.
- [ ] **Build a fake platform adapter** — Exercise supported, unsupported, denied and stale-target outcomes without macOS dependencies.
- [ ] **Implement one macOS accessibility slice** — Discover a target, read its tree, observe a change and execute one scoped action with permission handling.
- [ ] **Validate shared core on all three OSes** — Add a CI matrix when code exists; UI/native features may remain macOS-only initially.
- [ ] **Validate documents and interruptible audio** — Choose the UI only after testing the same workload against shortlisted frameworks.
- [ ] **Add Windows and Linux adapters later** — Define the supported Linux environments and capability differences before promising parity.
