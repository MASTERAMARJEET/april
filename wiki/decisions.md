# Decision log

Preserve rationale and validation steps when revising a decision. Chosen direction is distinct from implementation complete.

## Cloudflare as platform

Status: Chosen direction

User preference: use Cloudflare as the platform. Specific products and limits still need validation.

Next validation: Keep job contracts and data export portable; avoid requiring every component on day one.

## One interaction agent

Status: Chosen direction

One main agent communicates with me and delegates to specialists across devices and future apps.

Next validation: Define user identity, channel identities, sessions, and notification behavior.

## Pi as agent harness

Status: Proposed

Pi is the preferred open agent direction from the conversation, but CLI and Pi Durable are separate choices.

Next validation: Compare a minimal durable coordinator with a Pi CLI sandbox worker; test version compatibility.

## Autonomy through policy

Status: Chosen direction — clarified in voice on 31 October 2026

Avoid approval for each command. Give agents broad authority within user-configured guardrails and escalate defined exceptions. The user can tighten or relax guardrails according to observed performance; the agent does not independently expand its own authority.

Next validation: Write per-domain action classes: read, draft, modify, share, delete, spend, deploy.

Voice clarification: start restrictive and request permissions more often early on. Explore an approver model that learns from approvals and denials, handles suitable actions on the user's behalf over time, and escalates exceptions. The promotion of learned preferences into delegated authority, along with fixed boundaries and revocation, still needs an explicit design decision.

## Self-improving system

Status: Chosen product direction; execution controls need investigation

Coding bootstrap scope clarified in voice: only April's own repositories initially. The user will add other projects later. Repositories will be hosted on GitHub, and PR review/approval will use GitHub's system. This is a future hosting/review requirement, not a request to create or push a repository now. GitHub remains the review record even when review conversations happen through April.

Bootstrap with conversation, add coding and deployment capabilities for April's own app, harness and supporting services, then use those capabilities to extend the system incrementally. This is the user's intended development strategy. Coding specialist may improve the platform without directly controlling its own guardrails; release scope and approval requirements remain open.

Next validation: Define evaluation suite, protected policy store, staged rollout, versioning, and rollback.

Confirmed initial release workflow, clarified in voice: April can implement features, deploy them to a development environment, and open a pull request. The user reviews the PR, intent and related artifacts, then approves it before merge and production deployment. Exact merge/deploy execution, checks and rollback remain to be specified. This describes future April capabilities, not authorization to deploy the current project now.

For big features, April should arrange a discussion before beginning implementation, clarify what the user wants, and explore how the feature would best support them. What qualifies as big and how discussions are scheduled remain open. No calendar event or automation is requested at this stage.

Further user clarification: the user decides when the feature plan is ready to proceed. Either April may arrange the discussion or the user may initiate one and develop the feature collaboratively. Over time, PR reviews should also be possible through conversation. The UI should preserve an explicit record of what scope or revision was approved; the exact confirmation interaction remains to be designed.

## Canonical memory and wiki

Status: Direction clarified; implementation open

Need durable personal knowledge with provenance, corrections, and export. User proposes queryable retrieval plus a parallel model that maintains memory and supplies relevant conversational context. Long-term aspiration is comprehensive memory, with behavior tuned over time. Supermemory is a research reference, not a selected provider.

Confirmed interaction preference: store and use memory quietly. Provide inspection of stored information and controls for refining what is retained or excluded. Exact correction/deletion behavior and retention policies remain open.

Confirmed exception: financial and medical information should be kept separate and excluded from ordinary memory. The user can explicitly tag information or request access for a particular task, providing provisional task-scoped access. This does not authorize general retention or cross-task reuse. Storage, expiry, cleanup of derived copies and tagging semantics remain open.

Next validation: Choose formats, entity IDs, conflict handling, retention, and deletion propagation.

## Recordings and media processing

Status: Open

Device capture, speech processing, and sensitive identity/location enrichment are not yet designed.

Next validation: Validate consent flow, provider data handling, on-device options, and storage costs.

## Cross-device synchronization

Status: Offline-first direction confirmed; sync semantics open

