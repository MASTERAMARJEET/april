# Vision

One interaction agent, available across my devices and eventually my apps, that understands my intent and delegates to specialized agents. Specialists carry deep capabilities while the main agent keeps me informed. The system should manage real projects with bounded autonomy, protect my personal data, and improve over time.

## What success feels like

I can request a useful outcome from any device, leave, and return to a trustworthy result. I receive evidence and concise updates without approving every tool action. Personal knowledge and artifacts become easier to find, correct, and understand. The platform improves without silently widening its own authority.

## Principles

- One relationship, many specialists.
- Delegate outcomes with explicit scope, not unrestricted access.
- Persist useful knowledge; discard untrusted execution environments.
- Separate facts, inferences, preferences, and authorization.
- Protect originals; make changes reversible where possible.
- Verify independently before consequential release.
- Keep data, contracts, and model choice portable.
- Treat autonomy as a policy, not an absence of safeguards.

## Product clarification — voice conversation, 31 October 2026

Confirmed preferences from the user:

- Voice is the primary entry point, activated by a button or a wake word. Which activation modes ship first remains open.
- April should be available on both phone and laptop, with seamless continuity between them. Phone OS, exact handoff behavior and delivery sequence remain open.
- April should assist throughout the day rather than center on one isolated task or moment.
- Agents do work in the background and surface results as artifacts, websites and other useful interfaces.
- Interactive interfaces can collect information or let the user perform an action.
- Chat remains available in the background; it should not define the primary product experience.
- The existing cloud-agent design and specialist briefs remain the context for the broader vision.

Delivery order clarified later in the voice conversation: start with Mac alone, then add web support, then native mobile starting with Android. Phone/laptop continuity remains the destination rather than a first-release requirement. Windows/Linux remain core portability targets; their client delivery dates are unspecified.

These preferences do not imply continuous microphone recording, ambient monitoring, or permission to interrupt at any time. Listening, awareness, notification behavior and autonomy still require clarification.

## Memory direction — voice clarification, 31 October 2026

The long-term aspiration is an encompassing agent that remembers everything relevant to the user. Start pragmatically with a queryable memory engine and a parallel model that processes conversational context, maintains useful memory and supplies relevant context to the active conversation. Tune memory behavior over time toward the user's preferences.

“Remember everything” describes the aspiration, not authorization to capture every device signal or retain all data indefinitely. Capture sources, exclusions, retention, correction, deletion and context-injection rules remain open.

User clarification: April may store and use learned information quietly, without announcing each new memory. The user must be able to inspect what is stored and progressively tune what April does and does not store. This preference concerns information available through authorized interactions; it does not settle additional capture sources or indefinite retention.

## Sensitive information exception — voice clarification, 31 October 2026

Financial and medical information must stay separate from ordinary persistent memory. April should still help with those topics, but the user wants to explicitly tag the relevant information or ask for access, granting provisional access for a specific task. Such access is not blanket permission to retain the information in general memory or reuse it for unrelated tasks.

The storage mechanism for separately held information, exact tagging semantics, access expiry and deletion of task-derived copies remain to be designed. Apply the exclusion to automatic memory maintenance and context enrichment as well; inspect logs, summaries and derived artifacts when defining retention behavior.

## Mac interaction and vaults — voice clarification, 31 October 2026

Initial activation: press and hold a configurable key for a few seconds. The key is not selected. Release does not end the activated session. Wake-word activation is a future investigation, including ongoing microphone access; it is not required initially.

Later clarification resolves release behavior: the hold activates an ongoing session that persists after key release. Dismiss by an explicit spoken request or double-press of the configured key. Hold/double-press thresholds and failure handling remain open; no listening outside an activated session is implied.

Summoning the voice interface must preserve keyboard focus in the current application rather than activating April's UI. The user should be able to continue typing there while speaking with April.

On displays without a notch, keep April invisible while inactive. On summon, reveal a top-center capsule/indicator below the menu bar; it disappears when dismissed. Notched displays use the notch-originating visual. The active-display rule is clarified below.

Multi-monitor clarification: April should appear on whichever display the user is actively working on, including external monitors. Select the appropriate notch/non-notch presentation for that display. Detection and movement during an ongoing session remain to be defined.

When summoned, April should emerge visually from the notch, with a line/wave or blob animation and distinct listening and speaking behavior. Non-notch, multi-monitor and focus behavior are clarified below; fullscreen handling remains open.

Artifacts should be saved in an accessible folder chosen by the user. Use an Obsidian-inspired vault model: a default vault, with additional vaults that can be opened for different contexts, such as work, everyday personal use, financial matters and medical matters. File formats, storage layout, indexing, cloud sync and active-vault behavior remain open.

Financial/medical vaults do not override the sensitive-memory exception: opening or storing a vault does not by itself grant general memory retention or background access. Explicit provisional access for a particular task remains the confirmed requirement; clarify how vault selection relates to that grant.

Vault boundary clarification: the active vault is the main context, but vaults marked public for April may be consulted across contexts (e.g. work schedule from personal). Private vaults need explicit permission for specific information, with temporary access that later expires. Public does not mean internet-public. This replaces blanket isolation between all vaults; private-vault access and sensitive-memory exclusions remain explicit boundaries.

## Artifact presentation and task continuity

Confirmed Mac interaction: a vault browser indicates newly created and edited items. The user chooses whether to inspect them immediately or later. An unread artifact does not block April from continuing subsequent work. Pause dependent work only when an actual user action is required, such as input or approval; unrelated authorized work can continue. Exact badge/read-state design, change previews and notification routing remain open. The user explicitly confirmed that public vaults mean internally accessible across vaults, not internet-public.

## Unified application requirement

Keep the primary experience in April itself: voice, vault browsing, document previews and interactive artifacts should not require hopping between applications. Use an Obsidian-inspired workspace, but do not depend on the separate Obsidian app as the primary viewer. Reuse suitable editing, preview and layout libraries rather than assuming all components must be authored from scratch. DOCX preview is sufficient initially. Select the UI framework with these requirements in mind; no framework is selected yet.

## Audience and distribution

Confirmed in voice: personal use first. Longer term, anyone with a Cloudflare account and a MacBook should be able to use April. Multi-user hosted-service design and exact installation/account provisioning remain unspecified; do not require multi-user accounts for the initial version.
