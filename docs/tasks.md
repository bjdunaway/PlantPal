# PlantPal Development Tasks

This task list implements the Analyst's authoritative Level 1 stories `PP-01` through `PP-11`. The stories are no longer drafts; the rejected stories remain out of scope. Unspecified implementation details are listed as open questions and must not be assumed.

## PP-01 — Add a plant

**Analyst story:** As a plant owner, I want to add a plant from a list of common household plants so that I can keep track of the plants I own.

- **PP-01-T01 — Define the common plant catalog contract.** Create the data contract for the approved list of common household plant types.
  - Acceptance criteria: The contract defines a stable plant-type identifier, display name, recommended watering frequency, and active status for every catalog entry; duplicate identifiers and incomplete entries are rejected.
- **PP-01-T02 — Implement plant-type catalog retrieval in the API.** Create an endpoint that returns the active common household plant types.
  - Acceptance criteria: A client can retrieve only active plant types, each with the contracted fields; the response has a consistent shape and returns a predictable error when the catalog cannot be loaded.
- **PP-01-T03 — Implement plant creation in the API.** Create an endpoint that stores a new plant for the requesting plant owner using a selected plant type.
  - Acceptance criteria: A valid request creates exactly one plant record associated with the owner and plant type, returns the created plant, and rejects unknown plant types or invalid owner references with predictable errors.
- **PP-01-T04 — Implement the add-plant flow in the client.** Create a form that loads plant types from the catalog and submits a new plant.
  - Acceptance criteria: A user can select a plant type from the returned list, submit the form, see a success confirmation, and see clear validation or server errors when creation fails.

## PP-02 — Add a nickname

**Analyst story:** As a plant owner, I want to give each plant a nickname so that I can easily recognize each plant in my list.

- **PP-02-T01 — Define the nickname data contract.** Create validation rules for plant nicknames, including whether a nickname is required, trimming behavior, and maximum length.
  - Acceptance criteria: The contract documents the required/optional status and validation rules, and the implementation rejects empty, whitespace-only, or over-limit nicknames according to those rules.
- **PP-02-T02 — Store and return plant nicknames in the API.** Update plant creation and retrieval responses to include the nickname.
  - Acceptance criteria: A plant created with a valid nickname persists it, plant list and detail responses include it, and invalid nicknames are rejected without creating a plant.
- **PP-02-T03 — Implement nickname entry in the client.** Create a nickname field in the add-plant flow.
  - Acceptance criteria: A user can enter a nickname, receive immediate or submission-time validation feedback, and successfully save the plant with the nickname.
- **PP-02-T04 — Display nicknames as plant labels.** Implement nickname display in the plant list and plant details.
  - Acceptance criteria: The nickname is the primary visible label for each plant, remains visible after reload, and falls back to a clear placeholder only if the approved contract permits a missing nickname.

## PP-03 — View my plants

**Analyst story:** As a plant owner, I want to view all my plants and their watering dates so that I can keep track of their care.

- **PP-03-T01 — Define the plant-list response contract.** Create the response structure for a user's plants, including nickname, plant type, last watering date/time, next watering date/time, and schedule status.
  - Acceptance criteria: The contract defines every displayed field, specifies null behavior for plants with no watering record, and includes enough schedule information to show the next watering date.
- **PP-03-T02 — Implement plant-list retrieval in the API.** Create an endpoint that returns the requesting owner's plants with their watering dates.
  - Acceptance criteria: The endpoint returns only the owner's plants, derives last-watered and next-watering values from stored records and schedules, orders results deterministically, and returns an empty list when the owner has no plants.
- **PP-03-T03 — Implement the plant-list view in the client.** Create a mobile-friendly list that displays each plant's nickname, type, last watered date/time, and next watering date.
  - Acceptance criteria: A user can see every plant in their list, each plant shows its watering dates or a clear empty value, dates are formatted consistently, and loading or API errors are displayed clearly.
