# Verification agent

Status: Concept

Category: Quality

## Purpose

Independently evaluate whether a specialist output meets the requested outcome, using evidence rather than the worker’s success claim.

## Responsibilities

Run trusted acceptance checks in a fresh environment.
Inspect protected changes, regressions, and source quality.
Compare outputs against task criteria.
Return an evidence-based pass, fail, or needs-attention result.

## Inputs and context

Immutable candidate artifact; original task contract; trusted check definitions; scoped test data.

## Outputs and evidence

Verification report tied to exact artifact/commit; failures; evidence; recommendation.

## Tools and execution environment

Fresh sandbox; browser checks; policy engine; trusted check store; optional separate model.

## Allowed authority

Read candidate artifacts and execute checks. Cannot grant itself release authority or rewrite mandatory checks.

## Boundaries and sensitive data

Candidate code remains untrusted during verification.
No production secrets in test processes.
Model review is a signal, not a correctness guarantee.
Checks and policy must be outside candidate-editable scope.

## Dependencies

Shared identity, job protocol, scoped permissions, audit trail

## Open questions

What checks are mandatory for each project?
When do we use a second model?
What failures warrant repair versus escalation?

## First useful milestone

Verify the first coding patch independently and reject a deliberately failing fixture.

