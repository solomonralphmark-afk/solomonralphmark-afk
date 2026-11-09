# Synthetic CRM examples

Every example in this folder is fictional and exists only to illustrate field mapping and QA. Do not replace these values with patient, customer, or client records.

## Example lead record

```json
{
  "record_id": "demo-lead-001",
  "first_name": "Casey",
  "last_name": "Sample",
  "email": "casey.sample@example.invalid",
  "phone": "+1-202-555-0147",
  "source": "demo-form",
  "consent_to_marketing": false,
  "lifecycle_stage": "new"
}
```

The .invalid email domain is reserved for examples. The identity is fictional. Treat consent as an explicit input and never infer permission to contact. A production mapping should document field ownership, normalization, retention, and duplicate behavior before syncing data.