- **PP-03-T04 — Test plant-list date accuracy.** Verify that displayed watering dates match stored watering records and schedules.
  - Acceptance criteria: Tests or documented manual checks confirm that last-watered values come from the latest watering record and next-watering values come from the current schedule for each plant.

## PP-04 — Create watering schedule

**Analyst story:** As a beginner plant owner, I want PlantPal to create a watering schedule based on the plant type so that I know when to water my plants.

- **PP-04-T01 — Define the watering-schedule data contract.** Create the schedule fields needed to store a plant's watering frequency/interval and next watering date.
  - Acceptance criteria: The contract defines the plant reference, owner reference, frequency/interval representation, next watering date/time, timezone handling, and validation rules for each field.
- **PP-04-T02 — Store recommended frequencies for plant types.** Update the plant-type catalog so every active type has a recommended watering frequency.
  - Acceptance criteria: Every active plant type has a valid recommended frequency, the frequency is returned by the catalog API, and catalog entries without a frequency cannot be activated.
- **PP-04-T03 — Implement automatic schedule creation in the API.** Create a schedule when a plant is added, using the selected plant type's recommended frequency.
  - Acceptance criteria: Each newly created plant has exactly one active schedule, the first next-watering date is calculated from the documented reference time and plant-type frequency, and schedule creation failures prevent an incomplete plant setup or are retried safely.
- **PP-04-T04 — Implement schedule recalculation logic.** Create a reusable service that calculates the next watering date from a reference timestamp and the plant's current schedule rule.
  - Acceptance criteria: The service returns a deterministic next watering date for a given input, uses the documented timezone rules, and is used consistently by schedule creation, watering updates, and schedule adjustments.

## PP-05 — Adjust watering schedule

**Analyst story:** As a plant owner, I want to adjust a plant's watering schedule so that I can change it based on the plant's needs.

- **PP-05-T01 — Define the schedule-adjustment contract.** Create the request and response structure for changing a plant's watering frequency or schedule values.
  - Acceptance criteria: The contract identifies which schedule fields may be adjusted, validates frequency/date values, and documents whether adjustments affect only the next watering date or the recurring schedule.
- **PP-05-T02 — Implement schedule adjustment in the API.** Create an endpoint that updates an owned plant's watering schedule and recalculates the next watering date.
  - Acceptance criteria: A valid adjustment persists the new schedule values, recalculates the next watering date according to the documented rule, returns the updated schedule, and rejects invalid values or another owner's plant.
- **PP-05-T03 — Implement schedule adjustment in the client.** Create a control that lets a user adjust a plant's watering frequency/schedule.
  - Acceptance criteria: A user can view the current schedule, submit an adjustment, see the updated next watering date after success, and receive clear validation or server errors when the adjustment fails.
- **PP-05-T04 — Test schedule adjustment behavior.** Verify that adjusted schedules produce the expected next watering dates.
  - Acceptance criteria: Tests or documented manual checks confirm that each supported adjustment updates the stored schedule and next watering date without changing the plant's watering history.

## PP-06 — Get watering reminders

**Analyst story:** As a busy plant owner, I want to receive a reminder when a plant needs water so that I do not forget to water it.

- **PP-06-T01 — Define reminder eligibility rules.** Create the rules that determine when a plant is due for a watering reminder.
  - Acceptance criteria: The rules define due time comparison, timezone handling, snooze suppression, notification prerequisites, and behavior for plants with missing or invalid schedules.
- **PP-06-T02 — Implement reminder scheduling in the API.** Create a scheduler or service that identifies due plants and creates reminder records without duplicating active reminders.
  - Acceptance criteria: A due plant produces a reminder record, a non-due or snoozed plant does not, repeated scheduler runs do not create duplicate active reminders, and reminder creation does not alter watering history.
