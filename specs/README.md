# Specifications (`/specs`)

This folder contains **formal specifications** for the SuperOffice developer platform and APIs.
Unlike proposals or RFCs, these documents represent **accepted, reference-level designs** that are ready for implementation and long-term use.

---

## 📝 When to Promote a Document to `/specs`

A proposal or RFC should be promoted to a **specification** when:

- It has been **accepted** through the proposal/RFC process.
- The design is **stable and agreed upon** by the SuperOffice team.
- It contains **sufficient technical detail** for developers to rely on.
- It is ready to be used as a **reference document** in implementation and documentation.

---

## 🛠️ Spec Lifecycle

Each spec has a **status**:

- **Draft** → Initial spec draft, under final review.
- **Final** → Approved and considered the reference implementation.
- **Deprecated** → No longer recommended; superseded by a newer spec.

---

## 📎 References

- [Proposals folder](../proposals/) → Idea-stage contributions.
- [RFCs folder](../rfcs/) → Deep technical designs.
- [Spec Template](./template.md) → Use this to create a new specification.

---

## 🛤️ Path of Promotion

The following diagram illustrates the typical path from idea to implementation:

✅ *Proposal → RFC → Spec → Implementation*

```mermaid
flowchart TD
    A[Idea / Feedback] --> B{Is it substantial?}
    B -- minor --> I[Issue / Discussion]
    I -->|closed with outcome| A

    B -- significant --> C[Proposal PR in /proposals]
    C --> D{Review}
    D -->|needs work| C
    D -->|duplicate/out of scope| X[Closed Archived]
    D -->|approved| E[Accepted Proposal]

    E --> F{Broad / Cross-cutting?}
    F -- yes --> G[RFC Draft /rfcs]
    G --> H{RFC Review}
    H -->|needs work| G
    H -->|rejected| X
    H -->|approved| J[Accepted RFC]

    F -- no --> K[Spec Draft /specs]

    J --> K[Spec Draft /specs]
    K --> L{Spec Review}
    L -->|needs work| K
    L -->|approved| M[Spec: Final]
    L -->|deferred| Y[Deferred]

    M --> N[Implementation]
    N --> O[Docs & Release Notes]
    O --> P[Maintenance]
    P --> Q{Replacement?}
    Q -- yes --> R[Spec: Deprecated]
    Q -- no --> P
```
