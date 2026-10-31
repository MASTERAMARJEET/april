# Supermemory deep dive for April

Research checkpoint: 1 November 2026. Memory Q&A is paused pending review of this section. This is a documentation-based investigation, not an installed integration or a benchmark. Supermemory is a behavioral reference; no provider, deployment or license has been selected.

## Findings at a glance

The useful model is three connected layers: original source material, extracted facts with relationships over time, and a compact profile for conversational context. April can learn from that separation without adopting every Supermemory default. In particular, April’s private-task grants, user-led conflict clarification and deletion rules must remain authoritative.

Research used Exa across three angles: processing/retrieval, deployment/privacy/cost, and correction/review/deletion. Eighteen search-result entries were returned across four searches, including the preliminary correction lookup; repeated URLs were consolidated. Primary documentation was fetched for closer inspection. Vendor descriptions are not independent verification of quality, security or performance.

## 1. From a conversation or file to usable context

Supermemory accepts raw documents, including chat text, and performs extraction, chunking, embedding and indexing. Indexed source chunks and extracted graph facts are distinct outputs. A third output is a profile derived from the accumulated context.

An important consistency detail: document processing completion does not necessarily mean memory extraction is complete. The default dynamic processing groups related material; an instant option processes a document separately when immediate memory availability matters. Stable document identities help represent evolving conversations.

