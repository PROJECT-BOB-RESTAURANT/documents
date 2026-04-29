# User Stories Backlog

This list contains only stories that are implemented in the current codebase.

## User Stories

1. As a customer, I want to create a reservation with guest count, table selection, date-time range, and notes so that the restaurant can prepare for my visit.
- Role: Customer
- Scope: `implemented`
- Priority: High

2. As a waiter, I want to open a table service panel from the floor plan so that I can manage orders at the selected table quickly.
- Role: Waiter
- Scope: `implemented`
- Priority: High

3. As a waiter, I want to create and update order lines (quantity, note, status) so that kitchen and service flow stays accurate.
- Role: Waiter
- Scope: `implemented`
- Priority: High

4. As a waiter, I want to manage table reservations (create, update, delete) from the table service view so that walk-ins and changes can be handled quickly.
- Role: Waiter
- Scope: `implemented`
- Priority: Medium

5. As a waiter, I want single and split payment entry on a table so that bills can be closed according to guest preference.
- Role: Waiter
- Scope: `implemented`
- Priority: Medium

6. As a manager, I want to create restaurants and floors so that multi-location operations are modeled correctly.
- Role: Manager
- Scope: `implemented`
- Priority: High

7. As a manager, I want to design floor layouts using known objects (tables, doors, stairs, toilets, kitchen blocks) so that the digital map matches reality.
- Role: Manager
- Scope: `implemented`
- Priority: High

8. As a manager, I want to manage weekly opening hours and date-specific overrides so that special days are handled correctly.
- Role: Manager
- Scope: `implemented`
- Priority: High

9. As a manager, I want to manage menu folders and items with prices so that waiter ordering reflects the latest menu.
- Role: Manager
- Scope: `implemented`
- Priority: High

10. As a manager, I want to configure table labels and seating metadata in the editor so that reservation and seating rules are correct.
- Role: Manager
- Scope: `implemented`
- Priority: Medium

11. As a manager, I want reservation and service statistics views so that I can monitor active reservations and service workload.
- Role: Manager
- Scope: `implemented`
- Priority: Medium

12. As kitchen staff, I want to see incoming kitchen tickets with periodic refresh so that I can prioritize prep order.
- Role: Kitchen Staff
- Scope: `implemented`
- Priority: High

13. As kitchen staff, I want to move ticket lines through kitchen lifecycle states (pending, in progress, in prep, ready for server, served) so that front-of-house sees accurate status.
- Role: Kitchen Staff
- Scope: `implemented`
- Priority: High

14. As an admin, I want to create, update, search, and delete users so that access and staff accounts can be maintained.
- Role: Admin
- Scope: `implemented`
- Priority: High

15. As a manager, I want to assign existing users as restaurant workers and update/remove those assignments so that staffing reflects the active team.
- Role: Manager
- Scope: `implemented`
- Priority: High

## Notes for Grooming
- Keep user stories implementation-agnostic; acceptance criteria should be added in sprint planning.
- Keep roadmap ideas in a separate file so this document stays strictly implementation-truthful.
