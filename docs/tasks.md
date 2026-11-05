# PlantPal Development Tasks

This task list describes concrete development work for the baseline features. The stories remain **drafts pending Analyst final specification** and must not be treated as approved requirements. No features are implemented by this documentation change.

## Baseline stories and tasks

### PP-01 — Add a plant to a personal list

**Story (draft pending Analyst confirmation):** As a plant owner, I want to add a plant to my personal list so that I can track its care.

- **PP-01-T01 — Define the plant creation data contract.** Create the minimum validated fields and relationships required to create a plant.
  - Acceptance criteria: The contract identifies required and optional fields, enforces valid data types and values, and rejects incomplete or invalid plant creation requests.
- **PP-01-T02 — Implement plant creation in the API.** Store a valid plant and associate it with its approved owner reference and selected plant type.
  - Acceptance criteria: A successful request creates one plant record, returns the created plant, persists the owner and plant type relationships, and returns a predictable error for invalid requests.
- **PP-01-T03 — Implement the plant creation form in the client.** Create a form that collects the approved plant details and submits them to the API.
  - Acceptance criteria: A user can enter the required information, submit the form, see a success state, and see a clear validation or server error when creation fails.
- **PP-01-T04 — Implement personal plant-list retrieval.** Store and display the current plant owner's plants after they are created.
  - Acceptance criteria: The API returns only plants belonging to the requesting plant owner's reference, and the client displays each returned plant with enough information to identify it.

### PP-02 — Select a plant type

**Story (draft pending Analyst confirmation):** As a plant owner, I want to select a plant type so that I can see relevant basic care information.

- **PP-02-T01 — Define supported plant types and their data.** Create the initial plant-type catalog and the basic care fields associated with each type.
  - Acceptance criteria: Every supported type has a stable identifier, display name, and complete approved care information, including watering frequency.
- **PP-02-T02 — Store plant types and plant-type relationships.** Implement persistent storage for plant types and the relationship between a plant and its type.
  - Acceptance criteria: A created plant references exactly one valid plant type, and the selected type can be retrieved consistently from storage.
- **PP-02-T03 — Implement plant-type selection in the client.** Create a selection control that lets a user choose from supported plant types.
  - Acceptance criteria: A user can open the selector, view supported plant types, select one type, and submit that selection with a new plant.
- **PP-02-T04 — Display the selected plant type.** Implement display of a plant's selected type in the plant list and plant details.
  - Acceptance criteria: The selected type's display name is visible for each plant and remains correct after the plant is retrieved again.

### PP-03 — View basic care information and watering frequency

**Story (draft pending Analyst confirmation):** As a plant owner, I want to view basic care information and watering frequency so that I know how to care for my plant.

- **PP-03-T01 — Define the care-information response.** Create the API response structure for a plant's basic care information and recommended watering frequency.
  - Acceptance criteria: The response includes all approved care fields, identifies the plant and plant type, and uses consistent units and labels for watering frequency.
- **PP-03-T02 — Implement care-information retrieval in the API.** Retrieve and return the care information associated with a plant's selected type.
  - Acceptance criteria: A request for a plant owned by the requesting plant owner returns its current plant-type care information, while a missing plant or another owner's plant returns a predictable error.
- **PP-03-T03 — Implement care-information display in the client.** Create a plant details view that presents basic care information and watering frequency.
  - Acceptance criteria: A user can select a plant and see the approved care fields and recommended watering frequency in a readable layout.
- **PP-03-T04 — Test care-information accuracy and presentation.** Verify that displayed care information matches the selected plant type's stored data.
  - Acceptance criteria: Automated or documented manual checks confirm that each supported plant type displays its own approved watering frequency and care fields.

### PP-04 — Receive watering reminders

**Story (draft pending Analyst confirmation):** As a busy person, I want to receive watering reminders so that I do not forget to care for my plants.

The following tasks are blocked by unresolved product decisions. They must not be implemented until the dependencies are approved.

- **PP-04-T01 — Define reminder scheduling rules.** Create scheduling rules only after reminder timing and frequency controls are approved.
  - Dependencies: Reminder timing and frequency controls are unresolved.
  - Acceptance criteria: The approved rules define when reminders are created, how often they repeat, and how watering or plant changes affect the schedule.
- **PP-04-T02 — Implement reminder delivery.** Create and send reminders only after the notification method is approved.
  - Dependencies: Notification method is unresolved.
  - Acceptance criteria: The approved delivery channel receives a reminder for each due plant, and delivery failures are handled predictably.
- **PP-04-T03 — Implement reminder state in the client.** Display reminder status only after the notification and scheduling rules are approved.
  - Dependencies: Reminder timing, notification method, and snoozing behavior are unresolved.
  - Acceptance criteria: A user can distinguish pending, delivered, and completed reminders using the approved states and see clear errors when reminder status cannot be loaded.

### PP-05 — Record watering

**Story (draft pending Analyst confirmation):** As a plant owner, I want to record when I water a plant so that I can keep a care history.

- **PP-05-T01 — Define the watering-record data contract.** Create the validated fields required to associate a watering event with a plant and plant owner.
  - Acceptance criteria: The contract defines the watering timestamp, plant reference, and any approved additional fields, and rejects invalid or incomplete records.
- **PP-05-T02 — Implement watering-record creation in the API.** Store a watering event for a plant owned by the requesting plant owner.
  - Acceptance criteria: A valid request creates one watering record, associates it with the correct plant and owner reference, and returns the created record or a predictable validation error.
- **PP-05-T03 — Implement the watering action in the client.** Create a plant-owner action that records watering for the selected plant.
  - Acceptance criteria: A user can trigger the action for a visible plant, receive confirmation after success, and see a clear error when recording fails.
- **PP-05-T04 — Connect watering records to reminder state.** Update the approved reminder or next-watering state after a watering record is stored.
  - Dependencies: Reminder timing, frequency controls, and snoozing behavior are unresolved.
  - Acceptance criteria: Once approved, a successful watering record updates the relevant schedule according to the documented rules and does not create duplicate watering records.

### PP-06 — View watering history

**Story (draft pending Analyst confirmation):** As a plant owner, I want to view a plant's watering history so that I can understand its past care.

- **PP-06-T01 — Implement watering-history retrieval in the API.** Retrieve watering records for a plant owned by the requesting plant owner in chronological order.
  - Acceptance criteria: The API returns only records belonging to the requested plant, orders them by watering time, and returns a predictable empty result or error as appropriate.
- **PP-06-T02 — Implement watering-history display in the client.** Create a history view that lists a plant's watering events.
  - Acceptance criteria: A user can open a plant's history and see each watering event's approved details in a clear chronological list.
- **PP-06-T03 — Test watering-history integrity.** Verify that created watering records appear in history and plants belonging to other owners cannot be viewed.
  - Acceptance criteria: Tests or documented manual checks confirm that valid records appear once, timestamps are displayed correctly, and access is limited to the plant owner.

## Unconfirmed scope

The following work is **not approved** and must not be treated as part of the baseline. It requires explicit product approval and a separate specification before development.

- Editing plant details.
- Deleting plants.
- Account creation, login, logout, or other authentication flows.
- Filtering, searching, or paginating care history.
- Adding, editing, deleting, or displaying plant notes.
- Snoozing reminders.
- Configurable reminder timing or frequency controls beyond the approved baseline.
- Notification delivery through an unapproved method.

## Reminder dependencies

The following decisions remain unresolved and block complete reminder implementation:

- Reminder timing and frequency controls.
- Notification method.
- Snoozing reminders.
- How watering affects the next reminder.
- Plant notes, if they are later approved as part of care history.
