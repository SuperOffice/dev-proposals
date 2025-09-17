# Contributing to SuperOffice Developer Proposals

Thanks for your interest in contributing! 🎉  

This repository is where we **discuss, design, and evolve** the SuperOffice developer platform and APIs together with our partners and customers.  

We welcome your proposals, ideas, and feedback.  

---

## 💡 Ways to Contribute

You can participate in several ways:

- **Start a discussion** → For early ideas or open-ended questions, use [GitHub Discussions](../../discussions).  
- **Open an issue** → For focused suggestions or small improvements.  
- **Submit a proposal** → For larger design changes, new APIs, or significant enhancements.  
- **Comment on proposals** → Share your feedback and help refine existing proposals.  

---

## 📝 Submitting a Proposal

If you want to suggest a new API, feature, or design change, follow these steps:

1. **Check for existing proposals** in [/proposals](./proposals).  
   - Avoid duplicates by searching open and closed proposals.  

2. **Create a new proposal file**:
   - Copy the [proposal template](./proposals/template.md).  
   - Save it under:

     ```text
     /proposals/YYYY/NNN-title.md
     ```

     - `YYYY` = current year  
     - `NNN` = next available proposal number (e.g., 001, 002, 003…)  
     - `title` = short-dashed-title (e.g., `incremental-search-api`)  

3. **Open a Pull Request (PR)** with your proposal.  
   - Give it a clear title: `Proposal: Incremental Search API`  
   - Add a short summary in the PR description.  

4. **Discuss and refine**  
   - Community members and the SuperOffice team will review, ask questions, and suggest changes.  
   - Expect a few iterations before a decision is reached.  

---

## 📜 Proposal Lifecycle

Each proposal will go through these phases:

- **Draft** → newly submitted, open for comments  
- **In Review** → under active discussion and refinement  
- **Accepted** → approved and planned for implementation  
- **Implemented** → shipped and documented in the product  
- **Rejected** → declined, with rationale recorded  
- **Deferred** → postponed for future consideration  

The status is tracked at the top of each proposal document.  

---

## ✍️ Proposal Template (Summary)

Proposals follow a structured format:

```markdown
# Proposal: Short Title

- **Author(s):** @username(s)
- **Status:** Draft | In Review | Accepted | Rejected | Deferred
- **Version:** 1.0
- **Created:** YYYY-MM-DD
- **Updated:** YYYY-MM-DD

## Summary
Concise explanation of the change.

## Motivation
Why is this needed? What problem does it solve?

## Detailed Design
- Proposed API endpoints, schemas, workflows
- Security and compatibility considerations

## Alternatives
Other approaches considered and why they weren’t chosen.

## Open Questions
Unresolved points needing feedback.