The eventual client should work without connectivity, with the cloud serving as the source of truth. Synchronize eagerly while online and after reconnecting. The design workspace itself still uses browser-local edits and manual export/import; it does not implement this product requirement.

Offline functionality is not yet specified: distinguish local content, capture and queued work from local speech/model inference and autonomous execution. Define reconciliation of offline changes with cloud-authoritative state, conflict behavior, deletion propagation, ordering and user-visible sync status. Eager sync does not imply every raw artifact is uploaded regardless of policy.

Subsequent user clarification: initially, offline interaction falls back to typed chat that queues requests. Live voice/conversation mode is unavailable offline. Local inference and offline autonomous execution are not required for the first version. Queue processing on reconnect, cancellation/editing of queued requests, and offline access to saved artifacts remain to be specified.

Next validation: Design authenticated clients, session merge, offline queue, and channel notification deduplication.

Latest clarification supersedes any proposed private-vault sync exclusion: both public-to-April and private vaults live on Cloudflare and sync eagerly with local artifacts whenever connected. Cloudflare is the source of truth. Encryption and secure defaults are requirements; encryption architecture, key custody, recovery and sync implementation are not selected. Storage/sync does not grant the agent access. Public vaults are easier for agents to access; private vault access requires an explicit permission request each time a new grant is needed, preserving provisional task scope and expiry.

## Central approval agent and explicit overlay confirmation

Status: Chosen direction — voice clarification, 31 October 2026

All approval requests are routed through a central approval agent/model. April and specialists do not bypass it by directly presenting permission requests. The approval service owns the request flow and presents an overlay with details of what the user is authorizing. For private-vault permission, the user clicks an explicit button; spoken agreement must not be interpreted as approval. Log the exact authorization action for auditing.

This centralizes approval across the system. Earlier learned-approver aspirations remain within user-granted policy; they do not override mandatory explicit private-vault consent. Exact grant lifetime, request fields, trusted UI/service boundary, verification of click provenance, enforcement, revocation and audit integrity remain design work. The requirement to store encrypted data does not yet specify end-to-end encryption or model access to decryption keys.

Further approval-loop clarification: April continues initiating permission requests as usual through the central approval system. The dedicated approval model evaluates which requests need user involvement, auto-approves within policy and learns from user decisions. Repeated prompts for actions the user routinely permits can be reviewed and promoted into explicit default allowances in April's operating context/policy, reducing unnecessary future requests. This is a reviewed policy-learning loop, not unilateral permission expansion by a requesting agent. Existing explicit private-access and release requirements remain until the user changes them. Do not reopen whether an approval model exists as an unresolved product choice.


## Platform-agnostic core; macOS integrations first

Status: Chosen direction — 31 October 2026

Build the core for macOS, Linux and Windows. Implement accessibility and other native integrations on macOS first, then add platform adapters. This supersedes a macOS-specific architecture; simultaneous platform parity is not required.

GUI framework, language, native process layout and later Linux support matrix remain open. Swift remains useful for the macOS adapter rather than being assumed as the shared foundation.

Next validation: exercise the same capability contract with a macOS implementation and a fake alternate-platform adapter. Run core tests on all three operating systems as soon as implementation starts.

Confirmed client rollout: Mac first → web → native Android. This sequencing does not change the platform-agnostic core direction. Windows/Linux client timing and iOS support remain open.

## Mac activation and visual presence

Status: Chosen direction — voice clarification, 31 October 2026

Start with a configurable key held for a few seconds. Summoning reveals a notch-originating wave/blob with distinct listening and speaking states. The exact key and thresholds remain open; release, non-notch, focus and monitor behavior are clarified below. Investigate wake-word activation later; continuous listening is not an initial requirement.

Activation semantics subsequently confirmed: holding the configured key activates a persistent voice session; releasing the key does not end it. April remains active until the user explicitly dismisses it by voice or double-presses the configured key (described as double-clicking the key). Exact hold threshold, double-press timing, recognition of dismissal and mic/session behavior during failures or OS sleep remain open. This does not authorize listening outside an activated session.

