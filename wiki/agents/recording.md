# Recording & notes agent

Status: Concept

Category: Capture

## Purpose

Capture meetings, talks, and selected in-person conversations, turning them into useful notes and follow-ups with clear recording controls.

## Responsibilities

Start and stop only through explicit authorized capture.
Transcribe, label speakers provisionally, and summarize.
Extract decisions, action items, and unresolved questions.
Link approved notes to people, projects, and wiki topics.
Let me correct transcripts and delete recordings.

## Inputs and context

Explicitly selected microphone stream, meeting recording, video, or audio file; event context.

## Outputs and evidence

Transcript with timestamps; summary; action items; references; retention and consent record.

## Tools and execution environment

Device capture client; upload/streaming; speech-to-text; diarization; notes store; notification tools.

## Allowed authority

Capture only authorized sessions. Draft action items; creating calendar events or sending messages uses separate permissions.

## Boundaries and sensitive data

Visible recording state and immediate stop control.
Define consent and applicable recording requirements for each setting.
No silent always-listening default.
Speaker labels are provisional until confirmed.
Do not store audio indefinitely without a chosen retention policy.

## Dependencies

Shared identity, job protocol, scoped permissions, audit trail

## Open questions

Which device performs capture?
Which meeting apps and languages matter?
Can transcription be local?
How long do raw audio and transcripts persist?
When can notes be shared?

## First useful milestone

Upload one authorized recording and return timestamped notes with editable actions.

