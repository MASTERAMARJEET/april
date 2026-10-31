# Interaction agent

Status: Concept

Category: Coordinator

## Purpose

One familiar agent across my devices and, eventually, the apps I use. It understands intent, delegates work, and brings results back in the right level of detail.

## Responsibilities

Maintain conversational continuity across channels.
Clarify outcomes, not every implementation step.
Create scoped tasks for specialists and follow them to completion.
Reconcile conflicting results and surface consequential exceptions.
Remember preferences with provenance and allow correction.

## Inputs and context

Messages, voice, notifications, user preferences, specialist updates, project state.

## Outputs and evidence

Answers, plans, delegated jobs, concise progress reports, exception requests, durable decisions.

## Confirmed interaction direction — 31 October 2026

Voice-first interaction on phone and laptop, with cross-device continuity. Entry may be a button or wake word; activation uses a configurable held key initially; Android follows Mac and web. Background specialist work surfaces as artifacts, websites and interactive interfaces. Use those interfaces to collect input or support user actions. Chat is secondary rather than the main product surface.

The intended experience spans the user's day. Continuous recording, desktop observation and proactive interruption have not been authorized or selected by this preference.

## Context-aware delivery — voice clarification, 31 October 2026

Confirmed direction: decide whether and how to surface a result using its priority and whether user action is needed. Device-provided context should include which device the user is actively using. Adapt delivery to circumstances such as working at a desktop versus social time away from the laptop; the user expects April to make that judgment.

Open details: how work/home/social context is supplied or inferred; allowed signals and permissions; priority thresholds; interruption channels; confidence and freshness; explicit overrides. The examples do not select continuous location tracking, microphone monitoring or a specific sensor implementation.

## Adjustable autonomy — voice clarification, 31 October 2026

Confirmed preference: background agents should do as much as possible within user-configured guardrails. The user must be able to make those guardrails stricter or more permissive in response to observed agent performance.

This is a product requirement, not blanket authorization for current agents or individual consequential actions. Action classes, initial defaults, per-domain scopes, review and recovery mechanisms remain to be defined. The preference does not authorize an agent to expand its own permissions.

## Learned approval — voice clarification, 31 October 2026

Confirmed preference: begin with more restrictive defaults and ask for permission more frequently during early use. An approver model should learn from what the user permits and restricts, eventually approve suitable actions on the user's behalf, and flag cases needing attention.

The mechanism is still open: distinguish predicting a preference from granting authority. Clarify whether learned patterns first propose a standing rule for user approval or can become delegated approval behavior within an explicitly authorized scope. Hard boundaries, evidence thresholds, uncertainty handling, revocation and auditability remain unresolved. No automatic authority expansion is implemented or authorized by these notes.

## Collaborative feature planning and review

For substantial features, arrange a conversation before implementation or respond to a user-initiated planning conversation. The user decides when the plan is ready to proceed. Initial delivery uses a development environment and PR with supporting artifacts, followed by user approval before production. Conversational PR reviews are a desired later capability. Discussion scheduling mechanics, approval recording and release execution details remain open.

## Tools and execution environment

Conversation interface; task registry; specialist dispatch; memory search; scheduler; notification service.

## Allowed authority

Read approved shared summaries. Dispatch only registered task types within policy. Ask for exceptions when a requested action exceeds policy.

## Boundaries and sensitive data

Do not inherit every specialist credential.
Do not treat retrieved documents or tool output as user authorization.
Do not send unrelated personal context to a specialist.
A channel login does not automatically authorize sensitive actions.

## Dependencies

Shared identity, job protocol, scoped permissions, audit trail

## Open questions

How should conversations from different devices merge?
Which events deserve interruption?
What memory should be explicit versus inferred?
How do I revoke or correct a remembered preference?

## First useful milestone

A Mac voice-first conversation that submits an April coding task to Cloudflare, survives a disconnect, and reports the result; GitHub holds the review record.


## Mac interaction clarification

Unified April app with Obsidian-inspired vault browser; no required separate Obsidian host. Hold a configurable key to activate an ongoing session; dismiss by voice or double-press. Preserve current-app focus. Show distinct listening/speaking states on the active monitor, from the notch where available or a top-center overlay when not. Private-vault grants are explicit and temporary; public-to-April vaults allow cross-context consultation. Unread artifacts do not block authorized progress. Start with OpenAI realtime voice and natural interruption behind a replaceable provider boundary.

Approval routing clarified: all permission requests go to the central approval agent/service. April cannot bypass that service by sending its own prompt. Private-vault access is approved by an explicit button in an overlay showing the scope, with an audit record; spoken confirmation is not sufficient. Both public/private vaults sync eagerly to encrypted cloud storage; syncing is separate from granting access.

Cloud-first clarification: most work executes in Cloudflare; all persistent files are cloud-backed. The Mac is a lightweight voice/visual client and local-integration endpoint. Approved tasks continue when it disconnects, including private tasks within the existing grant; disconnection does not grant new authority.
