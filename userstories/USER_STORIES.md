# User Stories Backlog

## Scope Labels
- `current-fit`: aligns with current app direction
- `future`: not fully implemented yet, candidate roadmap

## User Stories

1. As a customer, I want to browse available tables by time slot so that I can quickly choose where to sit.
- Role: Customer
- Scope: `current-fit`
- Priority: High

2. As a customer, I want to create a reservation with guest count and notes so that the restaurant can prepare for my visit.
- Role: Customer
- Scope: `current-fit`
- Priority: High

3. As a customer, I want to edit or cancel my reservation from a confirmation link so that I can manage changes without calling the restaurant.
- Role: Customer
- Scope: `future`
- Priority: High

4. As a customer, I want to see whether a table is indoor, outdoor, or near special areas so that I can pick a table matching my preference.
- Role: Customer
- Scope: `future`
- Priority: Medium

5. As a waiter, I want to open a table service panel from the floor plan so that I can manage orders at the selected table quickly.
- Role: Waiter
- Scope: `current-fit`
- Priority: High

6. As a waiter, I want to create and update order lines (quantity, note, status) so that kitchen and service flow stays accurate.
- Role: Waiter
- Scope: `current-fit`
- Priority: High

7. As a waiter, I want to assign an order to myself or another worker so that accountability and handovers are clear.
- Role: Waiter
- Scope: `current-fit`
- Priority: Medium

8. As a waiter, I want to transfer a table to another waiter during shift change so that service continuity is smooth.
- Role: Waiter
- Scope: `future`
- Priority: Medium

9. As a manager, I want to create restaurants and floors so that multi-location operations are modeled correctly.
- Role: Manager
- Scope: `current-fit`
- Priority: High

10. As a manager, I want to design floor layouts using known objects (tables, doors, stairs, toilets, kitchen blocks) so that the digital map matches reality.
- Role: Manager
- Scope: `current-fit`
- Priority: High

11. As a manager, I want to manage opening hours per day so that customers and staff always see accurate operating times.
- Role: Manager
- Scope: `current-fit`
- Priority: High

12. As a manager, I want to manage menu folders and items with prices so that waiter ordering reflects the latest menu.
- Role: Manager
- Scope: `current-fit`
- Priority: High

13. As a manager, I want to configure table capacity and labels in the editor so that reservation and seating rules are correct.
- Role: Manager
- Scope: `current-fit`
- Priority: Medium

14. As a manager, I want analytics for table turnover and peak hours so that I can optimize staffing and seating strategy.
- Role: Manager
- Scope: `future`
- Priority: Medium

15. As a chef, I want to see incoming kitchen tickets in real time so that I can prioritize cooking order.
- Role: Chef
- Scope: `future`
- Priority: High

16. As a chef, I want to mark order lines as started, ready, or delayed so that waiters have accurate kitchen status.
- Role: Chef
- Scope: `future`
- Priority: High

17. As a chef, I want to flag an item as out of stock so that front-of-house cannot place unavailable dishes.
- Role: Chef
- Scope: `future`
- Priority: High

18. As kitchen staff, I want a simplified prep screen grouped by station (grill, cold, dessert) so that teams can work in parallel efficiently.
- Role: Kitchen Staff
- Scope: `future`
- Priority: Medium

19. As kitchen staff, I want allergy alerts highlighted on tickets so that dangerous mistakes are prevented.
- Role: Kitchen Staff
- Scope: `future`
- Priority: High

20. As an admin, I want role-based permissions for manager/waiter/chef/customer actions so that sensitive operations are protected.
- Role: Admin
- Scope: `future`
- Priority: High

21. As a manager, I want to mark specific calendar days as fully closed so that customers cannot place reservations on those dates.
- Role: Manager
- Scope: `future`
- Priority: High

22. As a waiter, I want a payment menu with full and split payment options so that groups can pay together or individually.
- Role: Waiter
- Scope: `future`
- Priority: High

23. As a customer, I want to reserve an entire floor for a large party so that private or corporate events can be organized easily.
- Role: Customer
- Scope: `future`
- Priority: High

## Notes for Grooming
- Keep user stories implementation-agnostic; acceptance criteria should be added in sprint planning.
- Break large stories into technical tasks (UI, store logic, backend endpoints, validation, audit logs).
- Validate each `future` story against business value and effort before adding to active sprint backlog.
