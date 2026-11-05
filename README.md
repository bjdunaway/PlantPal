# PlantPal

PlantPal is a personal plant-care application for beginner plant owners, students, and busy people. The Level 1 scope helps users manage a personal plant list, choose common household plant types, assign plant nicknames, view watering dates, create and adjust watering schedules, receive reminders, mark plants as watered, review watering history, and add plant notes.

This repository currently contains project documentation and folder structure only. Application code has not been implemented.

## Level 1 features

- Add plants from a list of common household plant types.
- Give plants nicknames for easy recognition.
- View all personal plants with last and next watering dates.
- Create watering schedules automatically from plant type.
- Adjust watering schedules based on plant needs.
- Receive reminders when plants need water.
- Snooze reminders and be reminded again later.
- Mark plants as watered with date and time.
- View past watering dates and care history.
- Edit watering records to correct mistakes.
- Add notes about plant condition, care activities, and progress.

## Proposed architecture

- **`client/`** — React application built with Vite.
- **`api/`** — Node.js and Express API.
- **`supabase/`** — Database schema, migrations, and Supabase configuration.
- **`docs/`** — Product requirements, task plan, and team conventions.

The intended data flow is a mobile-first Vite client communicating with an Express API, which uses Supabase for persistent data. The specification targets mobile phones; whether a native mobile wrapper is required remains an open question. This architecture is not yet implemented.

## Prerequisites

The proposed application will require:

- Node.js (LTS recommended)
- npm
- A Supabase project and database credentials

No application package files or installable projects exist yet, so there are currently no setup commands to run.

## Documentation

- [Product requirements](docs/prd.md)
- [Development tasks](docs/tasks.md)
- [Workspace rules](docs/workspace-rules.md)

## Status

- Current stage: project structure and documentation only
- Application screens: not built
- API and database: not implemented
- Features: not implemented
