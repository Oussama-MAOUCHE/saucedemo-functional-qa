# Authentication / Login — Post-Execution Review

## Execution checkpoint

The Authentication / Login test suite was executed in Testiny on 21 August 2026.

- Total test cases: 21
- Passed: 21
- Failed: 0
- Blocked: 0
- Skipped: 0
- Pass rate: 100%

No defect was created from this run because the observed results matched the expected results for all executed test cases.

## Selected portfolio evidence

Evidence was intentionally kept selective rather than capturing every passing test.

- TC-1 — successful login with `standard_user`
- TC-2 — locked-out account handling
- TC-7 — validation when both credential fields are empty
- TC-20 — direct access to a protected Inventory URL while logged out

The full Testiny execution report is retained as the formal execution artifact.

## Regression focus

A compact Authentication / Login regression set should prioritize the behaviors most likely to affect access to the application or prevent a user from continuing the main journey.

Recommended regression checks:

1. Valid `standard_user` login reaches the Products page.
2. `locked_out_user` is denied with the expected locked-account message.
3. Valid username with incorrect password is denied.
4. Missing username is rejected with the required-username message.
5. Missing password is rejected with the required-password message.
6. Direct access to `/inventory.html` while logged out is denied and redirected to Login.
7. A user can recover from a failed login by correcting the password without refreshing the page.

The remaining input-variation and special-account cases remain useful for broader functional coverage and targeted regression when authentication behavior changes.

## Automation candidate classification

The suite was reviewed using four categories: Keep Manual, Automate Soon, High-Value Regression Automation, and Not Worth Automating Yet.

### High-Value Regression Automation

- TC-1 — standard successful login
- TC-2 — locked-out account
- TC-3 — valid username with incorrect password
- TC-5 — missing username
- TC-6 — missing password
- TC-20 — unauthenticated direct access to Inventory

These cases are stable, deterministic, business-relevant, and inexpensive to validate repeatedly. They are strong first candidates for Playwright automation once automation work begins.

### Automate Soon

- TC-4 — unrecognized username
- TC-7 — both fields empty
- TC-8 — username case sensitivity
- TC-9 — password case sensitivity
- TC-10 to TC-13 — leading/trailing whitespace handling
- TC-16 to TC-19 — successful authentication for the additional documented account types
- TC-21 — recovery after correcting a failed login

These cases are repeatable and automatable, but they provide less incremental value than the high-value regression set for an initial automation slice.

### Keep Manual

- TC-14 — very long username
- TC-15 — very long password

These robustness checks are useful during exploratory or targeted validation, but they are lower priority for early automation because no documented field-length boundary exists and the current value is mainly defensive exploration.

### Not Worth Automating Yet

None of the current 21 cases needs to be permanently excluded from automation. The distinction is priority, not feasibility. The first automation slice should remain intentionally small and focus on the highest-value authentication regression behaviors.

## Residual risk

The Authentication / Login slice passed in the primary test environment, but this does not establish cross-browser, cross-device, performance, security, or backend correctness. Those areas remain outside the current project scope unless the test plan is explicitly expanded.

## Conclusion

The Authentication / Login slice is complete for the current manual functional-testing scope. The project should now move to the next SauceDemo functional area rather than expanding Login coverage for its own sake.
