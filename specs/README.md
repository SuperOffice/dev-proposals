# 📑 Spec Writing Guide

Think of `/specs` as the living technical specifications — things that are no longer just proposals (ideas) or RFCs (bigger architectural changes), but formally accepted, documented designs.

- **Purpose:** Guide for writing technical specifications (specs) for SuperOffice APIs and services.
- **Audience:** Internal developers, partners, and community members implementing or integrating with SuperOffice.
- **Location:** Store specs in `/specs/` directory, organized by category (e.g., `/specs/rest/`, `/specs/graphql/`, `/specs/integrations/`).

## 🧩 Spec Structure

Each spec should include the following sections for clarity and completeness:

- **Title & Metadata**
  - Spec ID (e.g., `rest/webhooks-v2`)
  - Author(s) and date
  - Status (Draft, Final, Deprecated)
    - Version number
    - Creation and last updated dates
- **Overview**
  - Brief description of what the spec covers and its scope.
  - Relation to existing systems or specs.

- **Goals**
  - Primary objectives of the specification.
  - What problems it solves or improvements it brings.

- **Non-Goals (Optional)**
  - Clarify what the spec does **not** cover to avoid scope creep.

- **Technical Specification**
  - Detailed API endpoints (methods, URLs, parameters, request/response schemas).
  - Data models (entities, relationships, attributes).
  - Workflows and state diagrams.
  - Error handling and status codes.
  - Security considerations (authentication, authorization).
  - Performance and scalability notes.
  - Backward compatibility and versioning strategy.
  - Example requests/responses, diagrams if relevant.
  - Any dependencies or prerequisites.
  - Testing and validation strategies.
  - Backward compatibility considerations.
  - Examples & use cases.
  - Security & compliance considerations.
  - Implementation & rollout plan.
  - References to related proposals, RFCs, or external standards.

- **References**
  - Links to related proposals, RFCs, or external standards.
  - Example: [Proposal #001 – Webhooks Improvements](../proposals/2025/001-webhooks-improvements.md)
