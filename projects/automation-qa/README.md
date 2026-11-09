# Automation QA reference

## Status

Reusable test design for CRM and workflow automations. Use synthetic records until an approved test environment and data-processing arrangement are in place.

## Scenario checklist

| Scenario | Expected result |
| --- | --- |
| Valid new lead | One contact is created with mapped source and owner |
| Same event delivered twice | No duplicate contact or repeated downstream action |
| Missing or malformed identifier | Safe rejection or a review queue; no guessed match |
| Authentication failure | Request is rejected and secrets are not logged |
| API rate limit / timeout | Bounded retry with backoff, then recoverable failure state |
| Conflicting field update | The agreed source-of-truth rule wins, or the item is quarantined |
| Partial workflow completion | Retry resumes safely without repeating completed side effects |
| Invalid consent state | No consent-dependent message is sent |
| Recovery / replay | Reconciliation restores expected state without duplicates |

## Release evidence

For each change, record the requirement, test data identifier (synthetic), expected and actual result, relevant safe log/correlation ID, and unresolved issue. Avoid screenshots or logs containing real contact data or credentials.

## GoHighLevel note

Map each scenario to the actual configured workflow and currently supported API behavior only after checking official documentation and a non-production account.
