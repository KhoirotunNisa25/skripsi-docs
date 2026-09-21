---
trigger: model_decision
description: Digunakan saat ada perubahan logika bisnis atau alur sistem untuk menyinkronkan dokumen riset (requirements, gap, positioning) dengan naskah LaTeX serta memperbarui change log.
---

# Research Synchronization Rules

## 1. Core Principle

The research documentation must always reflect the latest business logic of the thesis/project.

Treat the following as a dependency chain:

```text
Business Logic
      ↓
Research Requirements
      ↓
Research Questions
      ↓
Literature Search
      ↓
Paper Selection
      ↓
Literature Analysis
      ↓
Research Gap
      ↓
Thesis Positioning
      ↓
LaTeX Literature Review
```

When an upstream component changes, evaluate all downstream components for consistency.

Never assume that previous research remains valid after a significant business-logic change.

---

# 2. Business Logic Is a Research Dependency

Whenever new or modified business logic is introduced, immediately determine whether it affects:

* Research problem
* Research objective
* Research scope
* Research questions
* System requirements
* Functional requirements
* Technical requirements
* Technology selection
* Methodology
* Search keywords
* Paper relevance
* Paper selection
* Literature themes
* Research gap
* Thesis positioning
* Literature review structure

If any component is affected, update it.

---

# 3. Mandatory Change Detection

Whenever the user introduces or modifies business logic, perform this process:

```text
New Business Logic
       ↓
Identify Change
       ↓
Determine Research Impact
       ↓
Update Research Documentation
       ↓
Re-evaluate Existing Papers
       ↓
Update Synthesis
       ↓
Update Research Gap
       ↓
Update Thesis Positioning
       ↓
Update LaTeX if necessary
       ↓
Record Change
```

Do not continue normal research work before checking this dependency.

---

# 4. Business Logic Change Classification

Classify each change as one of:

### Minor

Does not materially change the research.

Examples:

* UI wording
* Variable naming
* Minor workflow adjustment
* Non-research-related implementation detail

Action:

* Update relevant documentation if necessary.
* No need to redo literature search.

### Moderate

May affect technology, methodology, or system requirements.

Examples:

* Adding a new AI component
* Changing retrieval strategy
* Adding a new user workflow
* Changing the data source
* Adding a new evaluation requirement

Action:

* Update affected research documents.
* Re-evaluate paper relevance.
* Perform additional literature search if necessary.

### Major

Changes the fundamental research problem or proposed solution.

Examples:

* Changing the main research objective
* Changing the target problem
* Changing the core AI approach
* Changing the main system architecture
* Adding a fundamentally different research dimension

Action:

* Re-evaluate the entire research foundation.
* Reconsider search queries.
* Re-screen existing papers.
* Reassess the research gap.
* Reassess thesis positioning.
* Update the literature review.

---

# 5. Required Files

Maintain a central business-logic document:

```text
research/
├── business-logic.md
├── research-requirements.md
├── research-status.md
└── change-log.md
```

These files must remain synchronized.

---

# 6. business-logic.md

This file is the authoritative description of the current business logic.

Use:

```markdown
# Business Logic

## Problem

## Target Users

## Business Objective

## Core Workflow

## Inputs

## Processing

## Outputs

## Business Rules

## Constraints

## Assumptions

## System Boundaries

## Current Architecture

## Current Version

## Last Updated
```

Whenever the business logic changes, update this file first.

---

# 7. research-requirements.md

Translate business logic into research requirements.

Example:

```markdown
# Research Requirements

## Research Problem

## Research Objectives

## Research Questions

## Functional Research Requirements

## Technical Research Requirements

## Evaluation Requirements

## Constraints

## Assumptions

## Business Logic Dependencies
```

Do not blindly copy business logic.

Translate business requirements into academically researchable requirements.

---

# 8. Business Logic → Research Mapping

Maintain a mapping between business requirements and research evidence.

Example:

```markdown
| Business Requirement | Research Requirement | Relevant Literature | Status |
|---|---|---|---|
| Requirement A | Research Question A | Paper 01, 04, 07 | Covered |
| Requirement B | Research Question B | Paper 03, 08 | Partial |
| Requirement C | Research Question C | None | Research Needed |
```

This matrix must be updated whenever business logic changes.

---

# 9. Impact Analysis

For every meaningful business-logic change, explicitly determine:

