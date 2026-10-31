# Roadmap

A proposed sequence of useful vertical slices.

## Current design phase: refine component architecture before implementation

Recovered from the “April’s Cloud-First Architecture” conversation: first define the cloud task runtime and the lightweight client's connection to it, then evaluate the GUI framework. The user explicitly wants the component details refined before starting the first implementation slice.

Work through these designs in order. For each, record responsibilities, authoritative state, interfaces/events, permission boundaries, failure/recovery behavior, unresolved decisions and acceptance criteria. A component remains proposed until its design is resolved; a checklist entry is not an implementation claim.

- [ ] **Cloud runtime and sessions** — Main interaction coordinator, conversation/vault scope, specialist job lifecycle, independent verification, durable progress, cancellation and reconnect-independent execution.
- [ ] **Client/cloud protocol and voice** — Device identity, resumable connection, voice provider boundary, interruption/tool events, task updates, local capability calls and unavailable-device behavior.
- [ ] **Vaults, memory and synchronization** — Cloud-backed files, local copies, conflict resolution, encryption/key custody, provenance, quiet memory and sensitive-data exclusions.
- [ ] **Approval and policy service** — Request routing, trusted overlay decisions, reviewed learned allowances, task-end grant expiry, revocation, audit and enforcement outside the model.
- [ ] **Plugins and specialist contracts** — App/tool integrations, specialist agents, artifact renderers, compatibility, lifecycle and isolated interactive execution. Detailed plugin deep dive remains planned, not complete.
- [ ] **Mac client and GUI evaluation** — Voice overlay, focus/display behavior, integrated artifact workspace, accessibility and measured efficiency/fluidity on the recorded Mac baseline. Evaluate frameworks against the earlier contracts rather than assuming a choice.
- [ ] **Coding/release bootstrap and validation plan** — April-only GitHub repositories, Cloudflare build/test flow, Mac-specific validation, dev preview, PR evidence and user-approved production release.

Then define and implement the smallest end-to-end slice against those contracts. Avoid reopening confirmed product preferences while resolving engineering choices. Research provider-specific capabilities when that component is evaluated; use Exa preferentially and primary sources.

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

## Integration follow-up

- [ ] **Define first Cursor, Slack and browser workflows** — These are the user's initial application targets. Choose browser, read/control scope and API-versus-UI behavior.
- [ ] **Explore plugin extensibility later** — Expand supported tools/apps over time; define plugin contracts, installation and authority separately.
- [ ] **Deep-dive computer use separately** — Codex as UX/capability reference; initial explicit sharing, later wider app awareness and delegated interaction. Define accessible-tree/screenshot inputs, action permissions, uncertainty, focus and recovery during that investigation.

## Performance and device validation

- [ ] **Validate against the user's current Mac** — MacBook Pro, M2 Pro, 10-core CPU, 16 GB memory; current macOS 26.7.1. Measure idle resources and fluid voice/artifact interactions before claiming minimum support.
- [ ] **Support authorized remote Mac capabilities later** — Phone requests may use an online, authorized Mac; design scoped routing and unavailable-device behavior.

## Cloud-first continuity validation

- [ ] **Validate approved task continuity after Mac disconnection** — Cloud/public/private-file tasks continue under existing scope and task-end expiry. Local integration steps handle an unavailable device explicitly. All persistent files remain cloud-backed; verify sync recovery without changing the cloud-first requirement.

- [ ] **Study long conversations and internal threading** — Use Codex's experience as a reference for internal branches, context management and subagents while preserving one user-facing thread. Study publicly observable/documented behavior, not assumed proprietary internals.
- [ ] **Separate voice and task interruption** — Barge-in stops playback/conversation output; only an explicit task instruction cancels delegated work. Validate that voice dismissal/reconnect does not terminate subagents.

- [ ] **Start with full local vault mirroring** — Sync all initial vault files to cloud and retain a complete local copy. Later add on-demand materialization/cloud-only files without changing cloud authority or private access rules.

- [ ] **Implement recoverable deletion and review** — Sync active-file deletion into a restorable bin; prompt for review every seven days; only permanently clear after the user's explicit review/cleanup, not an automatic seven-day purge.

- [ ] **Audit external data processors before selection** — AI, search, document processing and other external tools: zero-retention commitments, exact endpoint/account eligibility, exceptions/logging, data minimization and configuration. No vendor is accepted by default. Prefer processing in the user-controlled cloud.

- [ ] **Far future: evaluate owned AI inference** — Keep provider interfaces replaceable now; later assess user-controlled inference and reduced external data disclosure. Not required for the initial release.

- [ ] **Evaluate Cloudflare-account sign-in** — Access Cloudflare IdP plus Managed OAuth is a documented candidate; validate Mac flow and separate user sign-in, deployment privileges and encrypted-data key recovery. No infrastructure setup is authorized by this design note.


## Memory research checkpoint

Memory Q&A is paused for the [Supermemory deep dive](research/supermemory.md). Review the documented behavior and API-version differences before resuming. Provider selection, private-grant enforcement and deletion propagation remain open; no memory integration is installed.
