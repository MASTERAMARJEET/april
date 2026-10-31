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

Save artifacts to user-accessible folders at locations the user chooses. Provide a default vault and additional vaults for contexts such as work, personal, financial and medical matters, inspired by Obsidian. Active-vault scope, switching, permitted cross-vault access, file formats and sync rules remain open. Sensitive vaults retain the previously confirmed task-scoped access and ordinary-memory exclusions.

Subsequent clarification supersedes blanket active-vault isolation: vaults have cross-context accessibility classes, described by the user as public and private. Public vaults may be consulted from another active vault, for example reading the work schedule while in the personal vault. This describes internal agent access, not internet publication or sharing with other people. The exact allowed operations remain to be defined.

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