Focus behavior confirmed: summoning April must not take keyboard focus away from the application the user is working in. The current app retains focus and typing can continue during voice interaction. Focus when the user explicitly opens or interacts with April's vault browser is a separate detail.

Non-notch display fallback confirmed: April is invisible while inactive; activating with the configured key reveals the listening/speaking indicator from a top-center position just below the menu bar, using the suggested capsule/overlay approach. Do not require a permanent idle indicator. Notched displays retain the notch-originating presentation. The active-display rule is clarified below.

Multi-monitor behavior subsequently confirmed: show April on the display the user is actively working on, including an external monitor. Do not default to the built-in Mac display or designated primary display. The active display uses its own notch/non-notch presentation. How active work is detected and how an ongoing session moves between displays remain implementation details to specify.

## Provider-portable realtime voice

Status: Initial provider direction chosen; API capabilities require verification

The user wants to interrupt April naturally by speaking, as in the current voice interaction. Start by building on OpenAI's realtime voice API (referred to conversationally as GPT Live). Explore the full exposed feature set, with a replaceable provider layer that preserves the desired interaction behaviors when switching providers.

This does not establish that every provider offers identical capabilities or that every API feature must ship in the first release. Verify current official documentation before selecting API/model details; define required behavior, optional capabilities, compatibility tests and fallbacks. Provider-neutral session, audio, interruption, cancellation and tool-event contracts are proposed design work, not implemented interfaces.

## User-owned artifact vaults

Status: Chosen direction — voice clarification, 31 October 2026

Save artifacts to user-accessible folders at locations the user chooses. Provide a default vault and additional vaults for personal, financial and medical matters (work deferred), inspired by Obsidian. Active-vault scope, switching, permitted cross-vault access, file formats and sync rules remain open. Sensitive vaults retain the previously confirmed task-scoped access and ordinary-memory exclusions.

Subsequent clarification supersedes blanket active-vault isolation: vaults have cross-context accessibility classes, described by the user as public and private. Public-to-April vaults are accessible independently of conversations; browsing another vault does not change the conversation. This describes internal agent access, not internet publication or sharing with other people. The exact allowed operations remain to be defined.

Private vaults require explicit permission to access specific information from another context. Access is temporary and removed after a period of time; for example, financial information requested while in the personal vault. Define grant scope, lifetime, revocation, operation permissions and cleanup of retrieved context. Financial/medical memory exclusions remain in force. Defaults for new vaults and whether private-vault activation itself grants access are unresolved.

## Non-blocking artifact updates

Status: Chosen direction — voice clarification, 31 October 2026

Use a vault browser to indicate new and edited artifacts. The user may review them now or later. Merely not viewing an artifact must not block subsequent tasks. A genuine need for user action may block dependent work; viewing and granting approval are distinct states. Badge behavior, read-state synchronization and exact action-required UI remain open.

## Vault browser: Obsidian-inspired, integration under evaluation

Status: Obsidian-inspired layout chosen; separate Obsidian host ruled out

User prefers an Obsidian-style workspace, imitating its interaction patterns where appropriate: files/folders and tabbed artifacts. Desired content includes Markdown, DOCX, JavaScript and interactive files in one place. User proposes using Obsidian itself plus an April integration plugin to avoid rebuilding the viewer. This is an evaluation request, not a decision to adopt Obsidian or permission to install plugins.

Historical evaluation findings: Markdown, PDFs and common media are supported directly; DOCX and JavaScript/interactive artifact viewing require additional integrations or external viewers. Custom plugin views are available. Obsidian plugins inherit application access rather than providing reliable per-plugin permission isolation, so vault privacy and execution of generated interactive artifacts need boundaries outside a plugin alone. April's core, native voice shell and future web/Android clients should remain independent of an optional Obsidian surface. Office fidelity, isolated interactive rendering, multi-vault grants and sync ownership require a prototype before selection.

User clarification: DOCX preview is sufficient initially; full Word editing inside April is not required. This strengthens the case for prototyping Obsidian as the initial artifact interface, but adoption is still under discussion. Reuse its navigation, tabs and Markdown editing; add scoped April integration, update/action indicators, document previews and isolated interactive surfaces as needed. Do not assume that Obsidian itself implements April's cross-vault grants or future web client.

