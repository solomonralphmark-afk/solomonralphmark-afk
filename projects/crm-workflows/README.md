# CRM workflow reference: lead intake and follow-up

## Status

Reference design only. This describes a reusable pattern, not a live GoHighLevel deployment.

## Suggested flow

1. Receive an inbound form, import, or approved integration event.
2. Validate required fields and normalize email and phone formats.
3. Find a possible existing contact using an agreed stable identifier. Define source-of-truth rules before changing existing fields.
4. Create or update the contact while preserving source and explicit consent state.
5. Apply owner, tags, and pipeline stage from documented mapping rules; do not reset lifecycle state on unrelated updates.
6. Trigger the next action only when prerequisites are satisfied. Route missing or conflicting data for review.
7. Reconcile sample source and CRM records after changes.

## Mapping decisions

| Source concept | CRM field | Rule |
| --- | --- | --- |
| Email / phone | Contact identity | Normalization and duplicate policy |
| Source / campaign | Attribution | Preserve original source; define update behavior |
| Consent | Consent fields | Never infer consent |
| Owner / stage | Assignment / pipeline | Explicit business rule |

## GoHighLevel verification

Check current official GoHighLevel documentation for supported objects, endpoints, scopes, triggers, and payloads before implementing. This reference does not assume API behavior.

## Acceptance checks

- Repeated intake does not create duplicates.
- Missing or malformed identifiers go to review.
- Protected fields are not overwritten without an explicit rule.
- Failures can be retried or reconciled without repeating side effects.
- Examples use synthetic data only.
