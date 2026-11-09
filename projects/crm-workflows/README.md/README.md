# CRM workflow reference: lead intake and follow-up

## Status

Reference design only. This document describes a reusable workflow pattern; it is not evidence of a live GoHighLevel deployment.

## Goal

Capture an inbound lead once, preserve its source and consent context, route it to the right owner, and make follow-up status visible.

## Suggested flow

1. Receive a form, import, or approved integration event.
2. Validate required fields and normalize email and phone formats.
3. Check for an existing contact using an agreed stable identifier. Define field-level source-of-truth rules before updating an existing record.
4. Create or update the contact and retain the original acquisition source and consent state.
5. Apply tags, owner, and pipeline stage only from explicit mapping rules. Avoid resetting lifecycle state on unrelated updates.
6. Trigger the next action only when its prerequisites are met; record a clear failure or review path when they are not.
7. Reconcile a sample of source and CRM records after each release.

## Data mapping to define

| Source concept | CRM field | Rule to document |
| --- | --- | --- |
| Email / phone | Contact identifier | Normalization and duplicate policy |
| Source / campaign | Attribution fields | Preserve original source; define update behavior |
| Consent | Consent fields | Store only what is needed; never infer consent |
| Owner / stage | Assignment and pipeline | Map from explicit business rules |

## GoHighLevel implementation notes

Confirm the current supported objects, endpoints, scopes, and workflow triggers in official GoHighLevel documentation before implementation. This reference intentionally does not assume a specific endpoint or payload schema.

## Acceptance checks

- Repeated intake does not create duplicate contacts.
- Missing or malformed identifiers go to a review path.
- An update does not overwrite protected fields without an explicit rule.
- Consent and source information remain traceable.
- Failures can be retried or reconciled without duplicating downstream actions.

All examples should use synthetic data.
