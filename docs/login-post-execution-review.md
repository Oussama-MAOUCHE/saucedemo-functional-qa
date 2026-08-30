# Authentication / Login — Post-Execution Review

## Execution checkpoint

The Authentication / Login suite was formally executed in Testiny on **21 August 2026** in the primary environment defined in the Test Plan.

- Test run: `TR-1 — SauceDemo - Authentication / Login - Initial Execution - 21-08-2026`

| Result | Count |
|---|---:|
| Passed | 21 |
| Failed | 0 |
| Blocked | 0 |
| Skipped | 0 |
| Not Run | 0 |

All 21 recorded cases matched their expected results, so no Jira defect was created from TR-1.

The suite covered valid and invalid credentials, required-field validation, account states, input variations, direct access to a protected page while logged out, and recovery after a failed login.

## Selected execution evidence

Evidence was kept selective rather than attached to every passing case.

Representative evidence was retained for:

- TC-1 — successful login with `standard_user`;
- TC-2 — locked-out account handling;
- TC-7 — both credential fields empty;
- TC-20 — direct access to Inventory while logged out.

The closed Testiny run remains the formal execution record.

## Interpretation of the result

TR-1 establishes a working authentication baseline for the scenarios included in this slice. It does not establish performance, security, backend, cross-browser, or cross-device correctness.

One later finding is important for context: `performance_glitch_user` authenticated successfully in TR-1, so the related Login case correctly remained **Passed**. The visible delay associated with that account was investigated later in the Targeted Special-User Addendum and formalized separately as **SDQA-10**.

That later responsiveness finding does not change the recorded TR-1 authentication result.

## Regression focus

For a compact Authentication / Login regression set, the highest-value checks are:

1. `standard_user` can log in and reach the Products page.
2. `locked_out_user` is denied with the locked-account message.
3. A valid username with an incorrect password is denied.
4. Missing Username is rejected.
5. Missing Password is rejected.
6. Direct access to `/inventory.html` while logged out is denied.
7. A user can recover from a failed login by correcting the password without refreshing the page.

The remaining whitespace, case-sensitivity, long-input, and additional-account scenarios are still useful for broader functional coverage when authentication behavior changes.

## Automation candidates

### First regression candidates

- TC-1 — successful `standard_user` login
- TC-2 — locked-out account
- TC-3 — valid username with incorrect password
- TC-5 — missing Username
- TC-6 — missing Password
- TC-20 — protected Inventory access while logged out

These cases are stable, deterministic, and central to authenticated access, making them suitable for an initial Playwright regression slice.

### Add after the core set

- TC-4 — unrecognized username
- TC-7 — both credential fields empty
- TC-8 and TC-9 — username/password case sensitivity
- TC-10 to TC-13 — leading/trailing whitespace
- TC-16 to TC-19 — additional documented account types
- TC-21 — recovery after correcting a failed login

### Keep manual for now

- TC-14 — very long username
- TC-15 — very long password

These remain useful robustness checks, but they are lower-value early automation candidates because no field-length boundary was documented or observable.

This classification is about automation priority, not technical feasibility.

## Residual risk

The Login slice was executed in one primary desktop browser and environment. The result does not cover:

- cross-browser or cross-device compatibility;
- formal performance/load behavior;
- security testing;
- API, database, or backend correctness;
- undocumented authentication rules that cannot be established from the public interface.

## Related documents

- [Authentication / Login — Test Design](login-test-design.md)
- [Test Plan](test-plan.md)
- [Targeted Special-User Addendum](special-user-addendum-post-execution-review.md)

## Conclusion

The Authentication / Login slice is complete for the planned manual functional scope. TR-1 provides a clean baseline for core authentication behavior, while later account-specific findings remain separated into their own targeted investigations instead of being retroactively folded into this run.
