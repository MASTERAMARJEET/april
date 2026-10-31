# Ideas and working notes

## Research tool preference — 31 October 2026

User preference: use Exa rather than the Context7 MCP wherever possible for research and documentation discovery. Prefer primary and official sources when evaluating technical capabilities. This preference is recorded for the April project; it has not modified global assistant settings.

## Clarification conversation preference

Treat a natural pause as completion of the current answer and move to the next useful question without waiting for repeated confirmation. Review the existing wiki before asking architectural questions. Build on settled directions (Cloudflare execution, specialist agents, GitHub review, Mac-first client) rather than asking the user to restate them. Ask one focused question at a time and keep recording answers.

## Resume the clarification session

Session paused by user on 31 October 2026. Do not restart the questionnaire. Use the latest [question ledger](workspace/clarification-status.json), including partial answers, and ask one focused question at a time. Several topics are deliberately deferred to implementation or separate deep dives, not forgotten.

Highest-priority remaining clarifications: concrete initial guardrail/action classes and learned-approval boundaries; private grant expiry/revocation; encryption key custody and recovery; sync conflicts and deletion; task retry/cancellation and mistake recovery; costs and resource budgets; minimum bootstrap acceptance criteria. Other remaining product questions include replacement workflows, knowledge curation/corrections, cross-device sessions and remote capabilities, activity visibility, and later Windows/Linux support scope.

Explicitly deferred: plugin internals, API-versus-UI choice per integration, Codex-inspired computer-use deep dive, memory-system research (including Supermemory), headless interface, and final GUI/language selection. Final audio decisions: transcripts may lag; no retained audio by default, with explicit opt-in for saved meeting/conversation recordings.

## Future specialist ideas

Travel planning, health information organization, learning coach, household administration, finance summaries, and creative projects. Each needs its own data scope and action policy.

## Working context

This is a living design workspace, not a deployed agent system. Seeded from the conversation on 30 October 2026. Agent responsibilities and architecture choices are proposals unless marked as a chosen direction.

Next design conversation: pick one vertical slice and define its job contract, permission boundary, persistence, and success checks.

## Clarification review — original 50 questions

30 answered, 20 partial, 0 entirely open. The partial items include explicitly deferred design details; this does not mean implementation decisions are complete. Partial means the direction is known but a detail remains unresolved. See [question-by-question review](workspace/clarification-status.json).

Next priorities: cloud/key access to encrypted private vaults; private-grant lifetime/revocation; local/cloud sync conflicts; first native accessibility workflow and observation scope; resource/cost budgets; first coding acceptance criteria and recovery behavior. Languages, recording scope and detailed device handoff can be clarified later unless needed by the bootstrap.

Latest pass: original broad questionnaire is covered, with 20 scoped/deferred follow-ups. Confirmed task-end private grant expiry, soft $20 AI nudge, efficiency/fluidity over shipping speed, verified M2 Pro/16 GB Mac baseline, phone-to-Mac capabilities, preserve both sync conflicts, clarify/correct wiki conflicts, reviewed learned approval, proactive simple work and missing-capability task resumption. Next: evaluate architecture/GUI against these requirements; do not repeat settled preference questions.