For April, this suggests separate readiness states for file storage, searchable source material, extracted memory and refreshed conversational context. An acknowledgment that a file synced must not promise that April already recalls its contents. Background processing should stay outside the responsive voice path. These are proposed architecture implications, not a selected implementation. [Pipeline documentation](https://supermemory.ai/docs/concepts/how-it-works)

## 2. What the graph represents

The graph distinguishes a changed fact, an added detail, and an inferred conclusion. Updated facts take precedence for present-time retrieval while prior knowledge can remain historical. The documentation also describes temporary information expiring and low-value chatter being less likely to become durable memory.

For April, an inference must remain distinguishable from something the user actually stated. Automatic resolution is not blanket permission to settle ambiguous contradictions: the existing requirement is to ask the user about conflicting wiki information before correcting it and proceeding. A genuine change over time and an unresolved contradiction need different treatment. [Graph model](https://supermemory.ai/docs/concepts/graph-memory)

## 3. Retrieval and profiles

The documented retrieval paths serve different purposes: source chunks ground answers in documents; memory search retrieves extracted facts and relationships; profiles provide concise durable and recent context. Profiles include static and dynamic sections and can be shaped through categories.

For April, a small permitted profile can accompany the conversation, while task-specific retrieval supplies additional evidence. The earlier proposal for a concurrent context model remains a candidate, not something this API alone proves is needed. A profile must never silently include medical or financial facts just because an earlier task was authorized to read them. [Quickstart retrieval paths](https://supermemory.ai/docs/quickstart), [profile API](https://supermemory.ai/docs/v5/api-reference/profiles)

## 4. Corrections, history and API versions

The initial lookup found an older API page describing a direct memory update that preserves the original version. The current memory-operations guide explicitly says v5 has no direct memory-create or memory-update route: source documents are ingested or updated, and extracted memories follow. Do not combine legacy examples and current SDK signatures into one assumed contract.

The confirmed April direction is to use Supermemory as the correction-behavior reference: current answers should reflect corrected information, with history inspectable where supported. The exact provider API, correction propagation latency, old-version retrieval and profile invalidation need a version-pinned experiment before implementation. [Legacy update endpoint](https://supermemory.ai/docs/api-reference/content-management/update-a-memory-creates-new-version), [current memory operations](https://supermemory.ai/docs/recall/memory-operations)

## 5. Inferences can be reviewed

Supermemory documents a queue for inferred facts and actions to approve, decline or undo a review. Approval removes the inference flag; declining removes the inferred item from search through forgetting. Notably, these review routes are still documented under the older route family, despite current namespace terminology.

This provides a reference for April’s inspectable memory controls. It does not establish whether April should interrupt the user for every inference. The established preference is quiet memory use with user inspection and tuning; frequency and presentation of review remain open. [Inference review](https://supermemory.ai/docs/recall/memory-review)

## 6. Forgetting is not necessarily erasure

The memory-operation documentation describes forgetting as soft deletion: records stop appearing in search but are retained. Semantic bulk forgetting can preview matches; applying the exact reviewed IDs avoids changes in a repeated semantic match.

April must distinguish removal from retrieval, source-file deletion, the recoverable bin, and eventual permanent erasure. Its existing rule puts deleted sources and their summaries into the bin for a weekly user review. That rule is not automatically satisfied by forgetting extracted facts. Source chunks, profiles, derived memories, caches, logs, backups and restored copies need a documented deletion and regeneration policy. Cross-source derivation behavior remains unverified. [Memory operations](https://supermemory.ai/docs/recall/memory-operations)

## 7. Privacy boundaries and task-scoped access

Supermemory describes namespaces as isolation boundaries and metadata as organization/filtering within them. Namespace-scoped requests and credentials are useful primitives, but do not by themselves implement April’s task-bound grants. A general agent credential able to read all private namespaces would defeat the intended separation.

Proposed April boundary: a memory broker checks task identity, approved source scope and grant status before retrieval, extraction or profile inclusion. Restrict access before content enters a model, not just when formatting its answer. Private-derived context remains private; grant expiry removes future agent access while leaving the user free to view saved files. The exact mapping from vaults to namespaces is not selected. [Organization and filtering](https://supermemory.ai/docs/concepts/filtering)

## 8. Hosted service versus self-hosting

The security page states encryption and a no-training commitment. Those statements do not establish zero retention by every model, extractor and other processor. Deployment-specific contracts, subprocessors, logs and retention terms require the audit already requested for April. No sensitive project data was uploaded during this research. [Security overview](https://supermemory.ai/docs/overview/security), [privacy policy](https://supermemory.ai/privacy/)

The local product is documented as a downloadable server binary with a non-public server codebase, distinct from open-source SDKs. It uses a supplied model; remote models and some content extraction paths can still send data outside the host. Offline text processing is possible with local components, but it is not equivalent to all formats being processed offline.

Running this binary within April’s chosen Cloudflare deployment has not been validated. A managed-service adapter, a compatible self-hosted service or an independently built subsystem remain alternatives. [Local deployment](https://supermemory.ai/docs/self-hosting/overview), [local versus enterprise](https://supermemory.ai/docs/self-hosting/local-vs-enterprise)

## 9. Cost and quality need workload evidence

The reviewed pricing page lists a free allowance and a paid Pro subscription of $19/month, with ingestion and other operations consuming credits. This is separate from April’s voice/model spend and Cloudflare charges. A paid memory service could consume much of the initial approximate $20 AI budget; suitability cannot be inferred from the subscription alone. Model a representative week of conversation, files, updates, retrieval and reprocessing before choosing it. Prices and licensing require rechecking at selection time. [Pricing](https://supermemory.ai/pricing/)

No retrieval-accuracy, latency, multilingual or resource benchmarks were executed. Vendor benchmark claims are not accepted here as proof for April’s English/Hindi, long-running voice and privacy requirements.

## 10. Evaluation plan before adoption

Use synthetic fixtures first, with no private user material:

1. Correct a stated preference; verify current answers, retained history and profile refresh.
2. Present a real time-based change and an ambiguous contradiction; verify the latter triggers clarification under April policy.
3. Query immediately after ingest and after extraction; measure readiness and stale-context behavior.
4. Mix English and Hindi; evaluate missed facts, wrong inferences and retrieval quality.
5. Authorize one private source for one task; verify no sibling source or general profile leakage, including after expiry.
6. Delete a source and its summary; check chunks, facts, profile, cache and re-ingest behavior through bin review and purge.
7. Reject an inference; verify it is not silently regenerated from unchanged sources without the intended policy.
8. Restart or replay events; test idempotency, duplicate extraction, recovery and realistic cost.

Acceptance thresholds, fixture implementation and a provider comparison remain future work. No installation or subscription is authorized by this document.

## Resume the conversation here

The unanswered memory-browser question is parked, not rejected; prior sessions already established user inspection and tuning as a requirement. Avoid asking that preference again as though new.

First explain the three-layer model and correction/version distinction. Then resolve these architecture choices one at a time:

- Use Supermemory as a service, evaluate its self-hosted binary, or borrow the design for an owned subsystem?
- How should uncertain inferred facts be presented and used before user review?
- How should corrections and forgetting propagate across source history, graph facts, profiles and cached context?
- Which retention and deletion controls are required beyond removing facts from retrieval?
- How will memory extraction and retrieval enforce private task grants without contaminating the general profile?

The existing requirements remain in force. This research does not reopen settled choices or silently adopt all vendor defaults.