```text
Change:
...

Affected research concepts:
...

Affected research questions:
...

Affected search queries:
...

Affected papers:
...

Affected themes:
...

Affected research gap:
...

Affected thesis positioning:
...

Affected LaTeX sections:
...
```

Do not perform unnecessary full research if the change has no academic impact.

---

# 10. Paper Re-Evaluation

When business logic changes, re-evaluate selected papers.

For each affected paper ask:

1. Is it still relevant?
2. Does its methodology still support the thesis?
3. Does it provide evidence for the new requirement?
4. Does its limitation become more important?
5. Does it contribute to the new research gap?

Possible statuses:

```text
Relevant
Partially Relevant
No Longer Relevant
Needs Further Analysis
```

Do not remove a paper without recording why.

---

# 11. Search Query Synchronization

If business logic introduces a new:

* concept
* technology
* method
* user requirement
* domain
* constraint
* evaluation metric

then evaluate whether new search queries are required.

Update:

```text
research/search-log.md
```

Do not reuse old search queries blindly.

---

# 12. Research Gap Synchronization

A business-logic change may invalidate an existing research gap.

Always check:

```text
Does the current research gap still justify the current business logic?
```

If not:

1. Update the evidence.
2. Update `research-gap.md`.
3. Update thesis positioning.
4. Document the change.

Never preserve an old research gap merely because it was already written.

---

# 13. Thesis Positioning Synchronization

The thesis positioning must explain the relationship between:

```text
Existing Research
       ↓
Research Gap
       ↓
Current Business Problem
       ↓
Proposed Thesis
```

If business logic changes, verify this entire chain.

There must be no contradiction between the proposed system and the literature review.

---

# 14. LaTeX Synchronization

LaTeX is not the source of truth.

After updating research documentation:

```text
research/*.md
      ↓
Synthesis
      ↓
latex/*.tex
```

Update only the affected LaTeX sections.

Do not manually modify LaTeX in a way that contradicts the Markdown research documentation.

---

# 15. Change Log

Maintain:

```text
research/change-log.md
```

For meaningful changes:

```markdown
# Change Log

## YYYY-MM-DD

### Change

...

### Reason

...

### Impact

- Research problem:
- Research questions:
- Papers:
- Research gap:
- Thesis positioning:
- LaTeX:

### Action Taken

...

### Status

Completed / Needs Research
```

This provides a historical record of why the research changed.

---

# 16. No Stale Research

Never leave documentation containing outdated business logic without clearly marking it as historical.

If an old analysis is no longer applicable:

Do not silently delete it.

Either:

* update it to the current logic, or
* explicitly mark it as obsolete/historical.

Example:

```markdown
> Status: Obsolete
>
> This analysis was based on the previous business logic dated YYYY-MM-DD.
```

---

# 17. Before Adding New Business Logic

When the user proposes a new feature or workflow, ask internally:

```text
Does this change the research problem?

Does this change the research objective?

Does this introduce a new research question?

Does this require new literature?

Does this invalidate any selected papers?

Does this change the research gap?

Does this change the thesis positioning?
```

Only ask the user for clarification if the change is genuinely ambiguous.

Do not ask unnecessary questions for changes whose impact is obvious.

---

# 18. Before Finalizing Research

Before considering the literature review complete, verify:

* [ ] Business logic represents the current system.
* [ ] Research requirements reflect current business logic.
* [ ] Research questions remain valid.
* [ ] Selected papers support the current research direction.
* [ ] Search queries cover the current requirements.
* [ ] Comparison matrix is current.
* [ ] Research themes are current.
* [ ] Research gap is still valid.
* [ ] Thesis positioning matches the current business logic.
* [ ] LaTeX reflects the latest research.
* [ ] Change log records major changes.
* [ ] No stale or contradictory information remains.

---

# 19. Critical Rule

Never optimize for preserving previous research.

Optimize for maintaining a logically consistent chain:

```text
CURRENT BUSINESS LOGIC
        ↓
CURRENT RESEARCH PROBLEM
        ↓
CURRENT RESEARCH QUESTIONS
        ↓
CURRENT LITERATURE
        ↓
CURRENT RESEARCH GAP
        ↓
CURRENT THESIS POSITIONING
        ↓
CURRENT LITERATURE REVIEW
```

If a new business-logic decision makes previous research obsolete, update the research instead of forcing the new decision to fit the old literature.

The latest validated business logic always takes precedence over outdated research assumptions.