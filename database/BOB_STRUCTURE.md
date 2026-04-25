# Bob Database Structure

This document describes the current logical structure of the `bob` database after Flyway migrations `V1` to `V15`.

## Overview

The schema models a restaurant management system with these domains:

- Restaurant core: restaurants, users, and staff
- Floor planning: floors and floor objects (tables, chairs, decor)
- Menu management: menu folders and menu items
- Reservation flow: reservations per table object
- Order flow: table orders and order lines
- Opening hours: weekly schedule plus date-specific overrides

## Entity Relationship Summary

- `restaurant` -> `floor` (1:N)
- `floor` -> `floor_object` (1:N)
- `restaurant` -> `menu_folder` (1:N)
- `menu_folder` -> `menu_folder` (1:N self-reference for nested folders)
- `menu_folder` -> `menu_item` (1:N)
- `restaurant` -> `opening_hour` (1:N, unique per day)
- `restaurant` -> `opening_hour_override` (1:N, unique per date)
- `floor_object` -> `reservation` (1:N)
- `restaurant` -> `worker` (1:N)
- `floor_object` -> `table_order` (1:N)
- `worker` -> `table_order` (1:N, nullable on order side)
- `table_order` -> `table_order_line` (1:N)
- `worker` -> `table_order_line` (1:N, nullable on order line side)
- `user` -> `worker` (1:N)

## Tables

### `restaurant`

Master entity for each restaurant.

Key columns:

- `id` (PK, `binary(16)`)
- `name` (`varchar(120)`)
- `created_at`, `updated_at`

Indexes:

- `idx_restaurant_name` on `name`

### `floor`

Represents one editable floor/canvas of a restaurant.

Key columns:

- `id` (PK)
- `restaurant_id` (FK -> `restaurant.id`)
- `name`
- `width`, `height`
- `canvas_zoom`, `canvas_pos_x`, `canvas_pos_y`
- `created_at`, `updated_at`

Indexes:

- `idx_floor_restaurant` on `restaurant_id`

### `floor_object`

Objects placed on a floor (table/chair/decor/etc.).

Key columns:

- `id` (PK)
- `floor_id` (FK -> `floor.id`)
- `type`
- `x`, `y`, `width`, `height`
- `rotation`, `scale_x`, `scale_y`
- `metadata` (JSON-validated text)
- `created_at`, `updated_at`

Indexes:

- `idx_floor_object_floor` on `floor_id`
- `idx_floor_object_type` on `type`

### `menu_folder`

Hierarchical menu categories for a restaurant.

Key columns:

- `id` (PK)
- `restaurant_id` (FK -> `restaurant.id`)
- `parent_folder_id` (self FK -> `menu_folder.id`, nullable)
- `name`
- `sort_order`
- `created_at`

Indexes:

- `idx_menu_folder_restaurant` on `restaurant_id`
- `idx_menu_folder_parent` on `parent_folder_id`

### `menu_item`

Actual sellable items attached to menu folders.

Key columns:

- `id` (PK)
- `folder_id` (FK -> `menu_folder.id`)
- `name`
- `price`
- `sort_order`
- `created_at`

Indexes:

- `idx_menu_item_folder` on `folder_id`

### `opening_hour`

Opening configuration per restaurant and weekday.

Key columns:

- `id` (PK)
- `restaurant_id` (FK -> `restaurant.id`)
- `day_of_week` (smallint)
- `open_time`, `close_time`
- `is_closed` (bit)

Behavior notes:

- Overnight windows are supported (for example `18:00` to `02:00`).
- `open_time` and `close_time` must differ when `is_closed = 0`.

Indexes and uniqueness:

- `idx_opening_hour_restaurant` on `restaurant_id`
- `uq_opening_hour_restaurant_day` unique on (`restaurant_id`, `day_of_week`)

### `opening_hour_override`

Date-specific schedule override (holiday closure, special service day) for a restaurant.

Key columns:

- `id` (PK)
- `restaurant_id` (FK -> `restaurant.id`)
- `service_date` (date)
- `open_time`, `close_time`
- `is_closed` (bit)

Behavior notes:

- Overrides take precedence over weekly `opening_hour` rows in application logic.
- Overnight windows are supported and `open_time`/`close_time` must differ when open.

