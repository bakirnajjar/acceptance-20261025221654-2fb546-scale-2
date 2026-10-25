# Requirements analysis: customer password reset

Stage: `requirements_analysis` · Schema version: `1.0`

## Source references

- **S** — `user_story` / `user_story` / `characters 0-16000`: customer password reset story.
- **K1** — `knowledge` / `59efeb19-83f2-4ec6-bfd3-b4aeb7142930` / `v1, chunk 0`: account recovery standard, ACC-STD-01–03.
- **K2** — `knowledge` / `467a71ce-c5f8-4557-8f1e-a8ff1b01ecc3` / `v1, chunk 0`: identical account recovery standard, ACC-STD-01–03.

No attachments or approved prior outputs were supplied.

## Requirements

### REQ-001 — Sign-in reset entry point

The sign-in page offers a “Forgot password?” link that starts a password reset request.

- **Acceptance criterion:** Given the sign-in page, when a customer selects “Forgot password?”, then a password reset request starts.
- **Sources:** S; K1, K2 (ACC-STD-01).

### REQ-002 — Account-existence-neutral response

A password reset request returns an identical response whether the account exists or not.

- **Acceptance criterion:** Given otherwise equivalent reset requests for an existing and a nonexistent account, when each request is submitted, then their responses are identical.
- **Sources:** S; K1, K2 (ACC-STD-01).

### REQ-003 — Reset-request limit

Reset requests are limited to five per account per hour.

- **Acceptance criterion:** Given five reset requests for one account within an hour, when a sixth is made in that hour, then it is not accepted as another reset request for that account.
- **Sources:** S; K1, K2 (ACC-STD-01).

### REQ-004 — Single-use reset link

A reset link can be used only once.

- **Acceptance criterion:** Given a valid reset link used to complete a reset, when the same link is used again, then another reset cannot be completed with it.
- **Sources:** S; K1, K2 (ACC-STD-02).

### REQ-005 — Reset-link expiry

A reset link expires 30 minutes after issuance.

- **Acceptance criterion:** Given an issued reset link, when it is used at or after 30 minutes from issuance, then it cannot complete a reset.
- **Sources:** S; K1, K2 (ACC-STD-02).

### REQ-006 — Password reset completion

A customer can reset the account password with a valid reset link.

- **Acceptance criterion:** Given a valid, unused, unexpired reset link, when the customer completes the reset, then the account password is reset.
- **Sources:** S; K1, K2 (ACC-STD-02).

### REQ-007 — Sign out active sessions

Completing a password reset signs the account out of every active session.

- **Acceptance criterion:** Given an account with multiple active sessions, when its password reset completes, then none of those sessions remains signed in.
- **Sources:** S; K1, K2 (ACC-STD-02).

### REQ-008 — Notify account owner

The account owner is notified after every successful password reset.

- **Acceptance criterion:** Given a completed password reset, when it succeeds, then the account owner receives a notification for that reset.
- **Sources:** S; K1, K2 (ACC-STD-03).

## Assumptions

1. acceptance-20261025221654-2fb546-skill-sentinel — the acceptance skill produced this output.
2. Reset-link delivery mechanism is unspecified; verify link behavior without prescribing a delivery channel.
3. Owner-notification delivery mechanism is unspecified; require notification after each successful reset without prescribing a channel.
4. The response to a rate-limited request is unspecified; enforce the five-per-account-per-hour limit without prescribing error text, status, or presentation.
5. No new-password policy is supplied; do not add policy-specific requirements.

## Open questions (all non-blocking)

1. **How are password reset links delivered to customers?** Non-blocking. Assume no particular delivery channel; verify link behavior independently of delivery.
2. **How are successful-reset notifications delivered to account owners?** Non-blocking. Assume no particular delivery channel; require notification after every successful reset.
3. **What response should a rate-limited reset request receive?** Non-blocking. Assume no particular error text, status, or presentation; enforce only the specified request limit.
4. **What password policy applies to a new password?** Non-blocking. Assume no policy-specific rules beyond what is supplied; do not add password-policy requirements.
