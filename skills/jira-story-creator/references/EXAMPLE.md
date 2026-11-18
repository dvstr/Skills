# Examples

All decisions below are illustrative, not defaults for other products. These are demonstrations, not transcripts. Use the actual story's evidence and user decisions.

## 1. Clarify, then deliver a complete sign-in story

### Brief and available evidence

User: “Write the employee admin-panel sign-in story. Employees use email and a platform password.”

The supplied product notes already establish required email/password fields, platform-managed authentication, denial of incorrect credentials and suspension of either the employee or its organization. The form permits correction and resubmission after missing-field or incorrect-credential feedback. Suspension feedback explains that sign-in remains unavailable while the employee or organization is suspended; there is no self-service unsuspension in this story. They leave landing behavior and credential-error disclosure open. A separate current session decision establishes five minutes of inactivity or eight hours from creation, whichever comes first, enforced server-side; activity does not extend the maximum and session expiry does not expire credentials. Shared authorization is owned by the platform. There is no design artifact.

Reconcile the old source question “What are the session limits?” as answered. Do not ask it again or import account provisioning, password recovery or every security topic into this sign-in story.

### Clarification response

1. **Landing after sign-in:** Where should the employee arrive?
   - **A — Shared Welcome page:** Gives a consistent start, but requires navigation to a specific task.
   - **B — Originally requested permitted page:** Saves navigation, but needs a fallback decision.
   - **Recommendation:** Neither is preferable without the product's navigation goals.
