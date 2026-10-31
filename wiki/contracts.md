# Shared contracts

Draft fields for a portable task protocol; not yet an implemented API.

## Job

```text
jobId / parentJobId / userId / specialist / repository or resource IDs
objective / acceptanceCriteria / inputArtifacts / baseRevision
allowedOperations / networkPolicy / credentialScopes
modelBudget / wallClockLimit / retryLimit / cancellation
policyVersion / requestedBy / authorizationReference
```

## Result

```text
jobId / status / outputArtifacts / exactRevision
summary / evidence / checks / uncertainty
sideEffects / resourceUsage / followUpQuestions
provenance / retention / nextRecommendedAction
```

## Lifecycle

```text
Requested → Authorized → Queued → Running → Verifying → Completed
Alternative outcomes: Needs attention / Failed / Cancelled / Expired
A completed worker turn is not necessarily a verified task outcome.
Checkpoint before retries; make external side effects idempotent.
```


## Native capability boundary

Proposed contract fields supporting the confirmed platform-adapter direction; not an implemented API.

```text
Capability: deviceId / platform / adapterVersion / capabilityVersion
            operation / availability / permissionState / limitations
Request: requestId / taskId / deviceId / operation / targetRef
         arguments / deadline / cancellation / authorizationReference
Result: requestId / status / value / observedAt / provenance
        errorKind / retryable / sideEffects
Events: subscriptionId / sequence / observedAt / targetRef / change
```

Targets are adapter-owned references with explicit validity; do not serialize native pointers. Handle missing events, stale references and interrupted sessions. Side-effect retries require reconciliation or deduplication rather than blind replay. Linux/Windows adapters may report capabilities unavailable before they are implemented.

## Task-scoped sensitive context

Confirmed user preference: financial and medical information is excluded from ordinary memory and made available provisionally through explicit user tagging or an access request for a specific task. Proposed access contract: authorized data references, purpose/task ID, permitted operations, expiry/revocation, and retention constraints. Enforce the boundary for specialist context, memory enrichment and task-derived copies; exact implementation and cleanup rules remain open.

## Cross-vault access

Confirmed semantics: public-to-April vaults can be consulted from other active contexts; private vaults require explicit, temporary permission for specific information. These labels do not describe public internet sharing. Proposed grant fields include source/active vault, target vault and item references, task/purpose, permitted operations, user authorization, expiry and revocation. Expired grants must not allow continued access through cached context; the exact context/derived-data cleanup mechanism remains to be designed.

Storage clarification: both classes are cloud-hosted, encrypted by requirement and eagerly synchronized. Private status limits agent use, not whether data may sync to Cloudflare.

## Approval requests and audit

Confirmed: all requests route through the central approval agent. Private-vault access uses an overlay describing the scope and an explicit user button click; voice assent is insufficient. Proposed record fields: request and task identity, requesting specialist, vault/item references, operations, purpose, expiry, policy version, displayed scope, click/denial event, granted scope, revocation and execution evidence. Bind the recorded decision to the exact request and enforce grants outside the model. Final schema and trust mechanisms remain open.

Private-grant lifetime clarified: bind access to the approved task and expire it when that task ends. Do not carry the grant into subsequent tasks. Implement terminal-state and cleanup semantics explicitly.

Sync conflict requirement: preserve both conflicting local/cloud versions and request user resolution before discarding either. Cloud-authoritative state must not silently overwrite unresolved local changes.

## Cloud execution continuity

An approved cloud task continues after the Mac disconnects, including a private-file task under its existing grant. Bind authorization to task identity and scope, not client connectivity. Expire private access at task end; preserve explicit revocation and scope enforcement. Local integration steps report device unavailability separately from cloud task authorization. All persistent files are cloud-backed; offline edits are pending synchronization rather than a separate authoritative store.

## Session scope versus storage scope

Confirmed user clarification: Conversations are not tied to a particular vault. Vaults organize stored data and access, not conversational sessions. Public-to-April vaults are available to April across conversations without an active-vault switch granting access. Browsing a vault in the UI does not create a new conversation or restrict the conversation to that vault. Private vaults retain explicit task-scoped approval and task-end expiry. This supersedes earlier suggestions that the active vault defines the conversation context; an individual tool operation may still target a specific vault.

Session design requirement: preserve one user-facing thread while tracking internal branches/tasks/context references independently. Vault identity is not conversation identity. Context routing, compaction and merge behavior must preserve scoped authorization and task provenance; protocol details are still open.

## Interruption domains

Confirmed user direction: Spoken interruption stops or redirects the conversation, not delegated tasks. Heavy use of specialist/subagent execution is intended; tasks continue independently of the live conversation and require an explicit user instruction to interrupt/cancel them. Task lifecycle must be separate from voice playback/session lifecycle. Existing failure, permission and safety limits still apply; they are not overridden by conversational independence.

## Parent and child task authority

