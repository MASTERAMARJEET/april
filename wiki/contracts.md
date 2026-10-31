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
