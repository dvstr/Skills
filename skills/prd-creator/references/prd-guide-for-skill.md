# Product Requirements Document (PRD) Guide

---

## Introduction

**Rules:**
- Your one-liner must explain the core value proposition. If you can't explain why this matters in one sentence, the feature is probably too complex or lacks focus.
- Avoid listing features here; focus on the outcome.

**Strong Examples:**
- "We are redesigning the checkout flow to reduce cart abandonment by allowing guest checkouts."
- "We are automating the document verification process to reduce manual KYC review time from 24 hours to 5 minutes."

**Weak Examples:**
- "We want to add a guest checkout button, change the color of the pay button, and add Apple Pay to the cart page."
- "Rebuilding the core engine in Go so it runs faster." *(This is an engineering goal, not a product outcome).*

---

## Context and Problem

### Target Audience

**Rules:**
- Be specific about who experiences the problem. Avoid generic terms like "all users."
- Quantify the audience size or impact where possible.

**Strong Examples:**
- "Inactive users who haven't logged in for 30 days (approx. 15% of our monthly active users)."
- "Small to medium-sized retail businesses processing between $10k and $50k monthly."

**Weak Examples:**
- "Our customers."
- "Users who like fast apps."

### Problem Statement

**Rules:**
- Focus on the *user's* pain, not just a business metric.
- Contrast the "Current State" (the painful workaround) with the "Future State" (the desired seamless experience).

**Strong Examples:**
- "Currently, users have to call support to change their email address, taking an average of 15 minutes per request. In the future state, users should be able to update their email securely via their profile settings without agent intervention."
- "Current State: Partners manually upload CSV files bi-weekly, leading to data staleness. Future State: Partners connect via API to push real-time inventory updates."

**Weak Examples:**
- "We need an email change form because we don't have one."
- "The CSV upload is old and we should use an API."

---

## Business Requirements and Success Criteria

### Goals

**Rules:**
- Every goal must be paired with an observable, measurable metric.
- Do not use binary metrics (like "feature is launched") as your primary success criteria.

**Strong Examples:**
- **Goal:** "Reduce support tickets related to password resets." | **Metric:** "20% reduction in password-related Zendesk tickets within 30 days of launch."
- **Goal:** "Increase feature discovery." | **Metric:** "Increase the number of unique users clicking the 'Explore' tab by 10% week-over-week."

**Weak Examples:**
- **Goal:** "Build the feature." | **Metric:** "Code deployed to production."
- **Goal:** "Make users happy." | **Metric:** "More usage."

### BPMN Diagram

**Rules:**
- Keep this section for link – PRD owner should provide BPMN diagram later.

### Business Requirements

**Rules:**
To avoid leaking technical stuff, define requirements as *behavioral changes*:
- "User can …"
- "System must allow user to …" (only if truly user-facing)
- Business rules in plain language (limits, eligibility, validations, compliance checks as *policy*, not implementation)

**Strong Examples:**
- "A user can attempt to enter their PIN up to 3 times. On the 3rd failed attempt, the system must lock the account for 30 minutes and send an email notification."
- "The system must allow a user to generate a PDF summary of their monthly transactions between any two dates falling within the last 24 months."

**Weak Examples:**
- "Add a `failed_attempts` INT column to the database and set up a Redis cache to track timeouts." *(Too technical).*
- "Build a PDF export button that calls the `/api/v1/export` endpoint."

### Constraints / Compliance

**Rules:**
- List out any legal, regulatory, or business constraints that limit how the solution can be built.
- Be explicit about data privacy, geographic restrictions, and non-functional requirements (NFRs) like audit logging, history tracking, or data retention.

**Strong Examples:**
- "All financial data must be encrypted at rest and transit, complying with GDPR and PSD2. User consent must be explicitly gathered before processing data."
- "The system must keep an immutable log of all OTP verification attempts, including timestamps and device info, for 5 years."
- "The solution must conform to WCAG 2.1 AA accessibility standards for screen readers."

**Weak Examples:**
- "Make sure it's secure."
- "Keep logs of what happens."
- "Needs to be compliant with the law."

---

## Scope

### In Scope
**Rules:**
- List the specific use cases and user journeys that are required for this release to be considered complete.

**Strong Examples:**
- "Support for guest checkout via credit cards and Apple Pay in the US market only."
- "Push notifications and in-app messaging for abandoned cart reminders."

**Weak Examples:**
- "Checkout system."
- "Everything discussed in the brainstorming meeting."

### Out of Scope
**Rules:**
- Explicitly state what is *not* being built. This helps prevent scope creep and sets clear expectations with stakeholders.
- Mention if an out-of-scope item is planned for a future phase.

**Strong Examples:**
- "Support for Google Pay (planned for Phase 2). Multi-currency support (not currently planned)."
- "Automated email sequences (Marketing team is handling this manually for this launch)."

**Weak Examples:**
- Leaving this section blank.
- "Things we don't have time for."

---

## Dependencies and Impacts

**Rules:**
- Think holistically. How does this feature impact customer support, marketing, or other engineering teams?
- Identify external vendors or APIs that must be ready before launch.

**Strong Examples:**
- "We are dependent on the Risk team to provide the new fraud-scoring API endpoints by Oct 15th. CS needs updated macros for handling failed checkouts."
- "Marketing must define the new promotional copy before development begins, as character limits affect UI layout."
- "Adapter should implement the new API endpoints for the new fraud-scoring API endpoints first."

**Weak Examples:**
- "The Frontend team needs the Backend team to build the API." *(This is understood; focus on cross-functional impact).*
- "We depend on users to use the app."
