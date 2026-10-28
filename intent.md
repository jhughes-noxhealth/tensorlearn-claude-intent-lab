# Intent: Results-ready notification

Sources: approved PRD N-17 (`inputs/01-approved-prd.md`), discovery notes of 2026-09-20
(`inputs/02-current-meeting.md`). The early request of 2026-08-02
(`inputs/03-superseded-request.md`) is superseded by PRD N-17 and approves nothing here.

## Problem

- **I-1** The fictional clinic receives avoidable calls from patients checking whether their
  results are ready. (PRD)

## Proposed outcome

- **I-2** When a result is ready (as defined in I-3), the patient is notified that an update is
  available and directed to view it in the existing authenticated portal. The notification
  carries no clinical content (see C-2). The channel is not decided (OPEN-1). (PRD)
- **I-3** A result is ready to notify only after a doctor has reviewed **and** released it.
  Completion of the lab upload alone does not make a result ready. No other condition, such as
  an abnormal result, is approved. (PRD; notes, product owner)
- **I-4** Success will be observed as:
  - (a) fewer results-status (status-only) calls, counted separately from clinical questions and
    compared with a measured baseline (PRD; notes, support lead);
  - (b) fewer notification delivery failures (PRD).

  The baseline and any numeric target will be agreed during discovery; none is approved. (PRD)
- **I-5** In scope: use the existing portal result route (PRD; notes, engineering lead);
  duplicate prevention and delivery-failure handling, as set out in C-4. (PRD)

## Affected users and systems

- **I-6** People:
  - Patients: receive the "update available" notification and view the result in the portal.
    (PRD)
  - Doctors: their review and release makes a notification eligible. (PRD)
  - Clinic support staff: handle status calls today and count status-only calls separately from
    clinical questions. (notes, support lead)
  - Product, privacy and clinical owners: decide the open questions below. (PRD)
  - Referring doctors: possibly affected; whether they receive notifications is undecided
    (OPEN-2). (PRD; notes, clinical owner)
- **I-7** Systems: the existing authenticated portal and its existing result route (PRD; notes,
  engineering lead); notification logs (PRD) and operational logs (notes, privacy owner).

## Out of scope

- **I-8** Excluded from this work:
  - Portal redesign, appointment scheduling, clinical interpretation and notifying third
    parties. (PRD) Portal redesign is excluded by the approved PRD; any future redesign would
    need its own approval and is not an open decision of this intent.
  - A new patient dashboard, which is a separate project. (notes, engineering lead)
  - Anything approved only by the superseded early request: notifying as soon as the lab
    uploads, putting the test result in the message, choosing a channel, copying the referring
    doctor, rebuilding the patient dashboard and its call-reduction target. (PRD; notes)

## Constraints

- **C-1** A doctor must review and release the result before any notification is eligible.
  (PRD; notes, product owner)
- **C-2** The message only says that an update is available and directs the patient to the
  existing authenticated portal. No diagnosis, test result, clinical measurement or treatment
  detail goes in messages, notification logs or operational logs. (PRD; notes, privacy owner)
- **C-3** Access to results is authenticated in the existing portal. No attached results and no
  public result link. (PRD)
- **C-4** No duplicate notifications for the same released result version. Delivery failures are
  handled without sending duplicate patient messages. (PRD)

## Open questions and owners

- **OPEN-1** Channel: which channel delivers the notification. Owners: product owner and privacy
  owner, after the consent/delivery review. (PRD; notes, privacy owner)
- **OPEN-2** Referring-doctor notification: whether the referring doctor is an authorized
  recipient. Owners: clinical owner and privacy owner. Not approved by the PRD and not inferred
  from the superseded request. (PRD; notes, clinical owner)

## Decision record

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