2. **Credential-error disclosure:** How should incorrect credentials be reported?
   - **A — Generic response:** Reveals less account information, but gives users less troubleshooting detail.
   - **B — Distinct unknown-account and wrong-password errors:** Helps troubleshooting, but reveals whether an account exists.
   - **Recommendation:** A if limiting account enumeration is the priority. Applicable [OWASP authentication guidance](https://cheatsheetseries.owasp.org/cheatsheets/Authentication_Cheat_Sheet.html#authentication-and-error-messages) supports that security recommendation, not a product decision.
3. **Temporary authentication failure:** What should the employee be able to do?
   - **A — Submit another attempt:** Show a failure response and permit retrying, without a dedicated support workflow.
   - **B — Use a dedicated support route:** Adds escalation but requires an agreed route and owner.
   - **Recommendation:** A for this scope unless dedicated support is already required.
4. **Error presentation:** Who should decide the placement and wording of missing-field, credential, suspension and technical errors?
   - **A — Designer:** Keeps presentation consistent with the shared UI library, but leaves visual work to design.
   - **B — Specify it here:** Makes placement/copy explicit now, but needs those decisions before drafting.
   - **Recommendation:** A if design owns these interactions.

In an actual run, consult external guidance before claiming research; disclose if unavailable. Questions appear once in ordinary chat. Do not present the story until answered.

### User answers

“Use the Welcome page. Choose generic credential errors and allow another attempt after technical failure. The designer owns all error wording and placement, and other visual presentation, using the shared UI library. No dedicated design is planned. Account provisioning, password recovery and password changes are excluded. Keep session creation and expiry in this story. There are no first-use credential-expiry or first-sign-in password-change requirements for these employee accounts.”

These answers settle behavior and explicitly delegate presentation. They do not authorize extra lockout, MFA or support features.

### Complete description

## User Story

As an **employee with a platform account**,
I want **to sign in using my email and password**,
so that **I can access my permitted admin-panel work**.

## Context / Problem

Employees use platform-managed accounts for the admin panel. Shared authorization determines their permitted work. This story establishes sign-in and session lifetime.

## Functional Requirements

1. **FR-1: Credentials.** Require email and password. A submission with either field empty cannot authenticate and receives missing-field feedback while allowing correction and resubmission.
2. **FR-2: Credential verification.** Authenticate against the platform account. Incorrect credentials deny sign-in with the same generic response for unknown email and incorrect password; allow correction and resubmission.
3. **FR-3: Suspension.** Deny sign-in and show suspension feedback when the employee or its organization is suspended, including when credentials are otherwise correct. Feedback explains that sign-in remains unavailable while either suspension applies; no self-service unsuspension is offered.
4. **FR-4: Successful sign-in.** For correct credentials and no applicable suspension, create a session and open the shared Welcome page.
5. **FR-5: First-use age.** Account credentials have no first-use expiry.
6. **FR-6: First-login password.** Sign-in requires no first-login password change.
7. **FR-7: Technical failure.** When authentication is temporarily unavailable, create no session, show a technical-failure response and allow another attempt.
8. **FR-8: Session lifetime.** Expire the session after five minutes of inactivity or eight hours from creation, whichever comes first. Activity cannot extend the maximum. An expired session cannot authorize protected access; credentials remain usable subject to FR-2–FR-3.

## Technical Requirements

1. **TR-1: Session enforcement.** Enforce FR-8 server-side.

## Design Notes

No dedicated design is planned. The shared UI library is the established platform design baseline, not a new story-specific constraint. The designer owns wording and placement of feedback in FR-1–FR-3 and FR-7, plus other visual presentation. The behavior remains defined in those requirements.

## Out of Scope

- Account provisioning.
- Password recovery and password changes.

## Acceptance Criteria

### Happy path

#### AC-1: Session creation (FR-2, FR-3, FR-4)

- **Given** correct credentials and neither employee nor organization suspension
- **When** the employee submits those credentials
- **Then** an authenticated session is created.

#### AC-2: Successful landing (FR-4)

- **Given** correct credentials and neither employee nor organization suspension
- **When** the employee submits those credentials
- **Then** the Welcome page opens.

#### AC-3: No first-login password change (FR-6)

- **Given** an eligible employee has never signed in
- **When** the employee submits correct credentials
- **Then** no first-login password change is required.

#### AC-4: Sign in after session expiry (FR-2, FR-3, FR-4, FR-8)

- **Given** the earlier session expired and the employee remains eligible
- **When** the employee submits the same correct credentials again
- **Then** a new authenticated session is created.

### Edge cases

#### AC-5: Previously unused credentials (FR-5)

- **Given** an eligible employee has correct credentials issued long ago that have never been used
- **When** the employee submits them for the first time
- **Then** sign-in succeeds regardless of credential age.

This unusual long-unused starting state checks the explicit no-expiry rule; ordinary first sign-in is covered above. No age threshold is implied.

### Error states

#### AC-6: Rejected authentication attempt (FR-1, FR-2, FR-3)

- **Given** credentials are missing or incorrect, or the employee or organization is suspended
- **When** the employee submits the sign-in attempt
- **Then** no authenticated session is created.

Run each missing-field, incorrect-credential and suspension case named below separately. These cases share this denial outcome; their feedback and recovery differ.

#### AC-7: Missing credentials (FR-1)

- **Given** one or both credential fields are empty
- **When** the employee submits
- **Then** missing-field feedback identifies the required credentials that are absent.

Run email-only missing, password-only missing and both-empty cases separately.

#### AC-8: Incorrect credentials (FR-2)

- **Given** the email is unknown or the password is incorrect
- **When** the employee submits the credentials
- **Then** the same generic rejection feedback is shown without disclosing which credential failed.

Run unknown-email and wrong-password cases separately.

#### AC-9: Correct and resubmit credentials (FR-1, FR-2)

- **Given** a submission contains missing or incorrect credentials
- **When** the employee submits the attempt
- **Then** the form remains available for correcting the credentials and submitting another attempt.

Run the missing-field and incorrect-credential cases separately.

#### AC-10: Suspended access (FR-3)

- **Given** the employee or its organization is suspended
- **When** the employee submits otherwise correct credentials
- **Then** suspension feedback explains that sign-in is unavailable while suspension applies, with no self-service unsuspension offered.

Run employee-only, organization-only and both-suspended cases separately.

#### AC-11: Technical-failure recovery option (FR-7)

- **Given** authentication is temporarily unavailable
- **When** an employee submits otherwise correct credentials
- **Then** technical-failure feedback makes another attempt available.

#### AC-12: No session on technical failure (FR-7)

- **Given** authentication is temporarily unavailable
- **When** an employee submits otherwise correct credentials
- **Then** no session is created.

#### AC-13: Successful retry (FR-4, FR-7)

- **Given** an earlier attempt failed technically and authentication is available again
- **When** an eligible employee submits correct credentials again
- **Then** an authenticated session is created.

### Non-functional criteria

#### AC-14: Active session within limits (FR-8, TR-1)

- **Given** a session is younger than eight hours and has been inactive for less than five minutes, with no other access restriction
- **When** it is used for a permitted protected request
- **Then** neither lifetime limit prevents access.

Include requests immediately below each limit, keeping the other limit unexpired.

#### AC-15: Inactivity limit (FR-8, TR-1)

- **Given** a session has been inactive for five minutes or longer
- **When** it is used for a protected request
- **Then** the server denies access because the session has expired.

Verify at exactly five minutes and after it, independently of the maximum lifetime.

#### AC-16: Maximum lifetime (FR-8, TR-1)

- **Given** a session is eight hours old or older despite continued activity
- **When** it is used for a protected request
- **Then** the server denies access because the session has expired.

Verify at exactly eight hours and after it, keeping inactivity below five minutes.

## 2. Coherent FRs and chronology

Illustrative list decisions: an administrator opens a directory; first page is shown with Previous/Next controls. A separately agreed selector offers 25/50/100 rows, initially 25. Changing size returns to page one.

Opening the list, seeing several records, changing page size and navigating again are normal successful behavior, not edge cases solely because they involve multiple records or repeated actions. Keep page navigation and size selection as distinct FRs because they can change independently. Test the selector's options/default when opening the list, and its reload/reset behavior when changing size. Do not make “the selector offers 25/50/100” a new result of navigating to the next page.

Search/filter/sort questions from a source remain questions until resolved. Exclude them only when agreed; do not replace them with unrelated profile-management exclusions.

## 3. Provisioning and corrections

Illustrative decisions: an installation routine creates the first workspace before projects exist. Its established model requires a nonblank name and supported region; its initial status is Active. The user confirms repeat runs preserve an existing workspace.

Verify initial persisted values and a separate repeat-run path. Do not test a future settings screen. Removing an impossible first-installation collision with a project does not remove name/region validation or initial Active state.

If the user also requires a workspace property whose verification belongs to a later capability, retain the property and the established verification ownership. Do not claim those tests already exist without evidence. A correction excluding later management changes that workflow boundary, not every property of the created entity.

## 4. An explicitly requested provisional draft

User: “Draft now; I will decide resend and expiry later.”

Draft only established OTP behavior. Put the resend/expiry questions in the relevant section, visibly label the draft and omit guessed expiry durations, attempt limits, invalidation policies and their ACs. An unselected recommendation is not a decision. Without the early-draft request, ask material questions before delivering the description.

## 5. Classify the scenario, not the requirement

Illustrative search decisions: valid input enables Search; empty/invalid input disables it; a successful search lists matching records; an unavailable service shows failure feedback and offers retry.

- **Happy path:** Valid input enables Search; successful searches return one or several records. These are normal prerequisites and successful variations.
- **Edge cases:** Empty or invalid input keeps Search disabled. Name the boundary/input case explicitly.
- **Error states:** A submitted search fails because the service is unavailable; verify the feedback and retry path. Missing-field feedback after a submitted sign-in attempt above is also a failed-operation scenario, unlike pre-submit enablement.
- **Non-functional criteria:** Verify a measurable quality obligation only if established for this story. In the sign-in example, the session-limit tests verify the explicitly specified security lifetime policy, even though their data also includes boundaries; they are not duplicated under Edge cases.

For a creation-date sorting criterion, two records with distinct creation dates can show the ordering. Do not add several record types or conflicting status dates unless those distinctions are needed to test an established rule. These are illustrative cases, not additional product requirements.
