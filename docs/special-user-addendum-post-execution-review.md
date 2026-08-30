# Targeted Special-User Addendum — Post-Execution Review

## Purpose

After completing the main Inventory / Products checkpoint, I ran a bounded exploratory addendum against three additional SauceDemo accounts: `performance_glitch_user`, `error_user`, and `visual_user`.

The goal was not to repeat the full suite for every account. The addendum focused on behaviors that could expose different risk classes, including response delays, error handling, data consistency, visual consistency, form validation, and order completion.

## Execution checkpoint

The confirmed scenarios were formalized in Testiny after the underlying manual checks had already been executed and repeatedly reconfirmed.

- Test run: `TR-3 — SauceDemo – Special Users – Targeted Addendum – 29-08-2026`
- Total test cases: 10
- Failed: 10
- Passed: 0
- Blocked: 0
- Skipped: 0
- Not Run: 0

This is an intentionally defect-focused run. The 10/10 failure count should not be interpreted as an overall quality score for SauceDemo or as the result of a full regression suite.

## Confirmed findings

| Test case | Account | Jira defect | Finding |
|---|---|---|---|
| TC-57 | `performance_glitch_user` | SDQA-10 | Login completes only after a noticeable several-second delay |
| TC-58 | `error_user` | SDQA-11 | A non-default sort selection displays an explicit sorting error |
| TC-59 | `error_user` | SDQA-12 | Product descriptions are missing on Product Details |
| TC-60 | `error_user` | SDQA-13 | The Last Name field does not accept input during checkout |
| TC-61 | `error_user` | SDQA-14 | Checkout continues with Last Name empty and no validation message |
| TC-62 | `error_user` | SDQA-15 | Finish does not move the order to the completion state |
| TC-63 | `visual_user` | SDQA-16 | Product prices change after sorting and do not remain consistent with Product Details |
| TC-64 | `visual_user` | SDQA-17 | The first product card can display an unrelated image after sorting |
| TC-65 | `error_user` | SDQA-19 | Add to cart fails from a matching Product Details page |
| TC-66 | `error_user` | SDQA-20 | Remove fails from Product Details after the product was added successfully |

Detailed reproduction steps, impact, evidence, and defect relationships are maintained in Jira. Testiny records the formal execution result and the execution-to-defect link.

## Additional defect scope

The addendum also confirmed that `error_user` is affected by the same Products-page add/remove failure patterns already tracked in SDQA-5 and SDQA-6. Those Jira issues were extended with the additional affected-account evidence rather than duplicated as new defects.

No extra Testiny cases were added for those two extensions because the failure classes were already represented in the closed Inventory run. This keeps the addendum focused on distinct defect-reproduction scenarios rather than expanding the suite with duplicate coverage.

## Test-method notes

The addendum remained manual and black-box. Observed behavior was treated as the primary evidence, and defect grouping was based on the user-visible trigger, expected behavior, actual failure pattern, and relevant starting state.

One response-delay finding is included for `performance_glitch_user`, but this was not a load or performance test and no response-time SLA was assumed. It is documented only as a repeated user-visible responsiveness issue.

The special accounts were used as targeted test data, not as a basis for assuming what should fail. Account names or implementation intent were not used to define expected results.

## Automation decision

These addendum cases should stay manual for now. They mainly reproduce known abnormal behavior in a public demo environment.

The first Playwright work should still focus on stable regression flows such as successful login, standard product browsing, sorting, Product Details consistency, cart operations, and the stable Checkout baseline. The addendum cases remain useful for manual confirmation and defect traceability.

## Residual risk

This addendum was deliberately bounded. It does not represent exhaustive account-by-account regression and does not establish correctness for:

- Navigation and Logout;
- account-specific behavior outside the targeted scenarios;
- cross-browser or cross-device behavior;
- accessibility, security, API, database, or backend behavior;
- formal performance or load characteristics.

Some Checkout failures were discovered during the targeted `error_user` flow. They were formalized here without replacing the broader Checkout baseline, which was completed later as a separate checkpoint.

See: [`checkout-order-flow-post-execution-review.md`](checkout-order-flow-post-execution-review.md)

## Conclusion

The targeted special-user addendum is complete for the current portfolio scope. Ten reproducible scenarios are traceable from Testiny to Jira. Evidence for additional affected accounts was added to existing defects instead of creating duplicate tickets, and the stable baseline regression strategy remains separate from these defect-focused scenarios.
