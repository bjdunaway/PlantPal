# PlantPal Product Requirements Document

## Description

PlantPal is proposed as a personal plant-care application for beginner plant owners, students, and busy people. The product should help users keep track of their plants, understand basic care needs, remember when plants need water, and maintain a record of care.

The intended experience is practical and approachable: users should be able to identify the type of plant, review its basic care information, record care activity, and receive timely watering reminders without requiring advanced gardening knowledge.

## Target users

- Beginner plant owners who need simple, understandable care guidance.
- Students who may have limited time and need reminders.
- Busy people who need a lightweight way to track plant care.

## Scope

The proposed first version includes:

- Adding plants to a personal list.
- Selecting a plant type.
- Viewing basic care information for a plant type.
- Viewing recommended watering frequency.
- Receiving watering reminders.
- Recording that a plant was watered.
- Viewing a plant's watering and care history.

## Exclusions

The following are explicitly outside the proposed scope:

- Photo-based plant identification.
- Disease diagnosis.
- Shopping or purchasing plants and supplies.
- Smart-device integrations.
- Social features.
- Payments.

## Proposed architecture

The proposed technical architecture uses:

- React with Vite for the browser-based client.
- Node.js with Express for the API.
- Supabase for the database and persistence layer.

The client will call the Express API, and the API will manage access to Supabase data. This architecture has not been implemented and must be confirmed during technical planning.

## Constraints and assumptions

- The application is intended for personal use, with each user responsible for their own plants.
- The first version should prioritize the plant list, plant type information, watering records, history, and reminders.
- Care information should remain basic and should not claim to provide diagnosis or expert-level horticultural advice.
- Plant types should have predefined basic care information; user-authored plant-care guides are not in scope.
- Authentication and multi-user access need to be confirmed before implementation.
- The reminder system is part of the proposed scope, but its timing, notification method, and controls remain unresolved.

## Open questions

### Reminder timing and frequency controls

It is unresolved how users will configure reminder timing and frequency. Possible questions include whether reminders are based only on the plant type's recommended frequency, whether users can adjust timing per plant, whether multiple reminders can be active, and what happens after a plant is watered.

### Notification method

It is unresolved which notification method will be used. Browser notifications, email, in-app notifications, mobile push notifications, and another delivery method have not been selected.

### Snoozing reminders

It is unresolved whether users will be able to snooze reminders. If snoozing is supported, the allowed snooze duration, snooze limit, and interaction with the next scheduled reminder have not been defined.

### Plant notes

It is unresolved whether users can add free-form notes to plants. If supported, it is also unresolved what note types or purposes are allowed, how notes are edited or removed, and whether they appear in care history.

### Additional open questions

- What authentication model and privacy controls are required?
- Which plant types and care fields will be included initially?
- What constitutes a care-history event beyond watering?
- How should missed watering reminders be represented?
- Are user-defined custom plant types needed, or is selection limited to a predefined list?