Indexes and uniqueness:

- `idx_opening_hour_override_restaurant` on `restaurant_id`
- `idx_opening_hour_override_service_date` on `service_date`
- `uq_opening_hour_override_restaurant_date` unique on (`restaurant_id`, `service_date`)

### `reservation`

Guest reservation assigned to a table object.

Key columns:

- `id` (PK)
- `table_object_id` (FK -> `floor_object.id`)
- `guest_name`
- `party_size`
- `start_at`, `end_at`
- `note`
- `created_at`

Indexes:

- `idx_reservation_table` on `table_object_id`
- `idx_reservation_time` on (`start_at`, `end_at`)

### `user`

Authentication users that can be linked to workers.

Key columns:

- `id` (PK, `binary(16)`)
- `username` (`varchar(120)`, unique)
- `name` (`varchar(120)`, required)
- `password` (`varchar(255)`)
- `role` (`varchar(40)`, default `STAFF`)
- `created_at`

Constraints:

- `chk_user_username_nonempty`: `LENGTH(TRIM(username)) > 0`
- `chk_user_name_nonempty`: `LENGTH(TRIM(name)) > 0`
- `chk_user_role`: `role` in (`ADMIN`, `MANAGER`, `STAFF`)

Indexes:

- `idx_user_username` on `username`

### `worker`

Restaurant employees (manager/waiter/chef, etc.).

Key columns:

- `id` (PK)
- `restaurant_id` (FK -> `restaurant.id`)
- `user_id` (FK -> `user.id`, nullable)
- `name`
- `role`
- `created_at`

Indexes:

- `idx_worker_restaurant` on `restaurant_id`
- `idx_worker_user` on `user_id`

### `table_order`

Order session for a table object.

Key columns:

- `id` (PK)
- `table_object_id` (FK -> `floor_object.id`)
- `worker_id` (FK -> `worker.id`, nullable)
- `status` (default `OPEN`)
- `created_at`
- `closed_at`

Indexes:

- `idx_table_order_table` on `table_object_id`
- `idx_table_order_worker` on `worker_id`

### `table_order_line`

Individual line item within a table order.

Key columns:

- `id` (PK)
- `table_order_id` (FK -> `table_order.id`)
- `item_name`
- `quantity`
- `unit_price`
- `note`
- `placed_by_worker_id` (FK -> `worker.id`, nullable)
- `placed_by_worker_name_snapshot`
- `status` (default `PENDING`)
- `status_updated_at` (`datetime(6)`, required)
- `in_progress_at` (`datetime(6)`, nullable)
- `in_prep_at` (`datetime(6)`, nullable)
- `ready_for_server_at` (`datetime(6)`, nullable)
- `served_at` (`datetime(6)`, nullable)
- `created_at`

Indexes:

- `idx_table_order_line_order` on `table_order_id`
- `fk_table_order_line_worker` on `placed_by_worker_id`
- `idx_table_order_line_status_created` on (`status`, `created_at`)

Allowed statuses:

- `PENDING`
- `IN_PROGRESS`
- `IN_PREP`
- `READY_FOR_SERVER`
- `SERVED`
- `VOID`

## Foreign Key Delete Behavior

- Most child entities use `ON DELETE CASCADE`.
- This includes auth linkage: `worker.user_id` -> `user.id`.
- Staff references in order flows use `ON DELETE SET NULL`:
  - `table_order.worker_id`
  - `table_order_line.placed_by_worker_id`

This allows retaining historical order records if a worker is removed.

## UUID Storage Note

Primary and foreign keys use `binary(16)` values, which indicates compact UUID-style identifiers instead of integer IDs.

## Seed Data Notes (Latest Migrations)

- `V14` replaces previous sample data with a denser multi-restaurant seed set.
- `V15` aligns seeded user names, floor naming, and table labels with the latest expected demo format.
- These seed migrations affect demo content only, not the core schema relationships.

## Related Assets

- SQL dump: `database/bob-database.sql`
- ER diagram source (draw.io): `documents/database/BOB_ER_DIAGRAM.drawio`
- ER diagram source (png): `documents/database/BOB_ER_DIAGRAM.png`