- **PP-06-T03 — Implement reminder delivery.** Create a notification provider interface and integrate the approved delivery method once it is selected.
  - Dependencies: The notification technology is an open question.
  - Acceptance criteria: A due reminder invokes the configured provider, delivery failures are recorded or surfaced predictably, and failed delivery does not mark the plant as watered or change its schedule.
- **PP-06-T04 — Implement the reminders view in the client.** Create a view that shows plants needing water and their reminder status.
  - Acceptance criteria: A user can see which plants are due or reminded, distinguish reminder states using the approved statuses, and see clear empty and error states.

## PP-07 — Snooze reminders

**Analyst story:** As a busy plant owner, I want to snooze a watering reminder so that I can be reminded again later.

- **PP-07-T01 — Define the snooze data contract.** Create the fields needed to postpone a reminder, including the snooze end time and reminder reference.
  - Acceptance criteria: The contract requires a valid future snooze end time or approved duration, associates the snooze with the correct reminder and owner, and rejects invalid or expired snooze values.
- **PP-07-T02 — Implement reminder snoozing in the API.** Create an endpoint that marks a reminder as snoozed and suppresses it until the snooze end time.
  - Acceptance criteria: A successful snooze prevents the reminder from being delivered before the snooze end time, makes the reminder eligible again afterward, returns the updated reminder state, and rejects snoozing another owner's reminder.
- **PP-07-T03 — Implement snooze controls in the client.** Create a snooze action for watering reminders.
  - Acceptance criteria: A user can snooze a due reminder, see confirmation of the snooze, and see the next eligible reminder time when the approved snooze duration is known.
- **PP-07-T04 — Apply approved snooze configuration.** Implement the approved snooze duration options and limits once they are specified.
  - Dependencies: Snooze duration, preset options, and snooze limits are open questions.
  - Acceptance criteria: The client and API enforce only the approved snooze durations and limits, reject unsupported values, and preserve the underlying watering schedule unless the Analyst specifies otherwise.

## PP-08 — Mark plant as watered

**Analyst story:** As a plant owner, I want to mark a plant as watered so that PlantPal records the date and time and sets the next watering date.

- **PP-08-T01 — Define the watering-record data contract.** Create the fields required to record that a plant was watered.
  - Acceptance criteria: The contract defines the plant reference, owner reference, watering date/time, record timestamp, and validation rules; invalid or missing required values are rejected.
- **PP-08-T02 — Implement mark-as-watered in the API.** Create an endpoint that records the current watering date/time and updates the plant's next watering date.
  - Acceptance criteria: A valid request creates one watering record with the correct plant and owner, stores the watering timestamp, recalculates the next watering date from the current schedule rule, and returns the created record and updated schedule.
- **PP-08-T03 — Implement the mark-as-watered action in the client.** Create a user action that marks the selected plant as watered.
  - Acceptance criteria: A user can trigger the action for an owned plant, see a success confirmation with the new next watering date, and see a clear error if recording fails.
- **PP-08-T04 — Test watering-date updates.** Verify that marking a plant as watered updates both history and the next watering date.
  - Acceptance criteria: Tests or documented manual checks confirm that the watering record appears in history, the stored timestamp matches the action time according to the documented timezone rules, and the next watering date advances correctly.

## PP-09 — View care history

**Analyst story:** As a plant owner, I want to view a plant's watering history so that I know when it was last watered.

- **PP-09-T01 — Define the watering-history response contract.** Create the response structure for a plant's past watering records.
  - Acceptance criteria: The contract defines each history entry's date/time and record identifier, specifies chronological ordering, and defines empty-history behavior.
- **PP-09-T02 — Implement watering-history retrieval in the API.** Create an endpoint that returns watering records for an owned plant.
  - Acceptance criteria: The endpoint returns only records belonging to the requested plant, orders them by watering time, includes edited-record values accurately, and returns an empty list when no records exist.