Final direction from the subsequent voice clarification: do not require switching between April and another application. Build a unified April application that includes the vault browser, even if workspace functionality must be implemented. Reuse existing libraries where appropriate. Obsidian remains a UX reference; using it as a required separate host is ruled out for the primary experience. This supersedes the proposed Obsidian-host prototype. The unified shell, Markdown editing, DOCX preview and isolated interactive artifact requirements must inform the pending UI framework choice. Optional external integrations are not prohibited, but cannot be required for the core workflow.

## Headless product interface

Status: Deferred by user

No CLI or API interface for interacting with April is needed right now. The initial product interface is the app. This does not rule out internal APIs or a future headless client.

## Initial application integrations and extensibility

Status: Initial targets confirmed; plugin design deferred

Start with Cursor (coding-agent workflow), Slack and the user's browser. Exact browser and first workflows remain open. Explore a plugin system that expands April's integrations over time; return to its design later. Naming Cursor as a target does not by itself replace the proposed Pi/cloud harness. Third-party packaging and trust model remain open.

Further clarification: plugin architecture is a major confirmed direction, not merely an optional integration idea. It should cover app/tool integrations, specialist subagents and vault artifact handlers, including Markdown, PDF, Word, interactive HTML and JavaScript. Detailed architecture is deferred for a later focused discussion; no plugin framework or implementation has been chosen.

API-versus-UI preference is explicitly deferred to implementation. User recognizes a service API may be easier for an integration such as Slack, but has not chosen a universal preference. Proposed architectural response: capability/plugin contracts describe intent and required authority without assuming either a cloud API or a local UI. Each implementation declares device/connectivity needs and permission scope; do not make access to the local desktop mandatory for cloud-capable operations.

## Staged desktop awareness and computer use

Status: Chosen direction; detailed computer-use design deferred

Initially April sees only content the user explicitly shares. Over time, add broader awareness of desktop applications and then the ability to interact with those apps on the user's behalf, under the central permission model. Use Codex's computer-use interaction experience as a north star and study it in a separate session. This is a UX/capability reference, not a claim of access to proprietary internals or a decision to copy implementation. Ongoing desktop monitoring or control is not an initial default.

## Initial speech languages and audio inputs

Status: Chosen requirements

Support English and Hindi initially, including primarily English conversations with occasional Hindi mixed in. Include system-audio capture alongside microphone input. A user example is recognizing which music is playing. System audio is a capability requirement, not a choice to record continuously; activation, permission, routing, retention and music-identification implementation remain open.

## Background capture and visible listening state

Status: Chosen requirements

An explicitly started listening/recording session can continue when the workspace window is closed, including meeting capture through available audio inputs. Show an indicator whenever April is listening or recording, suggested as a small light beside the notch; use an equivalent on displays without a notch. This extends the earlier inactive-overlay rule: inactive can remain invisible, but active capture must remain visibly indicated. Closing the workspace is not equivalent to dismissing an active session. Explicit session start/stop, OS sleep, termination, retention and meeting consent details still need design. System-audio capability alone does not mean every meeting is automatically recorded.

## Transcription and audio retention

Status: Chosen requirements — final voice clarification

Transcription is mainly for later reference and may lag; the user does not need to read a live transcript of everything. This does not relax responsiveness requirements for spoken conversation. By default, do not retain audio recordings after processing. The user can explicitly request retaining a recording, including a meeting or important conversation, as a backup if transcription misses something. This final clarification supersedes the earlier blanket no-audio statement. Temporary processing buffers, provider retention, retention duration for explicitly saved recordings and deletion behavior remain implementation questions; no zero-retention implementation has been verified.

## Private-vault grant lifetime

Status: Confirmed by user

Access approved for a task ends when that task ends. It must not remain available for later unrelated tasks. A fixed wall-clock lifetime is not the selected primary expiry rule. Terminal-state handling (completion, failure, cancellation), early revocation and cleanup of cached/derived task context need implementation specification.

## Evolving approval rules and mistake correction

Status: User preference clarified; mechanisms open