Confirmed direction: Specialist agents may delegate further to subagents within the original task authority; delegation is not restricted to the main interaction agent. Represent parent/child task relationships and return results through the hierarchy while April remains the single user-facing coordinator. Delegation does not expand private-data access or permissions. Depth/concurrency limits, budget allocation, conflict handling and cancellation propagation remain implementation decisions.

Pause requests include the user's reason. The coordinator resolves which descendants pause or continue from that reason and records the decision; pause does not automatically apply identically to every child. Preserve task lineage, user intent and existing authority when resuming.

## Blocked specialist transition

Confirmed user direction: When a specialist is genuinely stuck, bring the blocker to the user and work through it together. The user sees this as a possible sign that requirements need clarification or the specialist scope is too large. Do not silently substitute specialists, expand scope or run an autonomous repair loop as the default response to being stuck. Preserve task state and resume or rescope after clarification. The definition/detection of a blocker and handling of routine transient errors remain implementation details.

Proposed runtime mapping of confirmed behavior: Running → Needs user input when stuck → Clarified/rescoped → Queued/Running. Keep the original objective, blocker, relevant task branch and changed scope linked for audit. This is a draft state mapping, not implemented execution.

## Offline request delivery

Confirmed user direction: Automatically send requests queued while offline when the client reconnects; no separate queue-review step is required. Sending a queued request is not approval to bypass private access, release or other policy checks. Ordering, deduplication, cancellation of unsent requests and stale-scope handling remain implementation details.

## Voice session recovery

Confirmed user direction: If connectivity drops during an active voice session, attempt automatic resumption on a best-effort basis. If recovery is not possible, the user can summon April again. Do not revive a session explicitly dismissed during the outage. Preserve visible connection/listening state; do not imply offline voice inference or default audio retention. Recovery deadlines, buffering and failure indicators remain implementation details.

Recovery deadline: approximately five seconds for automatic voice resumption; on timeout transition to manual-resume-needed rather than retrying indefinitely.

## Deletion and review lifecycle

Confirmed final user preference: Deleting a vault file removes it from active use and synchronizes deletion while retaining a restorable bin entry. The user's final preference supersedes the earlier automatic seven-day purge idea: prompt the user to review pending deletions every seven days, and let the user clear them at review. Do not permanently purge solely because seven days elapsed. Preserve recoverability until the user explicitly clears the bin. This is a future April product workflow, not a request to create a real reminder/automation now. Bin permissions, private metadata, restores and replica/backup cleanup remain implementation details.

## Downstream data handling

Confirmed user direction: Process as much data as possible within the user-controlled cloud environment. Send external AI providers, search tools and document-processing services only the minimum necessary content. Heavily audit services and select only those meeting the user's zero-data-retention requirement for the relevant service/endpoint and account configuration. This applies beyond model providers to external tools. No vendor or endpoint is verified or approved by this note; contractual promises, eligibility, exceptions, logging and actual configuration need validation. Private-file access grants do not imply unrestricted downstream disclosure.

## Derived-artifact privacy

Confirmed direction: Artifacts derived from private material automatically inherit its private classification, including summaries. Do not place them in ordinary/public-to-April memory or expose them through less-restricted artifact views. Existing private-task approval boundaries still apply. Mixed-source classification, explicit declassification and retention/derived-context cleanup remain implementation details; no automatic declassification is selected.

## Source-summary deletion propagation

Confirmed user direction: When a private source file is deleted, its derived summaries are deleted as well and follow the same restorable-bin and user-reviewed permanent-cleanup process. Do not leave the summaries as independently retained private artifacts by default. Maintain source-summary lineage for this behavior. Mixed-source summaries, restore consistency and indexes/embeddings need explicit implementation rules; the user specifically confirmed summaries, not an indiscriminate cascade to every linked document.

## Draft shared plugin contract

Confirmed roles: integration, specialist and renderer. Proposed contract fields, not implemented API:

- Identity/version, supported contract versions and role declarations.
- Capabilities, typed inputs/results and required execution host (cloud, local endpoint or renderer).
- Required resource/operation/network access, expressed as requests to the central approval/capability system rather than self-granted authority.
- Lifecycle and task correlation: initialization, invocation, progress, completion, failure, explicit cancellation, safe pause/resume and cleanup where applicable.
- Health, provenance and audit events linked to parent/child task lineage.
- Artifact media/schema support and isolated rendering/messaging boundaries for renderers.

Compatibility, packaging, secrets delivery, isolation mechanism and multi-role package structure remain engineering choices. Stuck specialist work escalates to the user under the confirmed policy.

## Plugin version binding

Confirmed default: Default plugin update behavior: tasks already running finish on the plugin version they started with; new tasks use the approved updated version. Do not hot-swap plugin behavior inside an in-flight task by default. Record the version with task/audit data. Retention of old versions, dependency resolution, resume behavior and exceptional migration handling remain engineering work.

Plugin lifecycle requirement: independent versioned updates with core/host compatibility checks. Bind task execution to an approved plugin version. Installation/update must not silently expand authority; approval policy and release verification still apply. Rollback, package integrity and old-version retention need concrete design.
