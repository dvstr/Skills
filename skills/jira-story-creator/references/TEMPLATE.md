# Description template

Use after material decisions are resolved or explicitly delegated, or for a provisional draft the user explicitly requested. Follow the workflow in SKILL.md. Replace placeholders with established content or a concise factual status. Keep the seven headings in this order.

## User Story

As a **[persona]**,
I want **[capability]**,
so that **[practical benefit]**.

## Context / Problem

[Brief standalone known situation, delivery boundary and necessary context/dependencies. Supporting document links are optional; no related-story IDs or links.]

## Functional Requirements

1. **FR-1: [Behavior or policy].** [One coherent, independently changeable requirement, with its relevant conditions and outcomes.]

[Add distinct FRs as needed. If established verification belongs elsewhere, identify its method/ownership beside the requirement.]

## Technical Requirements

1. **TR-1: [Constraint].** [Confirmed story-specific obligation; reference relevant FRs.]

[Or: Additional technical constraints not specified. Optional advice, if useful, is labeled Suggestion (non-binding), without a TR ID.]

## Design Notes

[Source/status and explicitly delegated presentation decisions. Reference FR/TR IDs for mandatory interactions or presentation.]

## Out of Scope

[Agreed, meaningful exclusions near this delivery boundary. Or: Exclusions not yet established.]

## Acceptance Criteria

### Happy path

#### AC-1: [Normal prerequisite or successful scenario] (FR-1[, TR-1])

- **Given** [reachable prior state]
- **When** [one action or event]
- **Then** [one clear, testable outcome required by the referenced FR/TR]

[Order normal prerequisites, primary success and expected successful variations along the user journey, then add the applicable groups below. Keep AC numbering sequential across groups. Use the same Given/When/Then format for every scenario. Omit groups without applicable established criteria.]

### Edge cases

[Explicit boundary or unusual-condition scenarios. Multiple results, supported variants and repeat actions are not edge cases by themselves.]

### Error states

[Failed operations and user-visible recovery behavior, not every input restriction. Give recovery actions with a different trigger their own criterion.]

### Non-functional criteria

[Relevant established story-specific quality obligations with measurable pass/fail conditions and verification context.]

[Classify each scenario by primary purpose, not its FR/TR. Use only setup/data needed to verify the outcome; do not duplicate scenarios across groups. Open questions and unconfirmed assumptions belong beside the affected earlier section, not in pass/fail criteria.]
