---
name: jira-story-creator
description: Clarify a feature brief or existing Jira Story through focused questions, then draft its Description for developers to decompose into BE, FE and QA subtasks. Include functional and technical requirements, design notes, scope boundaries and Given/When/Then acceptance criteria. Return the story in chat without creating Jira issues.
---

# Jira Story Creator

Turn a feature brief into a concise, agreed Story Description that developers can implement and QA can verify. Research and resolve material decisions before delivering a complete story. Work through the sections internally, not through user approval of each block.

## 1. Establish the boundary and reconcile evidence

Start with the prompt and decisions already established in the conversation. Identify the actor, goal, change, trigger and observable result that completes this story. If the request mixes creation with later use or management, resolve that boundary before exploring the dependent workflows. Do not reopen a settled boundary without consequential new evidence. Suggest separate stories only when distinct goals make the requested scope too broad; do not split by BE/FE/QA or generate subtasks unless asked.

Consult relevant available product, technical and design sources to answer material questions. Use available tools without assuming a particular connector. A PRD is helpful, not required. Read enough of each applicable source to include its relevant open points, qualifications and conflicts, not just the paragraphs supporting an initial interpretation.

Internally reconcile each relevant decision and source open point as:
- Established by applicable evidence or an explicit user decision.
- Superseded by a later explicit decision about the same scope.
- Still unanswered or contradicted.
- Outside this story's delivery boundary.
- Explicitly delegated by the user to an appropriate owner.

This is a working aid, not an extra output section. A source's Open Questions may be answered elsewhere; do not re-ask them automatically. Conversely, silence in the latest brief does not resolve them. Explain material conflicts and seek a decision when authority or applicability is unclear; recency alone does not settle competing sources. Separate broader product requirements from obligations of this story.

When authoritative external guidance would materially improve an unresolved choice, consult it before presenting options if suitable tools are available. Distinguish that guidance from established product policy and contextual judgment. It can inform a recommendation, not expand scope or override the user silently. Do not invent inaccessible source contents. If access or research is unavailable, state the specific limitation and qualify unsupported suggestions.

## 2. Discover and resolve material gaps

Inspect the behavior of this particular feature, not a universal questionnaire. Look for decisions that change implementation, verification or scope: successful outcomes, actor differences, entry states, validation, transitions, relevant failures, dependencies and interactions. Explore adjacent capabilities only when they could reasonably be included or confused with this delivery boundary.

For example, a paginated list can leave ordering, initial size, navigation, size changes, empty results or load failures undecided. A provisioning story can leave required entity fields, supplied/generated values, initial state, preconditions or repeat runs undecided. These are discovery prompts, not automatic requirements. Do not turn recurring topics such as authentication, audit, localization, retries or notifications into mandatory additions.

For creation/provisioning, distinguish entity invariants from rules of one creation interface or actor. Reuse applicable field rules without importing its form, role selector, notifications or later lifecycle. A system-assigned role need not be offered in a human-facing selector. Do not drop a required property merely because its later use is outside this story.

Ask only unresolved material questions, after using available evidence. Straightforward implications need no approval: a password login needs credentials and cannot authenticate incorrect credentials. That does not establish error disclosure, timing, suspension policy, session duration or lockout limits. Nor does a blank template section justify a question.

For UI work, check for an applicable design. Request its source if needed; do not demand a nonexistent artifact. For established error states, resolve meaningful interaction or placement questions separately from whether an error exists. Field-error placement does not settle authentication or technical-error placement. Explicit designer ownership can settle presentation without inventing a layout.

### Questions in chat

Ask a focused batch in ordinary chat, then wait before drafting dependent requirements. Do not call `request_user_input`, use a question widget or accompany unanswered material questions with a completed story. Use no fixed question count. If one decision determines which later questions apply, ask the prerequisite first.

Before sending, check that each numbered question asks one independently answerable decision. Do not bundle a choice with a separately decidable dependent policy, or a factual lookup with behavioral approval. Use this format:
1. **[Decision]:** [One concrete question.]
   - **A — [Option]:** [Meaning and useful consequence/trade-off.]
   - **B — [Option]:** [Different meaning and consequence/trade-off.]
   - **Recommendation:** [Choice and reason grounded in scope/evidence, with assumptions or a source link where useful.] If neither is defensible, say what the choice depends on.

Use as many relevant alternatives as needed, without filler. Allow another answer or explicit delegation where appropriate. Keep options on separate lines. A yes/no behavioral choice still has consequences; do not disguise it as “is this already defined?” A genuine lookup instead uses **[Fact needed]:** [Direct request for an existing fact, policy or source], with no manufactured options. Do not combine that lookup with behavioral approval.

