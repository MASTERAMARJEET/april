# Coding agent

## Confirmed initial scope

Access only April's own repositories initially; other user projects will be added explicitly later. Repositories are intended to be hosted on GitHub, with PR review and approval through GitHub. Conversational review should connect to that review record. Repository creation, credentials and access grants are not being configured by this design discussion.

Execution direction explicitly reaffirmed: coding builds and tests run on Cloudflare, consistent with the existing cloud specialist architecture. Do not reopen Mac-versus-cloud execution as an undecided preference. Platform-specific macOS build/signing and native testing support still need an implementation plan; choosing Cloudflare does not establish those capabilities in a Linux sandbox.

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

