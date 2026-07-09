---
skillsApplied:
  - high-level-architecture
  - go
  - openapi-conventions
---

# Design — Hello World API

## 1. Overview

The system is a single, minimal backend HTTP API that returns a friendly
greeting and exposes a health-check endpoint for platform liveness
monitoring. There is no UI, no authentication, and no persistent storage —
the goal is a clean, deployable baseline.

## 2. Components

- **hello-api** — `type: service`. The sole component. Exposes the greeting
  endpoint and the health-check endpoint. Owns no persistent data and no
  other component depends on it.

## 3. Capabilities

### hello-api

- **Greeting** — `GET /hello` returns a JSON payload containing a greeting
  message (e.g. `"Hello, World!"`), HTTP `200 OK` on success.
- **Health check** — `GET /health` returns HTTP `200 OK` when the service is
  running normally, for platform liveness probes.

## 4. Data model

No persistent entities. The only payload is the greeting response:

- **Greeting** — `message: string` (e.g. `"Hello, World!"`).

## 5. Roles & access

No authentication or authorization. All endpoints are publicly accessible.

## 6. Interactions

None. `hello-api` is a standalone service with no dependencies on other
components, external systems, or platform resources.

## 7. Data flow

1. A client sends `GET /hello` to `hello-api`.
2. `hello-api` responds immediately with `200 OK` and a JSON body containing
   the greeting message.
3. The platform periodically calls `GET /health`; `hello-api` responds
   `200 OK` while running normally.
