# Release service

Status: Concept

Category: Control

## Purpose

Promote verified changes under explicit project policy, with staged deployment, health checks, and recovery.

## Responsibilities

Match approval evidence to the exact artifact.
Merge eligible changes and deploy through scoped APIs.
Monitor rollout health and trigger defined rollback.
Keep release and policy-change records.

## Inputs and context

Verified artifact; signed/authoritative job record; project release policy; environment.

## Outputs and evidence

Release record; deployment link; health outcome; rollback result.

## Tools and execution environment

Trusted deterministic service; deployment APIs; monitoring; backups.

## Allowed authority

Only narrowly defined release operations. Prefer deterministic policy evaluation over open-ended model authority.

## Boundaries and sensitive data

Not a general-purpose agent with a production shell.
No untrusted build script executes with deployment credentials.
Database rollback requires a separate plan.
Policy edits require an external authorization path.

## Dependencies

Shared identity, job protocol, scoped permissions, audit trail

## Open questions

Which environments can deploy automatically?
What is the rollback trigger?
How do we promote updates to the agent system itself?

## First useful milestone

Deploy one verified low-risk artifact to preview and record health evidence.

