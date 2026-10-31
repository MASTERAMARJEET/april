# Coding agent

Status: Concept

Category: Builder

## Purpose

Improve my coding projects and the agent system itself with substantial autonomy inside a disposable development environment.

## Responsibilities

Turn scoped objectives into patches.
Build, test, debug, and inspect browser behavior.
Maintain project knowledge and dependency hygiene.
Return evidence, limitations, and a reproducible change.
Propose improvements to the agent platform without controlling its release policy.

## Inputs and context

Repository + exact commit; selected work-in-progress patch; task brief; acceptance criteria; allowed services; budget.

## Outputs and evidence

Patch or branch; test evidence; browser screenshots; implementation summary; unresolved risks.

## Tools and execution environment

Pi CLI; Cloudflare Linux sandbox; Browser Run; scoped repository broker; package registries.

## Allowed authority

Autonomous commands and edits inside one task sandbox. Write candidate branches through a broker. No direct production deployment.

## Boundaries and sensitive data

No production secrets or broad cloud token.
Cannot change external verification, permission, or release policies.
Fresh verification runs outside the coding sandbox.
Self-modification must pass a separate release path; no editing the running coordinator.

## Dependencies

Shared identity, job protocol, scoped permissions, audit trail

## Open questions

Which stacks need Docker networking or larger disks?
Which changes qualify for automatic merge?
How do we test the agent system before promoting a new version?
How many repair attempts are allowed?

## First useful milestone

Implement a small change in one low-risk repository, run checks, and return a patch and preview.

