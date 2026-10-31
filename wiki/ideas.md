# Ideas and working notes

## Research tool preference — 31 October 2026

User preference: use Exa rather than the Context7 MCP wherever possible for research and documentation discovery. Prefer primary and official sources when evaluating technical capabilities. This preference is recorded for the April project; it has not modified global assistant settings.

## Clarification conversation preference

Treat a natural pause as completion of the current answer and move to the next useful question without waiting for repeated confirmation. Review the existing wiki before asking architectural questions. Build on settled directions (Cloudflare execution, specialist agents, GitHub review, Mac-first client) rather than asking the user to restate them. Ask one focused question at a time and keep recording answers.

## Git delivery preference

User instruction: whenever changes are committed in April, push them to the configured `origin` as well. Complete the push and verify synchronization before reporting delivery complete. Report a blocked or failed push explicitly; do not claim a local-only commit has reached origin. Do not force-push to satisfy this preference.

## Resume the clarification session

Paused at the user's request after the broad product pass. The original 50-question ledger has 32 answered and 18 scoped/deferred follow-ups, not 18 missing product directions. Do not restart the questionnaire or repeat confirmed choices. See [question ledger and technical follow-ups](workspace/clarification-status.json).

Next session: compare architecture/GUI options against the recorded workflows and measured constraints. That question is now closed: approved cloud tasks, including private-vault tasks under their existing task-scoped grant, continue if the Mac disconnects. All files live in cloud storage; the Mac is a lightweight client.

Settled in the latest pass: private grants end with tasks; additional approval categories evolve through use; dedicated learned approver and reviewed default allowances; conversational mistake correction; Cloudflare $5 base-plan target (usage unverified), AI $20 soft nudge with work continuing; efficiency and fluidity over shipping speed; M2 Pro/10-core/16 GB Mac baseline; phone requests may use authorized online Mac; preserve both sync conflicts and ask; ask/correct wiki conflicts; proactive simpler work and discuss larger features; inform/add missing capabilities then resume; no language preference; replace ChatGPT workflows and manual Cursor prompting while retaining underlying tools.

- Confirmed: approved cloud/private-vault tasks continue when the Mac disconnects. Next: design key custody, revocation and device-unavailable handling without reopening that preference.
- Engineering evaluation: unified voice overlay and artifact workspace, plugin-ready architecture, low resource use and fluid interactions on the verified M2 Pro / 16 GB Mac.
- Private grants: task-end expiry is decided; specify revocation, terminal-state handling, derived-context cleanup, encryption keys and recovery.
- Sync: preserve both conflicting edits and ask the user is decided; specify lineage, resolution propagation, deletion and reconnection.
- Coding bootstrap: Cloudflare execution, April-only GitHub repositories, dev/PR/user approval flow are decided; validate macOS packaging/native tests and exact release evidence.
- Deferred deep dives: plugin contracts/trust, per-integration API versus UI, Codex-inspired computer use and memory systems including Supermemory.
- Operational implementation: accurate cost tracking and non-blocking $20 AI nudge, task retry/cancellation, recovery history and permission enforcement.

## Future specialist ideas

Travel planning, health information organization, learning coach, household administration, finance summaries, and creative projects. Each needs its own data scope and action policy.

## Working context

This is a living design workspace, not a deployed agent system. Seeded from the conversation on 30 October 2026. Agent responsibilities and architecture choices are proposals unless marked as a chosen direction.

Next design conversation: pick one vertical slice and define its job contract, permission boundary, persistence, and success checks.

## Clarification review — original 50 questions

32 answered, 18 partial, 0 entirely open. The partial items include explicitly deferred design details; this does not mean implementation decisions are complete. Partial means the direction is known but a detail remains unresolved. See [question-by-question review](workspace/clarification-status.json).

Next priorities are the technical follow-ups above. Languages, initial recording scope, grant expiry, conflict behavior and starting budget already have recorded answers; do not ask those preferences again.

Latest pass: original broad questionnaire is covered, with 18 scoped/deferred follow-ups. Confirmed task-end private grant expiry, soft $20 AI nudge, efficiency/fluidity over shipping speed, verified M2 Pro/16 GB Mac baseline, phone-to-Mac capabilities, preserve both sync conflicts, clarify/correct wiki conflicts, reviewed learned approval, proactive simple work and missing-capability task resumption. Next: evaluate architecture/GUI against these requirements; do not repeat settled preference questions.
