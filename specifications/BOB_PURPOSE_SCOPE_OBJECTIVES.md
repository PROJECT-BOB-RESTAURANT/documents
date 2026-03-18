# Project Definition

## Project Name
BOB Restaurant Operations Platform

## Purpose
Build a single platform that helps restaurants manage floor layouts, reservations, table service, menu operations, and staff workflows in one place.

The platform reduces manual coordination between front-of-house and back-of-house by providing a shared real-time operational view.

## Scope

### In Scope
- Multi-restaurant and multi-floor management
- Visual floor editor with known floor objects (tables, doors, stairs, toilets, kitchen blocks, etc.)
- Reservation management (guest-facing and staff-facing)
- Waiter workflow for table orders and order-line updates
- Basic worker and role management (manager, waiter, chef)
- Menu/category management and price updates
- Opening hours management
- Persistent backend API + relational database + migration-based seed data

### Out of Scope (Current Phase)
- Full payment gateway integrations (card processors, terminal SDKs)
- Advanced BI dashboards beyond core operational metrics
- Native mobile apps
- Multi-language localization at enterprise scale

## Objectives (Measurable Targets)

1. Reservation Completion Rate
- Target: >= 90% of initiated reservation flows are completed successfully.
- Measure: completed reservations / started reservation sessions.
- Timeframe: within 8 weeks after production launch.

2. Reservation Error Rate
- Target: < 2% backend/API error responses on reservation endpoints.
- Measure: count of 4xx/5xx reservation API responses / total reservation requests.
- Timeframe: sustained for 4 consecutive weeks post-launch.

3. Waiter Order Entry Speed
- Target: median time <= 45 seconds from table open to first submitted order line.
- Measure: event timestamps in waiter workflow.
- Timeframe: within 10 weeks post-launch.

4. Floor Layout Save Reliability
- Target: >= 99% successful floor-layout save operations.
- Measure: successful save responses / all save attempts.
- Timeframe: sustained for 4 consecutive weeks.

5. Data Consistency for Floor Objects
- Target: 0 unsupported floor object types in production data.
- Measure: nightly check against allowed object type list.
- Timeframe: continuous.

6. Menu Update Freshness
- Target: menu item changes visible to waiter ordering UI in <= 5 seconds (p95).
- Measure: time from manager save to waiter-side visibility.
- Timeframe: within 12 weeks post-launch.

7. System Availability
- Target: >= 99.5% monthly availability for backend API.
- Measure: uptime monitoring over calendar month.
- Timeframe: from first production month onward.

8. Migration Safety
- Target: 100% successful Flyway migration runs across dev/staging/prod pipelines.
- Measure: CI/CD migration execution results.
- Timeframe: continuous.

## Success Criteria Summary
The project is considered successful for Phase 1 if:
- Core operational workflows (floor editing, reservations, table ordering) are adopted by staff.
- All critical objective targets 1, 2, 3, and 4 are met for at least one full month.
- No data integrity incidents are caused by schema/migration issues.