Discover additional access/approval categories incrementally during use rather than defining every category now. Existing explicit private-vault and production-review requirements remain in force; deferring other categories is not blanket permission.

When the user notices a mistake, they expect to ask April to fix it conversationally. Automatic rollback, version-history retention, undo scope and behavior for irreversible side effects are not selected. Proposed supporting design: preserve enough provenance and recoverable history to investigate and correct changes, without treating conversational correction as a guarantee that every action can be undone.

## Replacement workflow targets

Status: Confirmed user goal

Replace the user's ChatGPT app workflow for text, voice and computer use. Progressively take over much of the user's manual Cursor prompting. Keep the existing phased bootstrap and initial integration scope; full parity is a destination, not an initial-release promise.

User confirmed the integration boundary: initially retain Cursor as the editor, Slack as its client, and the existing browser. April orchestrates those tools rather than rebuilding them. Its own voice/chat/artifact workspace remains the unified interaction surface; existing tools may still be used or shown when a workflow calls for them. Do not treat this as selecting particular API or UI adapters.

## Initial operating budget

Status: User budget preference confirmed; actual costs unverified

User expects to start with the Cloudflare $5 Workers plan and approximately $20/month for AI usage. AI spend may increase if needed based on actual monthly use. These are starting budget targets, not a verified estimate that all infrastructure fits within $5 or blanket authorization for unlimited spending. Validate sandbox/container, storage, traffic and other usage costs before implementation. Warning thresholds, overage approval and hard caps remain open.

Overage behavior clarified: $20/month AI is a soft threshold, not a blocking cap. April should ask/nudge the user about additional spend but may keep working while that request is pending. This does not establish unlimited spending authority or a separate hard safety ceiling; exact overrun bounds, notification frequency and accounting remain implementation questions. Route the budget request through the central approval flow; do not suspend ordinary work solely because the soft threshold is reached.

## Client performance priorities

Status: Confirmed user priorities

Prioritize efficient resource use and fluid, non-janky interaction over shipping sooner. Evaluate idle CPU/memory/battery use as well as voice, overlay and artifact responsiveness under load. No numeric targets or UI framework have been selected. Resource efficiency should not be reduced to executable size or renderer benchmarks alone; compare representative end-to-end workloads. Minimum supported Mac hardware remains unspecified.

Technology preference clarified: no strong programming-language preference or exclusion. Choose the best fit for the established requirements, portability, resource efficiency and fluid interaction. Framework/language selection is an engineering evaluation, not an unanswered personal preference.

## Away-state task management

Status: Direction confirmed; detailed rules deferred

April may manage notifications and task state while the user is away; detailed triggers and behaviors will be mapped later. Keep cloud task state, scheduling, notification decisions and resumable user-attention requests independent of an open Mac window. Device-dependent actions still require an available, authorized device. This supports the existing Cloudflare/background-agent direction and does not select a new framework or grant blanket authority to send messages to other people.

## Resolve conflicting wiki information through clarification

Status: Confirmed user preference

When April encounters conflicting wiki information, actively prompt the user for clarification before choosing a version. Correct the wiki according to that clarification, then continue the affected work from the corrected version. Do not silently resolve the conflict or merely leave competing versions unresolved. Preserve provenance and revision history as supporting design; unrelated work need not be blocked. Mechanisms for surfacing the request, invalidating stale derived context and applying edits remain implementation work.

## Proactive small work; discuss substantial work first

Status: Confirmed product boundary; detailed routing deferred

April can proactively research and perform simpler day-to-day work within existing authority. Research or notes may produce ideas that feed into coding; exact routing and triggers will be mapped later. Substantial work, such as building a feature, requires a conversation with the user before proceeding. This elaborates the existing feature-planning requirement rather than granting automatic implementation of every researched idea. The user considers this sufficient direction for now; do not require exhaustive proactive-task classification during this pass.

## Missing capability as a self-extension workflow

Status: Confirmed desired behavior

If a user-requested task requires an unsupported feature, April should tell the user, add the capability where feasible, then complete the original task. Keep the user in the loop instead of treating unsupported functionality as an automatic dead end. Preserve the original objective while tracking implementation as a dependency. This extends the self-improvement vision; it does not supersede the existing substantial-feature conversation, central permission flow, development/PR review and production-approval boundaries. The meaning of notification versus explicit go-ahead for small additions remains to be clarified as needed.

