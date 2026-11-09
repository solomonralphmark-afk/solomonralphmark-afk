# Webhook integration reference

## Status

Reference design only. Confirm current provider behavior and supported authentication before implementation.

## Processing outline

1. Accept only the expected content type and validate the event shape before doing work.
2. Verify a provider signature or authentication token when the provider supports it. Compare signatures safely and do not log secrets or full sensitive payloads.
3. Require a stable event identifier when available. Store processed identifiers so retries do not repeat side effects.
4. Persist accepted events before returning success when the architecture requires durable processing.
5. Apply field mapping and source-of-truth rules; reject or quarantine events that conflict with protected CRM state.
6. Return the documented response code promptly. Retry transient failures with bounded backoff; route exhausted failures for review or replay.
7. Record a correlation ID, event type, result, and safe error summary for monitoring.

## Failure and recovery cases

- Invalid signature or malformed payload: reject and record a safe diagnostic.
- Duplicate delivery: acknowledge according to the provider contract without repeating the CRM change.
- CRM timeout or rate limit: retry within policy, then queue for recovery.
- Mapping conflict: quarantine for review instead of guessing which value wins.
- Partial completion: use idempotent steps or reconciliation to resume safely.

## Provider verification

Before shipping, consult the official GoHighLevel documentation for the selected webhook/event, signing method, delivery guarantees, retry schedule, payload schema, and rate limits. This reference does not assume these details.

## Privacy

Use synthetic payloads in public examples. Keep tokens, contact details, and client data out of logs and repository history.
