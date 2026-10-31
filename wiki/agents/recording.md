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

Confirmed audio requirements: English and Hindi, including mixed-language conversation. Support system audio as well as the microphone, with music identification as one example task. Exact capture/session controls and implementation remain open; no continuous capture default is selected.

Explicitly started sessions may continue with the workspace window closed, including meeting recordings. Require a visible listening/capture indicator near the notch or equivalent on non-notch displays whenever capture is active. Closing the workspace does not stop a session by itself; dismissal, stop controls, sleep handling and retention must be defined separately. This is not automatic permission to record all meetings.

Final retention clarification: transcription may lag and is mainly for later reference. Do not retain original audio by default after processing. Retain a recording only on explicit user request, including as a meeting/conversation backup. Distinguish delayed reference transcription from responsive live voice. Saved-recording duration, temporary buffers, provider handling and deletion remain open.

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