- **PP-09-T03 — Implement the watering-history view in the client.** Create a history screen or section that lists past watering dates and times.
  - Acceptance criteria: A user can open a plant's history, see each watering event's date and time in the documented order, and see a clear empty state when no watering has been recorded.
- **PP-09-T04 — Test watering-history access and ordering.** Verify that history is accurate and owner-scoped.
  - Acceptance criteria: Tests or documented manual checks confirm that records appear once, timestamps are displayed correctly, and another owner's plant history cannot be viewed.

## PP-10 — Edit watering record

**Analyst story:** As a plant owner, I want to edit a watering record so that I can correct information if I forgot to record a watering.

- **PP-10-T01 — Define the watering-record edit contract.** Create the rules for which watering-record fields may be corrected and how edited values are validated.
  - Acceptance criteria: The contract identifies the editable fields, validation rules, ownership requirements, and whether edits create a revision history or overwrite the record.
- **PP-10-T02 — Implement watering-record editing in the API.** Create an endpoint that updates an owned watering record.
  - Acceptance criteria: A valid edit persists the corrected values, returns the updated record, rejects invalid values or another owner's record, and preserves the record's association with the correct plant.
- **PP-10-T03 — Implement watering-record editing in the client.** Create an edit form for an existing watering record.
  - Acceptance criteria: A user can select a watering record, view its current values, submit corrections, see the updated record in history, and receive clear validation or server errors when editing fails.
- **PP-10-T04 — Test watering-record corrections.** Verify that edited records are reflected in history and related views.
  - Acceptance criteria: Tests or documented manual checks confirm that corrected values replace the prior displayed values, invalid edits are rejected, and the plant's other watering records remain unchanged.

## PP-11 — Add plant notes

**Analyst story:** As a plant owner, I want to add notes about a plant's condition and care so that I can keep track of its progress.

- **PP-11-T01 — Define the plant-note data contract.** Create the fields required for a note about a plant's condition, care, or progress.
  - Acceptance criteria: The contract defines the plant reference, owner reference, note content, creation timestamp, and validation rules; empty or invalid notes are rejected.
- **PP-11-T02 — Implement plant-note creation in the API.** Create an endpoint that stores a new note for an owned plant.
  - Acceptance criteria: A valid request creates one note associated with the correct plant and owner, returns the created note, and rejects invalid content or another owner's plant.
- **PP-11-T03 — Implement plant-note retrieval in the API.** Create an endpoint that returns notes for an owned plant.
  - Acceptance criteria: The endpoint returns only notes belonging to the requested plant, orders them consistently, includes the information needed to understand plant progress, and returns an empty list when no notes exist.
- **PP-11-T04 — Implement plant notes in the client.** Create a note-entry form and display area on the plant detail view.
  - Acceptance criteria: A user can write and submit a note about plant condition or care, see the note after saving, see validation or server errors when submission fails, and view previously saved notes for the plant.
- **PP-11-T05 — Test plant-note persistence and access.** Verify that notes are stored and displayed correctly.
  - Acceptance criteria: Tests or documented manual checks confirm that notes persist after reload, appear only for the owning user's plant, and reject empty or invalid content.

## Open questions and dependencies

The following details remain unspecified and must be resolved before the affected implementation is finalized:

- Exact common household plant catalog and recommended watering frequencies.
- Whether a separate basic care-information display is required beyond suggested watering frequency.
- Watering frequency units, timezone rules, and first-schedule calculation details.
- Whether schedule adjustment changes frequency, next watering date, or both.
- Notification technology and delivery provider.
- Reminder timing rules beyond the next watering date.
- Snooze durations, preset options, limits, and whether snoozing changes the schedule.
- Editable watering-record fields and whether edits recalculate the next watering date.
- Whether edited watering records display a correction indicator.
- Whether watering history needs filtering, searching, or pagination.
- Whether plant notes can be edited or deleted after creation.
- Authentication/account model, privacy requirements, offline behavior, and native-mobile requirements.