## Initial Mac hardware baseline and remote use

Status: User-selected baseline; hardware verified locally

Initial performance baseline: the user's current MacBook Pro, Apple M2 Pro, 10-core CPU (6 performance + 4 efficiency), 16 GB unified memory, currently macOS 26.7.1. Hardware read locally at the user's request; serial numbers and device identifiers are not recorded. Run efficiently and fluidly on this machine. This is an initial target, not a benchmark-proven minimum; older OS/hardware support remains open.

User confirms that a request from the phone may use capabilities on an online, authorized Mac. Device availability and scoped permissions remain required. Exact remote routing, sleep/offline handling and device selection remain implementation work.

## Local/cloud edit conflicts

Status: Confirmed user preference

If local and cloud edits conflict, preserve both versions and ask the user which to keep. Cloud authority does not justify silently discarding local work. Conflict detection, version lineage, merge choices and propagation of the resolved version remain implementation details.

## Cloud-first tasks; approved work survives Mac disconnect

Status: Confirmed user architecture clarification

All tasks are cloud-first and most work runs in Cloudflare. All files, including public and private vault contents, have cloud storage as their persistent home and source of truth at all times. The Mac is a lightweight client for voice, visuals and local device integrations; local copies and offline pending changes synchronize with cloud state. Approved cloud tasks, including private-file tasks, continue if the Mac disconnects, within the existing task-scoped grant. Disconnection neither revokes the grant nor expands its scope; private access still expires when the task ends. Operations needing a local integration require that device to be reachable. Encryption-key custody, revocation and enforcement remain implementation work.

Supersedes resumption notes that described private-task continuation after Mac disconnection as unanswered. No additional authorization is required merely because the client disconnects; new scope still follows the central approval flow.

## Vault-independent conversations

Confirmed user clarification: Conversations are not tied to a particular vault. Vaults organize stored data and access, not conversational sessions. Public-to-April vaults are available to April across conversations without an active-vault switch granting access. Browsing a vault in the UI does not create a new conversation or restrict the conversation to that vault. Private vaults retain explicit task-scoped approval and task-end expiry. This supersedes earlier suggestions that the active vault defines the conversation context; an individual tool operation may still target a specific vault.

## Initial vault scope: personal, medical and financial

Confirmed: Initial scope excludes work and any work vault. Start with personal, medical and financial vaults. Work can be reconsidered later. Vaults remain storage/access boundaries, not conversation containers; public-to-April vaults are always available, private data requires task-scoped approval.

## One user-facing thread, internally managed context

Confirmed user direction: The user interacts through a single ongoing thread and does not manage separate conversation sessions. April may internally organize, branch and manage task/topic context as needed. Internal context/session boundaries are implementation details, not user-facing vault boundaries. Vaults remain independent storage/access domains. This does not require one ever-growing model prompt or bypass private-data approvals.

## Voice interruption is not task cancellation

Confirmed user direction: Spoken interruption stops or redirects the conversation, not delegated tasks. Heavy use of specialist/subagent execution is intended; tasks continue independently of the live conversation and require an explicit user instruction to interrupt/cancel them. Task lifecycle must be separate from voice playback/session lifecycle. Existing failure, permission and safety limits still apply; they are not overridden by conversational independence.

## Specialists can delegate to subagents

Confirmed direction: Specialist agents may delegate further to subagents within the original task authority; delegation is not restricted to the main interaction agent. Represent parent/child task relationships and return results through the hierarchy while April remains the single user-facing coordinator. Delegation does not expand private-data access or permissions. Depth/concurrency limits, budget allocation, conflict handling and cancellation propagation remain implementation decisions.

## Task overview and full delegation audit

Status: Confirmed user requirement

Show top-level task summaries for the ordinary overview. Also expose the full parent/child specialist/subagent tree for monitoring and audit rather than hiding nested execution. Exact fields and presentation remain to be designed; retain task lineage, status and evidence without exposing unrelated private context or credentials.

