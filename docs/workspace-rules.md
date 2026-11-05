# PlantPal Workspace Rules

These rules establish a shared workflow for contributors. They do not authorize publishing, pushing, merging, or deploying changes without the appropriate review and approval.

## Naming conventions

### Files and folders

- Use lowercase kebab-case for new source files, folders, and documentation files when practical: `plant-list.tsx`, `care-history.md`, `watering-reminders/`.
- Use clear, descriptive names that reflect the file's responsibility.
- Keep configuration and documentation filenames aligned with their tool's expected conventions, such as `README.md` and `package.json`.
- Do not commit generated files or local environment files.

### Code identifiers

- Use descriptive names for variables, functions, components, types, and database entities.
- Follow the conventions of the language and framework being used.
- Prefer names that communicate purpose over abbreviations unless the abbreviation is widely understood in the project.

## Commit messages

Use concise commit messages that explain the purpose of the change. Prefer a consistent format such as:

```text
type: short summary
```

Recommended types include `feat`, `fix`, `docs`, `refactor`, `test`, `chore`, and `style`. Examples:

```text
docs: add product requirements
docs: define workspace contribution rules
feat: add plant list screen
fix: correct watering history date
```

Keep each commit focused. Do not include secrets, credentials, or unrelated changes.

## Feature branches

- Create a dedicated branch for each feature, bug fix, or documentation initiative.
- Branch names should be lowercase kebab-case and identify the work, for example:
  - `feature/plant-list`
  - `feature/watering-reminders`
  - `docs/prd-and-tasks`
- Do not commit feature work directly to the main branch.
- Keep branches reasonably scoped and update them from the agreed base branch according to the team's workflow.

## Pull requests

Every substantial change should be proposed through a pull request. A pull request should include:

- A clear summary of the change.
- The reason for the change.
- Links to relevant tasks or requirements.
- Screenshots or other evidence when the change affects the user interface.
- Notes about testing performed and any known limitations.
- A request for review from the appropriate teammate or reviewer.

Pull requests must not be merged automatically. Changes should remain open for review until a human reviewer approves them.

## Human review

- All proposed code and documentation changes require human review before acceptance.
- Reviewers should check correctness, scope, security, accessibility, and alignment with the approved requirements.
- Product decisions that affect scope, unresolved requirements, or user-facing behavior require explicit human approval.
- Automated checks may support review but do not replace it.
- Do not publish, push, merge, deploy, or make externally visible changes without authorization from the responsible human reviewer.

## Scope and change control

- Keep changes aligned with the Analyst's Level 1 specification and the task plan in `docs/tasks.md`.
- The selected stories `PP-01` through `PP-11` define the approved baseline scope.
- Do not implement rejected features: plant identification, disease diagnosis, shopping or payments, smart devices or sensors, social features, shared plant management, multi-device syncing, public profiles, subscriptions, browsing a large plant catalog, or health guarantees.
- Do not assume unspecified details such as notification technology, snooze duration or limits, schedule-adjustment semantics, watering-record edit rules, note editing/deletion, offline behavior, or authentication requirements.
- Raise scope or requirement questions before making assumptions.
