# Evidence-to-requirement map (T001)

## Authorized evidence

- **S** — `{source_type: user_story, source_id: user_story, locator: "characters 0-16000"}`: “As a customer I want to reset my password. Apply the curated recovery standard.” Complete; no end marker.
- **K1** — `{source_type: knowledge, source_id: 59efeb19-83f2-4ec6-bfd3-b4aeb7142930, locator: "v1, chunk 0"}`: Account recovery standard v1, ACC-STD-01–03.
- **K2** — `{source_type: knowledge, source_id: 467a71ce-c5f8-4557-8f1e-a8ff1b01ecc3, locator: "v1, chunk 0"}`: Same relevant standard, independently returned. Cite **both** knowledge references on each applicable requirement.
- Attachments and approved prior outputs: none.

## Atomic requirement candidates

| ID | Observable behavior | Given/When/Then acceptance check | Evidence |
| --- | --- | --- | --- |
| REQ-001 | Sign-in page offers a “Forgot password?” link starting a reset request. | Given the sign-in page, when a customer selects “Forgot password?”, then a password reset request starts. | S; K1, K2 (ACC-STD-01) |
| REQ-002 | A reset request returns the same response whether the account exists or not. | Given otherwise equivalent requests for an existing and a nonexistent account, when each is submitted, then the responses are identical. | S; K1, K2 (ACC-STD-01) |
| REQ-003 | Reset requests are limited to five per account per hour. | Given five reset requests for one account within an hour, when a sixth is made in that hour, then it is not accepted as another reset request for that account. | S; K1, K2 (ACC-STD-01) |
| REQ-004 | A reset link is single-use. | Given a valid link used to complete a reset, when the same link is used again, then another reset cannot be completed with it. | S; K1, K2 (ACC-STD-02) |
| REQ-005 | A reset link expires 30 minutes after issuance. | Given an issued link, when it is used at or after 30 minutes from issuance, then it cannot complete a reset. | S; K1, K2 (ACC-STD-02) |
| REQ-006 | A customer can complete a password reset using a valid reset link. | Given a valid, unused, unexpired link, when the customer completes the reset, then the account password is reset. | S; K1, K2 (ACC-STD-02) |
| REQ-007 | Completing a reset signs the account out of every active session. | Given an account with multiple active sessions, when a reset completes, then none of those sessions remains signed in. | S; K1, K2 (ACC-STD-02) |
| REQ-008 | The account owner is notified after every successful reset. | Given a completed reset, when it succeeds, then the account owner receives a notification for that reset. | S; K1, K2 (ACC-STD-03) |

## Assumptions and non-blocking questions for T002

- `acceptance-20261025221654-2fb546-skill-sentinel` — the acceptance skill produced this evidence map.
- **Question:** How are reset links delivered? **Assumption:** Delivery mechanism is unspecified; test link behavior without prescribing a channel.
- **Question:** How are owner notifications delivered? **Assumption:** Require notification after each success without prescribing a channel.
- **Question:** What response follows a rate-limited request? **Assumption:** Only the five-per-account-per-hour limit is specified; do not prescribe error text, status, or presentation.
- **Question:** What password policy applies to the new password? **Assumption:** No policy is supplied; do not add policy-specific requirements.

The supplied assessment agrees with this scope. The stated approved `plan.md` was not present at the supplied path during T001; this map does not create or replace it.
