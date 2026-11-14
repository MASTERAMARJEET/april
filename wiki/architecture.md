# Architecture

Proposed allocation of responsibilities. Revalidate provider capabilities and maturity before implementation.

User channels → main interaction agent → scoped specialist jobs → independent verification → policy-controlled release/report.

Persist trusted state; discard untrusted execution environments. Cloudflare Computer provides workspace capabilities, the harness provides the agent loop, and a Linux sandbox provides isolated execution.

## Always-on agent design reference

[Building always-on agents](https://claude.com/resources/articles/building-always-on-agents), William Hu, Anthropic, 13 November 2026. Added as a reference for building April on 14 November 2026.

The article describes short, event-triggered runs with durable state between them. Its five primitives are an event inbox, timers, memory, permissions and an outbox.

Use it as an implementation checklist when evaluating April’s cloud coordinator:

- Durable event intake with deduplication, batching, retry recovery and one active worker per inbox.
- Persisted follow-ups and recurring schedules that enqueue work when due.
- Cross-run instructions, user context and task progress, with lean initial context and pointers to retrievable sources.
- Deferred approvals that resume through incoming events while other work continues.
- Outgoing delivery with recovery and notification pacing when needed; background runs may finish silently.

April-specific interpretation: map these responsibilities onto the candidate Cloudflare services while preserving the central approval service, private-data boundaries and single user-facing thread. The article’s internal sessions need not become separate user conversations. This is a design reference, not an adopted implementation; storage schemas, concurrency scope and delivery guarantees remain to be evaluated.

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

The shared domain core owns conversation/task state, tool contracts, capability routing, cancellation, result provenance and policy decisions. Cloudflare-specific hosting code belongs behind service boundaries; the existing cloud direction remains unchanged. Tasks are cloud-first; most work executes in Cloudflare. The Mac is a lightweight voice/visual client and native integration endpoint.

User clarification: agent coordination and specialist coding builds/tests belong on Cloudflare. The Mac provides the native interaction/device integration. Remaining placement questions concern particular capabilities and data boundaries, not whether the coding specialist should primarily execute on the Mac.

Native adapters implement accessibility inspection/actions/events, screen capture, input, audio devices and desktop integration. Begin with macOS; later add Windows and Linux implementations. The shared core must not depend on native element objects, framework widgets or OS permission APIs.

Expose capability availability and permission state explicitly. Use scoped, short-lived element references and distinguish unsupported operations, denied permissions, stale references and transient errors. Preserve platform-specific semantics rather than promising identical behavior. Recheck authorization at the local execution boundary.

Keep real-time audio work independent of UI repainting. A separate native helper process is a proposal to evaluate, not a confirmed requirement. The GUI consumes core state and invokes capability contracts; the UI framework and core language are not selected.

## Offline-first clients and cloud authority

Confirmed in voice: clients should remain usable without internet, with cloud state as the source of truth and eager synchronization when connected. Local persistence, pending operations and reconnection handling are required design areas. Initial offline interaction is queued typed input; local inference is not required. Reconciliation, deletion and sync implementation remain design work. Distinguish provisional local changes from cloud-accepted state; do not silently discard offline work.

Initial offline scope clarified: typed chat as a request queue; no live voice conversation or local-model requirement. Show queued work distinctly from executing or completed work. Reconnect behavior and saved-artifact availability remain open.

Both public-to-April and private vaults sync eagerly between local devices and Cloudflare, which is authoritative. Require encryption and secure defaults for all vault storage. Keep sync/storage authorization separate from task execution access: synchronized private data still requires a temporary explicit grant before agents can use it. Key custody, encryption boundaries and recovery remain to be designed; do not assume an encryption scheme is already chosen.

## Central approval service

April / specialist → central approval agent → scoped request shown in trusted overlay → explicit user button click → auditable grant → capability enforcement. Private-vault approvals cannot be inferred from voice. April does not directly issue permission prompts outside this flow. User-facing approval coordination is centralized; enforcement must occur at the resource/capability boundary rather than relying only on a model decision. Learned approval behavior is bounded by the user's policy and explicit-consent requirements.

## Plugin architecture — major direction, detailed design deferred

Confirmed user direction: build around a plugin architecture across three areas:

- Application/tool integrations, initially Cursor, Slack and the user's browser.
- Specialist/subagent capabilities and their integrations with the main agent.
- Vault artifact support, including Markdown, PDFs, Word documents, interactive HTML and JavaScript.

Treat extensibility as an architectural requirement rather than an assumption that every artifact renderer or specialist is built into the core. Return later to plugin contracts, discovery, packaging, lifecycle, compatibility, isolation, permissions and distribution. The user has not selected those mechanisms or requested plugin implementation now. Plugins must fit the central approval and vault-access boundaries; these requirements do not grant arbitrary execution or data access.

## Cloud-first execution and disconnected clients — confirmed clarification

All tasks are cloud-first and most work runs in Cloudflare. All files, including public and private vault contents, have cloud storage as their persistent home and source of truth at all times. The Mac is a lightweight client for voice, visuals and local device integrations; local copies and offline pending changes synchronize with cloud state. Approved cloud tasks, including private-file tasks, continue if the Mac disconnects, within the existing task-scoped grant. Disconnection neither revokes the grant nor expands its scope; private access still expires when the task ends. Operations needing a local integration require that device to be reachable. Encryption-key custody, revocation and enforcement remain implementation work.

This closes the previously unanswered private-task/offline-Mac question. Cloud task execution must not rely on a live Mac session to remain authorized; device-specific work still depends on the relevant endpoint. This is a documented requirement, not implemented infrastructure or a chosen key-management design.

## Conversation and vault boundaries

Confirmed user clarification: Conversations are not tied to a particular vault. Vaults organize stored data and access, not conversational sessions. Public-to-April vaults are available to April across conversations without an active-vault switch granting access. Browsing a vault in the UI does not create a new conversation or restrict the conversation to that vault. Private vaults retain explicit task-scoped approval and task-end expiry. This supersedes earlier suggestions that the active vault defines the conversation context; an individual tool operation may still target a specific vault.

## User-facing continuity and internal context branches

Confirmed user direction: The user interacts through a single ongoing thread and does not manage separate conversation sessions. April may internally organize, branch and manage task/topic context as needed. Internal context/session boundaries are implementation details, not user-facing vault boundaries. Vaults remain independent storage/access domains. This does not require one ever-growing model prompt or bypass private-data approvals.

## Independent conversation and delegated-task lifecycles

Confirmed user direction: Spoken interruption stops or redirects the conversation, not delegated tasks. Heavy use of specialist/subagent execution is intended; tasks continue independently of the live conversation and require an explicit user instruction to interrupt/cancel them. Task lifecycle must be separate from voice playback/session lifecycle. Existing failure, permission and safety limits still apply; they are not overridden by conversational independence.

## Nested specialist delegation

Confirmed direction: Specialist agents may delegate further to subagents within the original task authority; delegation is not restricted to the main interaction agent. Represent parent/child task relationships and return results through the hierarchy while April remains the single user-facing coordinator. Delegation does not expand private-data access or permissions. Depth/concurrency limits, budget allocation, conflict handling and cancellation propagation remain implementation decisions.

## Phased local file availability

Confirmed user direction: Initially keep/copy all vault files locally and synchronize everything to the cloud, simplifying the first version. Cloud remains authoritative and private-file agent access stays task scoped. Future direction: fetch only files being viewed or needed, keeping the rest cloud-only. Selective caching/pinning is not required initially. This describes future product behavior, not authorization to copy/upload the user's current files now.

## External processing and data minimization

Confirmed user direction: Process as much data as possible within the user-controlled cloud environment. Send external AI providers, search tools and document-processing services only the minimum necessary content. Heavily audit services and select only those meeting the user's zero-data-retention requirement for the relevant service/endpoint and account configuration. This applies beyond model providers to external tools. No vendor or endpoint is verified or approved by this note; contractual promises, eligibility, exceptions, logging and actual configuration need validation. Private-file access grants do not imply unrestricted downstream disclosure.

## Future inference ownership

Confirmed long-term user goal: Far-future direction: own/control the AI inference layer so private data processing no longer requires sending content to external AI providers. This is not an initial-release requirement and does not establish that a chosen Cloudflare product can host the required models. Preserve a replaceable inference/provider boundary now. Hardware, model quality, operating cost and any remaining external-tool dependencies need later evaluation; the user's goal is to keep data private under their control.

## Privacy propagation

Confirmed direction: Artifacts derived from private material automatically inherit its private classification, including summaries. Do not place them in ordinary/public-to-April memory or expose them through less-restricted artifact views. Existing private-task approval boundaries still apply. Mixed-source classification, explicit declassification and retention/derived-context cleanup remain implementation details; no automatic declassification is selected.

## Identity, provisioning authority and key recovery

User prefers identity/setup and recovery tied to their Cloudflare account, with Access/OAuth-style facilities to be evaluated rather than a separate recovery-key UX chosen now. Official Cloudflare docs confirm Cloudflare-as-identity-provider support in Access and Managed OAuth for supported non-browser clients; evaluate native-client compatibility, policy, token/device lifecycle and account recovery before selecting the flow. Distinguish application sign-in from OAuth permissions to manage Cloudflare resources and from encryption-key recovery. This does not create/configure accounts, grant credentials or settle key custody.

Verified official references via Exa:

- [Cloudflare as identity provider](https://developers.cloudflare.com/cloudflare-one/integrations/identity-providers/cloudflare/)
- [Access Managed OAuth](https://developers.cloudflare.com/cloudflare-one/access-controls/applications/http-apps/managed-oauth/)
- [Authorizing access to Cloudflare resources](https://developers.cloudflare.com/fundamentals/oauth/authorizing-an-application/)

## Plugin trust and initial distribution scope

Confirmed direction: Start with plugins built and reviewed as part of April itself. Leave interfaces extensible enough for external plugins later; no marketplace or external-plugin installation system is required initially. Third-party refers to authorship, not multiple users. Reusing reviewed external libraries is not excluded. Existing central approval, private-vault scope and isolated artifact execution rules still apply.

## Plugin roles and proposed execution boundaries

Confirmed plugin roles: integrations perform actions/access external or local capabilities; specialists handle delegated work; renderers display artifact types and interactive content. Plugins declare capabilities and needed access, while permission decisions/enforcement remain centrally controlled. Different roles may need different execution hosts; no universal runtime or packaging format has been selected.

Proposed mapping, not a selected implementation: cloud-first integration/specialist hosts; local capability endpoints only for operations needing a device; client-side artifact renderers in an isolated surface. Rendering a file does not confer filesystem, private-vault or arbitrary network authority. Packages may expose roles through stable contracts without making the core depend on one implementation language. Host/protocol details need validation.

## Plugin lifecycle separate from core releases

Confirmed direction: Plugins should be independently installable/updatable rather than requiring a whole April release for every change. Bundled releases would be simpler initially, but independent lifecycle fits incremental self-extension. Use reviewed, versioned releases and compatibility checks; running tasks keep original versions. Cloud/client/runtime host distinctions and native packaging/signing constraints must be evaluated: changes to native client capabilities may still require a client release. No plugin packaging/runtime product has been selected.