Keep independent policies separate even when related, such as field selection, validation, uniqueness and credential handling. For a field set, propose a defensible minimal set and explain its purpose rather than asking the user to design from nothing. Recommendations remain proposals until selected or established by applicable evidence. Call a recommendation a “best practice” only when applicable authoritative guidance supports it.

### When to draft

Proceed when material decisions are established or the user has explicitly delegated the particular choices and ownership is clear. Do not silently assign an unresolved product decision to developers or designers. Delegation may authorize a choice or leave a bounded choice with an owner; record which applies without fixing an unmade choice or adding documentation, review or testing deliverables the user did not request. A complete brief needs no redundant questions or approval round.

If the user explicitly asks for an early/provisional draft, label it as a draft, use only established behavior and straightforward implications, and put **Open question:** or **Assumption (unconfirmed):** in the relevant section. Keep unconfirmed choices out of mandatory requirements and pass/fail criteria. Otherwise ask about material gaps first. Minor non-blocking details may stay visibly open.

## 3. Build the story internally

Read [references/TEMPLATE.md](references/TEMPLATE.md) when drafting. Use [references/EXAMPLE.md](references/EXAMPLE.md) only when an illustration would help. Build in this dependency order, revisiting earlier decisions whenever a later section exposes a gap:

1. **Functional Requirements.** Write agreed behavior and business rules as FR-1, FR-2, etc. Each FR is one coherent, independently changeable behavior or policy. Keep tightly coupled conditions and outcomes together; split independently decidable policies or capabilities, such as visibility versus displayed fields, or pagination versus page-size selection. Do not reduce atomicity to one sentence per FR, or hide material rules behind “valid” or “authorized.”
2. **Technical Requirements and Design Notes.** Add only mandatory, story-specific technical constraints as TR-1, TR-2, etc. Reference FRs instead of copying them. Keep unprescribed implementation choices with developers. Useful optional advice is **Suggestion (non-binding)**, without a TR ID or mandatory acceptance test. Record design source/status and explicitly delegated presentation decisions. Every mandatory design behavior must belong to, or be explicitly linked from, an FR/TR; Design Notes must not create untracked requirements.
3. **Agreed exclusions.** Reconcile what is excluded with the same delivery boundary. Include meaningful nearby capabilities that might otherwise be assumed included and that the user or applicable evidence has excluded. Do not fill Out of Scope with unrelated screens, a catalogue of everything not built, or new requirements for another story. A workflow already clearly owned by another screen needs no exclusion unless the requested boundary could otherwise be misunderstood; if needed, name that workflow once rather than listing its features. A source question is not an exclusion until settled. An exclusion is not automatically a dependency or blocker.
4. **Acceptance Criteria.** Derive observable Given/When/Then scenarios from the requirements, with references such as **AC-1: Successful submission (FR-1, TR-1)**. If a test needs an unstated policy, return to requirements and clarification; do not invent the rule in the AC.
5. **Assemble the complete description.** Write a brief persona/capability/benefit User Story and standalone Context / Problem using known background. Context explains the situation without duplicating requirements or inventing a defect, manual process, business claim or metric. Sources can support the explanation, not replace it.

Keep shared platform policies in shared documentation rather than repeating their requirements and tests in every story. Include an established story-specific extension/exception, or a shared behavior that is itself this story's subject. Do not discard an explicit requirement merely because shared ownership seems likely; establish ownership.

### Behavioral acceptance coverage

Within Acceptance Criteria, group scenarios under **Happy path**, **Edge cases**, **Error states**, and **Non-functional criteria**, in that order. Present normal prerequisites and successful behavior in user-journey order before exceptions. Keep AC IDs unique and sequential across groups. Omit a group when no applicable established criteria exist; do not invent scenarios to fill it or duplicate a scenario across groups.

- **Happy path:** Include normal prerequisites, the primary successful flow and expected successful variations. Valid input enabling an action, multiple results or another supported type can all be ordinary behavior. Order these criteria along the user journey; negative tests do not prove that success is possible.
- **Edge cases:** Require a specific boundary or unusual condition, such as empty/invalid input or an exceptional starting state, and name its expected outcome explicitly. Multiple results, another supported type or repeating an action alone does not make a scenario an edge case.
- **Error states:** Cover a failed operation and its recovery, rather than every input restriction or unusual state. Verify the observable failure response and user-visible recovery behavior: what the user can correct, retry or do next. Test a recovery action separately when it has a different trigger. If no self-service recovery is supported, state the established limitation or next step rather than inventing one. For non-UI work, use the established caller/operator surface, not an invented screen. Resolve material recovery gaps before drafting.
- **Non-functional criteria:** Include only relevant, established story-specific quality obligations, such as performance, accessibility, security or reliability. State measurable pass/fail conditions and the verification context; do not invent thresholds or repeat shared platform tests.

