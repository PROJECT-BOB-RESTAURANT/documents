# Project Definition

## Project Name
BOB Restaurant Management System

## Purpose
Provide a web platform for day-to-day restaurant operations where staff can:

- manage restaurants, floors, and table layouts,
- create and manage reservations,
- run table service and kitchen ticket workflows,
- maintain opening hours and menu catalog data,
- manage users and worker assignments.

The current product focus is operational consistency across manager, waiter, kitchen, and admin workflows rather than advanced reporting or external integrations.

## Scope

### In Scope
- Multi-restaurant and multi-floor management
- Visual floor editor with known floor objects (tables, doors, stairs, toilets, kitchen blocks, etc.)
- Reservation creation, update, deletion, and timeline/statistics views
- Waiter workflow for table orders, order lines, and local payment logging (single and split)
- Kitchen queue workflow with order-line lifecycle states
- User and worker management (ADMIN, MANAGER, STAFF) with assignment to restaurants
- Menu folder/item management and price updates
- Weekly opening hours and date-specific opening overrides
- Persistent backend API + relational database + migration-based seed data

### Out of Scope (Current Phase)
- Full payment gateway integrations (card processors, terminal SDKs)
- Advanced BI beyond the implemented reservation/queue/revenue summary views
- Native mobile apps
- Customer self-service reservation links/portals (edit/cancel via tokenized links)
- Stock/allergy/station-based kitchen planning features

## Objectives (Measurable Targets)

1. Migration Alignment
- Target: 100% of schema changes are delivered via Flyway and reflected in docs.
- Measure: every merged migration has corresponding documentation update.

2. Reservation Validity
- Target: 100% of accepted reservations pass interval and opening-hours validation.
- Measure: backend acceptance path only persists valid reservation windows.

3. Order-Line Lifecycle Integrity
- Target: 100% of persisted order-line statuses are in the supported lifecycle set.
- Measure: database check constraint and API validation.

4. Core CRUD Reliability
- Target: no known blocker defects in CRUD flows for restaurants, floors, objects, menu, workers, and opening-hours overrides.
- Measure: regression checks on primary management screens and linked APIs.

5. Authorization Baseline
- Target: authenticated sessions are required for protected APIs; roles map to implemented UI areas.
- Measure: login/token flow and role-based app navigation work in QA/demo environments.

## Success Criteria Summary
The project is considered successful for Phase 1 if:
- Core workflows (floor editing, reservations, waiter ordering, kitchen queue, opening-hours management) are stable and usable end to end.
- Admin and manager workflows (user/worker/menu/restaurant management) are functional without manual database intervention.
- Schema migrations remain reproducible, and documentation stays aligned with the actual persisted model.
