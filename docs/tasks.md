# PlantPal Development Tasks

This task list organizes proposed implementation work by feature. Acceptance criteria describe expected outcomes but are not implementation commitments. No features are implemented in this repository stage.

## User stories

The following user stories are **drafts pending Analyst confirmation**. They should not be treated as approved requirements.

- As a plant owner, I want to add a plant to my personal list so that I can track its care.
- As a plant owner, I want to select a plant type so that I can see relevant basic care information.
- As a plant owner, I want to view recommended watering frequency so that I know when to check my plant.
- As a plant owner, I want to record when I water a plant so that I can keep a care history.
- As a plant owner, I want to view a plant's care history so that I can understand past care.
- As a busy person, I want to receive watering reminders so that I do not forget to care for my plants.

## Feature tasks

### Personal plant list

- **Task:** Define the data and interaction needed to add a plant to a user's personal list.
  - Acceptance criteria: A user can create a plant entry with the minimum approved fields, see it in their personal list, and identify it separately from other users' plants.
- **Task:** Define how a user edits or removes a plant entry.
  - Acceptance criteria: An approved edit or removal action changes only the intended plant entry and preserves the expected access controls.
- **Task:** Define how users access only their own plant list.
  - Acceptance criteria: Authentication and authorization rules prevent one user from viewing or modifying another user's plants.

### Plant type selection

- **Task:** Define the available plant types and required selection behavior.
  - Acceptance criteria: A user can select a valid plant type from the approved list, and the selected type is stored with the plant.
- **Task:** Define how basic care information is associated with a plant type.
  - Acceptance criteria: Each supported plant type has approved, consistently structured basic care information.

### Basic care information and watering frequency

- **Task:** Define the fields included in basic plant care information.
  - Acceptance criteria: Users can view the approved care fields for their selected plant type without receiving diagnostic claims.
- **Task:** Define how watering frequency is displayed.
  - Acceptance criteria: A user can view the recommended watering frequency associated with the plant type and understand how it applies to the plant.

### Watering reminders

- **Task:** Confirm reminder timing and frequency controls before designing reminder behavior.
  - Acceptance criteria: The approved rules define whether timing is based on plant type, user settings, per-plant settings, or another source.
- **Task:** Confirm the notification method before implementation.
  - Acceptance criteria: The approved rules identify the supported delivery channel and user expectations for notifications.
- **Task:** Define reminder scheduling and notification behavior after approval.
  - Acceptance criteria: Approved scenarios describe when reminders are created, sent, repeated, and stopped.
- **Task:** Resolve snoozing behavior before implementation.
  - Acceptance criteria: The approved rules state whether snoozing is supported, its duration and limits, and its effect on the next reminder.

### Watering records

- **Task:** Define the minimum information captured when a user records watering.
  - Acceptance criteria: A user can record watering for a selected plant and the record is associated with that plant and user.
- **Task:** Define how a successful watering record affects care state.
  - Acceptance criteria: Approved behavior states whether and how watering updates the next watering reminder or schedule.

### Care history

- **Task:** Define the events included in a plant's care history.
  - Acceptance criteria: Users can view approved care events for a plant in a clear chronological order.
- **Task:** Define how history is filtered or paginated if needed.
  - Acceptance criteria: Users can find relevant past care events without losing access to older records.

### Plant notes

- **Task:** Resolve whether plant notes are in scope before implementation.
  - Acceptance criteria: Product approval either includes or excludes free-form plant notes and defines any constraints.
- **Task:** If approved, define note creation, editing, display, and removal behavior.
  - Acceptance criteria: Users can manage only their own notes and see them in the approved location in the product.

## Cross-cutting tasks

- **Task:** Confirm authentication and authorization requirements.
  - Acceptance criteria: The team agrees on how users are identified and how access to plants, records, and reminders is protected.
- **Task:** Define validation and error-handling expectations for client and API work.
  - Acceptance criteria: Invalid plant data and failed requests have predictable, user-friendly handling.
- **Task:** Define Supabase schema and migration approach before database implementation.
  - Acceptance criteria: Approved entities, relationships, constraints, and migration ownership are documented.
- **Task:** Define non-functional expectations for responsiveness and accessibility.
  - Acceptance criteria: The team records minimum usability expectations for the first version.