## Explicit pause and resume controls

Status: Confirmed user preference; execution semantics open

Provide task pause/resume, not only cancellation. The user asks where these controls would be useful; proposed presentation is conversational commands plus controls on task summaries/tree items. Useful cases include reviewing direction, supplying changed information or reprioritizing work. Voice interruption remains separate and does not pause tasks. Define safe checkpoints, in-flight side effects, child-task propagation, progress preservation and permission revalidation before implementing. Pause must not be described as undoing already completed actions or freezing an external operation instantly.

Pause propagation clarified: the user supplies a reason when pausing; the coordinator decides what should happen to relevant subagents based on that reason. Do not impose an unconditional stop-all-descendants rule. Record the reason and coordinator's decision for audit. Scope of a pause must respect the user's expressed intent; if that scope is materially ambiguous, clarification may be required rather than silently continuing the affected action. Safe-checkpoint and in-flight-operation handling remain engineering details.

## Escalate stuck specialists to the user

Confirmed user direction: When a specialist is genuinely stuck, bring the blocker to the user and work through it together. The user sees this as a possible sign that requirements need clarification or the specialist scope is too large. Do not silently substitute specialists, expand scope or run an autonomous repair loop as the default response to being stuck. Preserve task state and resume or rescope after clarification. The definition/detection of a blocker and handling of routine transient errors remain implementation details.

Pause reason taxonomy is explicitly deferred: the user supplies the reason at the time, and the coordinator interprets it. Do not require an exhaustive list during this design pass.

## Automatically send offline requests on reconnect

Confirmed user direction: Automatically send requests queued while offline when the client reconnects; no separate queue-review step is required. Sending a queued request is not approval to bypass private access, release or other policy checks. Ordering, deduplication, cancellation of unsent requests and stale-scope handling remain implementation details.

## Best-effort voice reconnection

Confirmed user direction: If connectivity drops during an active voice session, attempt automatic resumption on a best-effort basis. If recovery is not possible, the user can summon April again. Do not revive a session explicitly dismissed during the outage. Preserve visible connection/listening state; do not imply offline voice inference or default audio retention. Recovery deadlines, buffering and failure indicators remain implementation details.

Voice recovery timeout clarified: Bound automatic voice-session recovery to approximately five seconds. If it cannot resume within that attempt window, stop automatic resumption and wait for the user to summon/resume manually. Display recovery/failure state and do not reopen a dismissed session. Exact timer implementation remains engineering work.

## Full local vault copy initially; on-demand files later

Confirmed user direction: Initially keep/copy all vault files locally and synchronize everything to the cloud, simplifying the first version. Cloud remains authoritative and private-file agent access stays task scoped. Future direction: fetch only files being viewed or needed, keeping the rest cloud-only. Selective caching/pinning is not required initially. This describes future product behavior, not authorization to copy/upload the user's current files now.

## Recoverable deletion with seven-day user review

Confirmed final user preference: Deleting a vault file removes it from active use and synchronizes deletion while retaining a restorable bin entry. The user's final preference supersedes the earlier automatic seven-day purge idea: prompt the user to review pending deletions every seven days, and let the user clear them at review. Do not permanently purge solely because seven days elapsed. Preserve recoverability until the user explicitly clears the bin. This is a future April product workflow, not a request to create a real reminder/automation now. Bin permissions, private metadata, restores and replica/backup cleanup remain implementation details.

## Own-cloud processing and audited minimal disclosure

Confirmed user direction: Process as much data as possible within the user-controlled cloud environment. Send external AI providers, search tools and document-processing services only the minimum necessary content. Heavily audit services and select only those meeting the user's zero-data-retention requirement for the relevant service/endpoint and account configuration. This applies beyond model providers to external tools. No vendor or endpoint is verified or approved by this note; contractual promises, eligibility, exceptions, logging and actual configuration need validation. Private-file access grants do not imply unrestricted downstream disclosure.

## Quiet reconnection feedback

Confirmed user direction: After voice reconnection, do not give a spoken announcement. An optional brief chime may signal recovery; chime choice/settings are not finalized. Preserve the existing approximately five-second automatic recovery window and manual fallback.

