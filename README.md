# PlantPal

PlantPal is a proposed personal plant-care application for beginner plant owners, students, and busy people. It helps users maintain a list of plants, choose plant types, review basic care information and watering frequency, record watering, view care history, and receive watering reminders.

This repository currently contains project documentation and folder structure only. Application code has not been implemented.

## Proposed architecture

- **`client/`** — React application built with Vite.
- **`api/`** — Node.js and Express API.
- **`supabase/`** — Database schema, migrations, and Supabase configuration.
- **`docs/`** — Product requirements, task plan, and team conventions.

The intended data flow is a Vite client communicating with an Express API, which uses Supabase for persistent data. This architecture is not yet implemented.

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
