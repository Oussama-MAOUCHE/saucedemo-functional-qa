# Checkout / Order Flow — Post-Execution Review

## Execution checkpoint

The Checkout / Order Flow slice was formally recorded in Testiny after the underlying manual scenarios had already been executed and reviewed.

- Test run: `TR-4 — SauceDemo – Checkout / Order Flow – Initial Execution – 30-08-2026`
- Total test cases: 9
- Passed: 8
- Failed: 1
- Blocked: 0
- Skipped: 0
- Not Run: 0

The run combines a `standard_user` checkout baseline with one targeted `problem_user` defect-reproduction case. It was completed and closed after the results, execution comment, and Jira traceability were checked.

## Baseline result — standard_user

Eight `standard_user` scenarios passed within the focused checkout scope.

Coverage included:

- completing an order from Checkout Information through Checkout Complete;
- required-field validation with all customer-information fields empty;
- individual validation for missing First Name, Last Name, and Postal Code;
- cancelling from Checkout Information and returning to the Cart without losing the added product;
- cancelling from Checkout Overview and returning to Products while preserving the cart state;
- generating and opening the PDF order receipt after completion.

The order data remained internally consistent in the executed baseline. For the representative Backpack order, the item price was `$29.99`, the displayed tax was `$2.40`, and the displayed total was `$32.39`. The generated receipt matched the recipient, product, and displayed amounts used in the completed order.

This verifies consistency within the observed flow; it does not infer an undocumented tax rule or backend calculation method.

No confirmed functional defect was found for `standard_user` in the Checkout / Order Flow scenarios covered here.

## Confirmed finding — problem_user

One targeted `problem_user` scenario failed:

| Test case | Jira defect | Finding |
|---|---|---|
| TC-74 | SDQA-22 | Characters entered in Last Name modify First Name instead, leaving Last Name empty and preventing checkout from continuing |

The failure was kept as one defect model. Because Last Name remains empty, the subsequent `Error: Last Name is required` validation is consistent with the working `standard_user` baseline and is treated as a consequence of the input-routing failure rather than a separate validation defect.

Detailed reproduction steps, impact, and the supporting screen recording are maintained in Jira. Testiny records the failed execution, the concise actual-result comment, and the link to SDQA-22.

## Coverage boundaries and traceability

The Checkout slice does not duplicate the `error_user` checkout defects already formalized in the Targeted Special-User Addendum. Those cases remain traceable in the separate closed TR-3 run.

This checkpoint therefore serves two purposes:

- establish a working `standard_user` baseline for the main checkout flow;
- formalize the distinct `problem_user` Last Name failure without creating duplicate coverage for previously documented special-user behavior.

Evidence is kept in the tool where it adds the most value: execution history in Testiny, defect detail and video evidence in Jira, and a concise portfolio-level review here.

## Regression focus

A practical Checkout regression set should prioritize:

1. successful progression from Checkout Information to Checkout Complete;
2. required-field validation for First Name, Last Name, and Postal Code;
3. order data consistency on Checkout Overview;
4. cancellation from Checkout Information and Checkout Overview without losing cart contents;
5. completion-state behavior, including return to Products;
6. PDF receipt generation and consistency with the completed order.

The `problem_user` case remains useful for targeted confirmation testing of SDQA-22, but it should not replace the stable `standard_user` regression baseline.

## Automation candidate classification

### High-value regression automation

- TC-67 — checkout order completion using `standard_user`
- TC-68 to TC-71 — required-field validation using `standard_user`

These cases are deterministic, central to the purchase flow, and provide strong regression value once the Playwright layer is introduced.

### Automate soon

- TC-72 — cancel from Checkout Information
- TC-73 — cancel from Checkout Overview

These are stable state-preservation checks and are suitable once the core checkout path is automated.

### Keep manual for now

- TC-74 — targeted `problem_user` defect reproduction
- TC-75 — PDF receipt generation and content review

TC-74 reproduces known demo-specific abnormal behavior. TC-75 is valid automation material later, but download and document-content assertions are not the first priority while the core browser regression layer is still being established.

## Residual risk

This checkpoint does not establish correctness outside the tested Checkout scope. Remaining risks include:

- Navigation and Logout behavior;
- account-specific behavior outside the targeted scenarios already documented;
- cross-browser and cross-device compatibility;
- formal accessibility, security, performance, API, database, and backend behavior;
- undocumented input limits or business rules that cannot be inferred defensibly from the public UI.

No real payment processing or customer data is involved in this public demonstration environment.

## Conclusion

The Checkout / Order Flow slice is complete for the current manual functional-testing scope. The `standard_user` baseline covers the main completion, validation, cancellation, state-preservation, and receipt paths, while the distinct `problem_user` Last Name failure is traceable from Testiny to Jira.

The next manual QA checkpoint is Navigation / Logout.