## Long-term owned inference

Confirmed long-term user goal: Far-future direction: own/control the AI inference layer so private data processing no longer requires sending content to external AI providers. This is not an initial-release requirement and does not establish that a chosen Cloudflare product can host the required models. Preserve a replaceable inference/provider boundary now. Hardware, model quality, operating cost and any remaining external-tool dependencies need later evaluation; the user's goal is to keep data private under their control.

## Private classification follows derived artifacts

Confirmed direction: Artifacts derived from private material automatically inherit its private classification, including summaries. Do not place them in ordinary/public-to-April memory or expose them through less-restricted artifact views. Existing private-task approval boundaries still apply. Mixed-source classification, explicit declassification and retention/derived-context cleanup remain implementation details; no automatic declassification is selected.

## Delete derived summaries with private sources

Confirmed user direction: When a private source file is deleted, its derived summaries are deleted as well and follow the same restorable-bin and user-reviewed permanent-cleanup process. Do not leave the summaries as independently retained private artifacts by default. Maintain source-summary lineage for this behavior. Mixed-source summaries, restore consistency and indexes/embeddings need explicit implementation rules; the user specifically confirmed summaries, not an indiscriminate cascade to every linked document.

## Cloudflare-account-based identity and recovery direction

User prefers identity/setup and recovery tied to their Cloudflare account, with Access/OAuth-style facilities to be evaluated rather than a separate recovery-key UX chosen now. Official Cloudflare docs confirm Cloudflare-as-identity-provider support in Access and Managed OAuth for supported non-browser clients; evaluate native-client compatibility, policy, token/device lifecycle and account recovery before selecting the flow. Distinguish application sign-in from OAuth permissions to manage Cloudflare resources and from encryption-key recovery. This does not create/configure accounts, grant credentials or settle key custody.

Verified official references via Exa:

- [Cloudflare as identity provider](https://developers.cloudflare.com/cloudflare-one/integrations/identity-providers/cloudflare/)
- [Access Managed OAuth](https://developers.cloudflare.com/cloudflare-one/access-controls/applications/http-apps/managed-oauth/)
- [Authorizing access to Cloudflare resources](https://developers.cloudflare.com/fundamentals/oauth/authorizing-an-application/)

## Reviewed first-party plugins initially

Confirmed direction: Start with plugins built and reviewed as part of April itself. Leave interfaces extensible enough for external plugins later; no marketplace or external-plugin installation system is required initially. Third-party refers to authorship, not multiple users. Reusing reviewed external libraries is not excluded. Existing central approval, private-vault scope and isolated artifact execution rules still apply.

## Three plugin roles

Status: User confirmed

Confirmed plugin roles: integrations perform actions/access external or local capabilities; specialists handle delegated work; renderers display artifact types and interactive content. Plugins declare capabilities and needed access, while permission decisions/enforcement remain centrally controlled. Different roles may need different execution hosts; no universal runtime or packaging format has been selected.

## Pin running tasks to their plugin version

Confirmed default: Default plugin update behavior: tasks already running finish on the plugin version they started with; new tasks use the approved updated version. Do not hot-swap plugin behavior inside an in-flight task by default. Record the version with task/audit data. Retention of old versions, dependency resolution, resume behavior and exceptional migration handling remain engineering work.

## Independent plugin releases

Confirmed direction: Plugins should be independently installable/updatable rather than requiring a whole April release for every change. Bundled releases would be simpler initially, but independent lifecycle fits incremental self-extension. Use reviewed, versioned releases and compatibility checks; running tasks keep original versions. Cloud/client/runtime host distinctions and native packaging/signing constraints must be evaluated: changes to native client capabilities may still require a client release. No plugin packaging/runtime product has been selected.

## Automatic rollback of failed plugin updates

Confirmed user direction: If a plugin update fails after rollout, automatically revert to the last known working plugin version and notify the user. Record failed and restored versions plus rollback evidence. This is the chosen recovery default, not a requirement to await user permission before reverting. Concrete health criteria, affected in-flight task recovery, compatibility/data-migration handling and irreversible side effects still require design; code rollback must not be assumed to undo external actions.
