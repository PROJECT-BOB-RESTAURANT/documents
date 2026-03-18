# Tech Stack Summary

## Frontend
- Framework: React 19
- Build tool: Vite 7
- Language: JavaScript (ES modules)
- State management: Zustand
- UI styling: Tailwind CSS 4
- Drag and drop: `@dnd-kit/core`, `@dnd-kit/utilities`
- Utility libraries: `clsx`
- Linting: ESLint 9 with React Hooks and React Refresh plugins

## Backend
- Framework: Spring Boot 4.0.3
- Language: Java 21
- API style: REST controllers (Spring Web MVC)
- Persistence: Spring Data JPA
- Validation: Spring Validation
- Security: Spring Security
- Database migrations: Flyway (`spring-boot-starter-flyway` + `flyway-mysql`)
- Build tool: Maven
- Runtime DB driver: MariaDB JDBC
- Boilerplate reduction: Lombok

## Database
- Engine: MariaDB 11.4 (Docker)
- Orchestration: Docker Compose
- Default database: `bob`
- Seed and schema management: Flyway SQL migrations (`V1`, `V2`, `V3`, `V4`)

## High-Level Architecture
- Frontend (React + Zustand) calls backend REST endpoints via a central API service.
- Backend (Spring Boot) exposes business endpoints and persists data through JPA.
- Flyway versioned migrations manage schema and seed data for consistent environments.

## Dev Workflow (Short)
- Frontend local dev: `npm run dev`
- Backend local dev: `./mvnw spring-boot:run` (or `mvnw.cmd` on Windows)
- Database local dev: `docker compose up -d` in the database folder
