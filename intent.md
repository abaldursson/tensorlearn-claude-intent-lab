# Intent: results-ready notification

Sources: PRD N-17 (approved for discovery and specification, 2026-09-18) and the 2026-09-20 discovery notes. The 2026-08-02 early request is superseded and approves nothing.

## Problem

The fictional clinic gets avoidable calls from patients asking whether their results are ready.

## Proposed outcome

- I-1: Once a doctor has reviewed and released a result, the patient is told an update is available and is pointed to the existing authenticated portal.
- I-2: A finished lab upload alone never makes a result eligible.
- I-3: The same released result version never triggers a duplicate notification, even after a delivery failure.

Success is observed by counting status-only calls (kept separate from clinical questions) against a measured baseline, and by counting delivery failures. The baseline and any numeric target are not yet approved and are to be agreed in discovery, so none is stated here.

## Affected users and systems

Patients (notified, then sign in), doctors (review and release), support staff (take and count the calls), and the existing portal result route, which is reused as it is.

## Out of scope

- Third-party notifications are not approved. Whether the referring doctor is notified is undecided (OPEN-2).
- Portal redesign, a new patient dashboard, appointment scheduling and clinical interpretation.
- Anything approved only by the superseded request: sending on upload, results in an SMS, copying the referring doctor, rebuilding the dashboard, and the 90% target in one week.

## Constraints

- C-1: Doctor review and release come before any notification.
- C-2: The message says only that an update is available. No diagnosis, test result, clinical measurement or treatment detail appears in it or in logs.
- C-3: Access stays authenticated in the portal: no attached results, no public result link.
- C-4: No duplicate patient messages, including when handling delivery failures.

## Open questions

- OPEN-1: Channel (SMS, email or portal push), pending consent and delivery review. Owners: product and privacy.
- OPEN-2: Whether the referring doctor is notified, pending recipient authorization. Owners: clinical and privacy.

```json
{
  "notifyWhen": ["doctor-reviewed", "released"],
  "messageMayInclude": ["update-available"],
  "inScope": ["existing-portal-route", "duplicate-prevention", "delivery-failure-handling"],
  "openDecisions": [
    {"topic": "channel", "owners": ["product", "privacy"]},
    {"topic": "referring-doctor-notification", "owners": ["clinical", "privacy"]}
  ],
  "successMeasures": ["status-only-calls", "delivery-failures"],
  "numericTarget": null
}
```