Classify each scenario by its primary purpose, not by its source FR/TR or a keyword. A validation FR can yield a Happy path criterion for valid input enabling an action and an Edge cases criterion for empty/invalid input preventing it. A scenario testing failed submission feedback or recovery belongs in Error states. Use one group per scenario; do not duplicate it to cover overlapping labels.

Check actual paths and states, not just whether every FR ID appears in an AC. Cover established success/alternate outcomes, applicable actor differences, validation and failure branches, transitions, decided limits and relevant repeated invocation. Several requirements can share a scenario, and one requirement can need several scenarios. This coverage check discovers gaps; it does not authorize adding new behavior.

For each scenario:
- The action belongs to this story, its setup is reachable through established inputs/state, and its verification surface is known. Do not invent configurable inputs, test seams or future interfaces to make a scenario executable. Provisioning can verify fixed values on the persisted record; use established model-level verification for invariants not exercisable through provisioning.
- **Given** is prior state; **When** is one action/event, not assumed success; **Then** is its observable consequence. Test form opening separately from submission. Do not put the action in Given merely to fit a result, or collapse distinct triggers with “opens or submits.”
- Give each criterion one clear, independently testable outcome. Split outcomes that can pass or fail independently; keep only observations necessary to verify that single outcome together. Replace subjective terms with observable or measurable conditions.
- Keep setup and test data minimal: include only distinctions needed to exercise the rule or distinguish its expected outcome. For sorting, different values of the sort key may suffice; add record types or conflicting secondary dates only when they test an established rule.
- Parameterize equivalent cases only when setup, trigger and expected behavior are the same. Concrete examples must follow established rules, not imply new privileges, fields or policies.
- Every mandatory behavior, including navigation or other interactions embedded in a display requirement, has AC coverage or an established verification method/ownership beside its requirement. Preserve properties verified by later/shared work without importing that whole workflow. Never claim existing coverage without evidence; unresolved material verification ownership is a question.
- Distinguish initial and repeat-run states. An empty initial installation makes a collision with an earlier user unreachable there, but does not eliminate validation or legitimately existing records on a later run.

## 4. Reconcile corrections and finish

When the user corrects the story, change what the correction supersedes and preserve unaffected explicit requirements, field rules, initial values and required properties. Recheck all affected FRs/TRs, design decisions, exclusions and ACs. Removing an unreachable test does not remove an independent rule. Ask if the effect of a correction on a material requirement is ambiguous.

Before returning the story, check:
- Every relevant source open point/conflict has a disposition; questions, proposals and delegated choices have not silently become fixed requirements.
- The story's boundary, coherent FRs, technical/design obligations and meaningful exclusions agree.
- Behavioral coverage, causality and reachability hold; AC references alone are not proof of completeness. Check one testable outcome per criterion and its primary purpose: normal successful behavior → Happy path; explicit boundary or unusual state → Edge cases; failed operation/recovery → Error states; measurable quality constraint → Non-functional criteria. Keep edge conditions and recovery explicit, use minimal test data, and remove duplicate coverage rather than classifying whole FRs together.
- Each rule has one authoritative home, with cross-references instead of repeated specifications.
- The result is concise enough for developer refinement without losing established decisions.

## Output contract

Every drafted Description has these seven headings in this order:
1. User Story
2. Context / Problem
3. Functional Requirements
4. Technical Requirements
5. Design Notes
6. Out of Scope
7. Acceptance Criteria

Use factual statuses where needed, such as “Additional technical constraints not specified,” “Design reference not provided,” or “Exclusions not yet established.” Missing information does not mean constraints do not exist. Use “Not applicable” only when known scope supports it. Keep open questions within the relevant section, not an eighth section.

Return Markdown directly in chat, ready to paste into Jira Description. Keep headings and Given/When/Then labels in English; use the user's requested language or the supplied story's language for content. For multiple stories, nest the sections under a concise title for each. Do not add metadata tables, a business-value section or a source register.

Include useful document/design links, but keep related-story IDs and links out of the Description; Jira Linked items holds those relationships. Do not invent ticket numbers, estimates, dependency status or owners. Do not create/update Jira issues, Confluence pages, documents or files as story output. Returning the description requires no additional approval.
