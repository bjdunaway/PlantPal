# PlantPal Product Requirements Document

## Source and status

This document is aligned to the Analyst's Level 1 Specification and User Stories documents. The selected stories are authoritative for the Level 1 baseline and are numbered `PP-01` through `PP-11`. The rejected stories remain out of scope.

PlantPal is a personal plant-care application for beginner plant owners, students, and busy people who want to keep houseplants healthy without memorizing every watering date. The Level 1 focus is simple plant management, watering schedules, reminders, watering records, and plant notes.

## Target users

### Maya Chen — student / beginner plant owner

Maya is a 20-year-old college student who lives in a dorm and has three desk plants. She wants to keep her plants alive during busy periods such as midterms and finals and avoid overwatering. She needs quick plant setup, simple care information, and reminders that help her remember when each plant needs water.

### Robert Alvarez — plant collector

Robert is a 58-year-old nurse who works night shifts, gardens on weekends, and owns about 15 houseplants. He wants to track plants with different watering needs and know which ones he have already watered. He needs an organized plant list and an easy-to-check last-watered record.

### Other users

Other potential users include beginner plant owners and busy people who like houseplants but do not want to memorize separate care schedules. The main audience remains individual plant owners; shared-caregiver and social roles are not part of the initial scope.

## Usage context

- PlantPal is primarily intended for mobile phones so users can receive watering notifications and check their plants through the application.
- Users may use PlantPal at home, in a dorm room, at school, or while away from their plants.
- Users need notifications enabled on their phones to receive watering reminders.
- An internet connection may be needed for some application features, but offline functionality has not been confirmed.

## Scope

The Level 1 scope centers on five core activities:

1. Managing a personal plant list.
2. Creating watering schedules.
3. Receiving watering reminders.
4. Recording watering and care history.
5. Adding notes about plant conditions, care activities, and progress.

The Analyst's project summary also mentions viewing basic plant-care information and suggested watering frequency. Suggested watering frequency is required for schedules; whether a separate general care-information display is required is an open question.

### Selected user stories

| ID | Story | Scope label |
| --- | --- | --- |
| PP-01 | As a plant owner, I want to add a plant from a list of common household plants so that I can keep track of the plants I own. | Add a plant |
| PP-02 | As a plant owner, I want to give each plant a nickname so that I can easily recognize each plant in my list. | Add a nickname |
| PP-03 | As a plant owner, I want to view all my plants and their watering dates so that I can keep track of their care. | View my plants |
| PP-04 | As a beginner plant owner, I want PlantPal to create a watering schedule based on the plant type so that I know when to water my plants. | Create watering schedule |
| PP-05 | As a plant owner, I want to adjust a plant's watering schedule so that I can change it based on the plant's needs. | Adjust watering schedule |
| PP-06 | As a busy plant owner, I want to receive a reminder when a plant needs water so that I do not forget to water it. | Get watering reminders |
| PP-07 | As a busy plant owner, I want to snooze a watering reminder so that I can be reminded again later. | Snooze reminders |
| PP-08 | As a plant owner, I want to mark a plant as watered so that PlantPal records the date and time and sets the next watering date. | Mark plant as watered |
| PP-09 | As a plant owner, I want to view a plant's watering history so that I know when it was last watered. | View care history |
| PP-10 | As a plant owner, I want to edit a watering record so that I can correct information if I forgot to record a watering. | Edit watering record |
| PP-11 | As a plant owner, I want to add notes about a plant's condition and care so that I can keep track of its progress. | Add plant notes |

### Scope details from the Analyst specification

- Users choose a plant type from a list rather than browsing an unlimited plant catalog.
- Users can create a plant nickname and view their plant list.
- Watering schedules are created automatically by plant type, can have watering frequency adjusted, and should expose the next watering date.
- Reminder flows should identify plants that need water, deliver a notification, and allow reminders to be snoozed/postponed and created again later.
- Watering care should record the watering date and time, show past watering dates/history, and allow a watering record to be corrected.
- Plant notes should let users record information about plant condition, care activities, and progress.

## Exclusions

The following rejected stories and related capabilities are outside the Level 1 scope:

- Photo-based plant identification.
- Identifying plant diseases from pictures.
- Detailed expert plant diagnosis.
- Guaranteeing that plants stay healthy.
- Purchasing plants, fertilizer, plant supplies, or other shopping features.
- Subscriptions, premium accounts, and payment processing.
- Connecting to smart watering devices, soil moisture sensors, or equipment-control systems.
- Sharing plant pictures, following other plant owners, commenting on plants, or creating public profiles.
- Sharing a plant list with family members or other shared plant-management workflows.
- Syncing plant information across multiple devices.
- Browsing thousands of indoor and outdoor plants beyond the approved common-household-plant list.

## Proposed architecture

The proposed technical architecture uses:

- React with Vite for the client.
- Node.js with Express for the API.
- Supabase for the database and persistence layer.

The client will call the Express API, and the API will manage access to Supabase data. The specification targets mobile phones; the React/Vite client should be mobile-first, but whether a native mobile wrapper is required remains an open question.

This architecture has not been implemented.

## Constraints and assumptions

- The application is intended for individual plant owners managing their own plants.
- Shared-caregiver, family-sharing, and social roles are excluded from the initial scope.
- The plant catalog should be a short list of common household plants, not a comprehensive botanical database.
- Watering schedules must be based on plant type but may need user adjustment.
- Reminder delivery requires users to have notifications enabled, but the notification technology is not specified.
- Care guidance should remain beginner-friendly and must not claim to diagnose disease or guarantee plant health.
- Authentication, account management, and privacy requirements are not fully specified.

## Open questions

### Plant catalog and care information

- Which common household plant types will be included in the initial catalog?
- What basic care fields, if any, must be displayed for each plant type?
- What watering frequency unit and values will each plant type use?
- Are custom plant types allowed, or must users choose only from the approved list?

### Watering schedules

- How should watering frequency be represented and adjusted?
- What timezone should be used for schedule calculations and display?
- When should the first next-watering date be calculated after a plant is added?
- Does adjusting a schedule change only the next watering date, the recurring frequency, or both?
- How should daylight-saving time and date boundaries be handled?

### Reminders and snoozing

- Which notification technology will be used, such as browser push, email, in-app notification, or mobile push?
- What reminder timing rules apply beyond the next watering date?
- What snooze durations or preset options are allowed?
- Is there a limit on how many times a reminder can be snoozed?
- Does snoozing change the underlying watering schedule or only postpone the notification?
- How should notification permission failures be handled?

### Watering records and history

- Which fields on a watering record may be edited?
- Can users enter a watering date/time directly, or must they edit an existing record to correct it?
- Should editing a watering record recalculate the next watering date, and under what rules?
- Should watering history be filtered, searched, or paginated?
- Should edited watering records display an indication that they were corrected?

### Plant notes

- Are plant notes editable or deletable after creation?
- Should notes appear only on the plant detail view, in watering history, or in a combined care timeline?
- What validation limits apply to note content?
- Can notes be attached to specific care activities or only to the plant generally?

### Accounts, privacy, and platform

- What authentication or account model is required for personal plant lists?
- What privacy and data-retention expectations apply?
- Is offline functionality required?
- Is a native mobile application required, or is a mobile-first responsive web client sufficient?
