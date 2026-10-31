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
