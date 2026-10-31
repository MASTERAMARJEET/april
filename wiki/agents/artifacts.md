# Digital artifacts agent

Status: Concept

Category: Personal data

## Purpose

Organize my photos, documents, and other digital artifacts while preserving originals and keeping identity and location inferences reviewable.

## Responsibilities

Index approved libraries and find duplicates.
Group photos by time, place, event, and known people.
Connect artifacts to meetings, projects, and trips.
Propose organization and record every change.
Support corrections and deletion across derived metadata.

## Inputs and context

Selected photo/document libraries; EXIF; approved location history; user-confirmed people labels.

## Outputs and evidence

Searchable catalog; proposed albums and tags; duplicate candidates; provenance; reversible organization plans.

## Tools and execution environment

Read-scoped connectors; object storage; metadata database; image analysis; geospatial enrichment.

## Allowed authority

Start read-only. Add reversible metadata and organization only after policy is set. Destructive deduplication remains a separate permission.

## Boundaries and sensitive data

Preserve original media.
People tags and locations are sensitive; inferred matches need confidence and correction.
Use confirmed person IDs rather than inventing identities.
Do not upload an entire library to model providers by default.
Separate deletion of originals from deletion of indexes.

## Dependencies

Shared identity, job protocol, scoped permissions, audit trail

## Open questions

Where are originals today?
May image content leave my storage boundary?
What retention applies to embeddings and face-derived data?
What can be automatically tagged versus confirmed?

## First useful milestone

Read-only index of a small chosen album, with duplicate suggestions and reversible event tags.

