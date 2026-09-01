# Checkout / Order Flow — Post-Execution Review

## Execution checkpoint

TR-4 formalizes the Checkout / Order Flow scenarios that had already been executed manually and reviewed.

- Test run: `TR-4 — SauceDemo – Checkout / Order Flow – Initial Execution – 30-08-2026`
- Run status: Closed
- Total test cases: 9
- Passed: 8
- Failed: 1
- Blocked: 0
- Skipped: 0
- Not Run: 0

The run contains eight `standard_user` baseline cases and one targeted `problem_user` defect-reproduction case.

## Working baseline — standard_user

The eight passing cases cover the main checkout path and its most important validation/state checks:

- completing an order through Checkout Information, Checkout Overview, and Checkout Complete;
- validation when all customer-information fields are empty;
- individual required-field validation for First Name, Last Name, and Postal Code;
- cancelling from Checkout Information and returning to the Cart without losing the added product;
- cancelling from Checkout Overview and returning to Products while preserving the Cart state;
- generating and opening the PDF order receipt after completion.

For the representative Backpack order, the displayed item price was `$29.99`, tax was `$2.40`, and the total was `$32.39`. The generated receipt matched the recipient, product, and displayed amounts from the completed order.

The figures are internally consistent within the observed flow. No undocumented tax rule or backend calculation method is inferred from them.

The completion flow also cleared the cart badge, and **Back Home** returned to Products with the Cart empty.

No confirmed functional defect was found for `standard_user` in the Checkout / Order Flow scenarios covered here.

## Confirmed defect reproduction — problem_user

One targeted case failed:

| Test case | Jira | Finding |
|---|---|---|
| TC-74 | SDQA-22 | Characters entered in Last Name modify First Name instead, leaving Last Name empty and preventing checkout from continuing |

In the representative reproduction, First Name accepts input normally. While Last Name is focused, typing `Tester` changes the First Name value instead of populating Last Name. Last Name remains empty. Postal Code accepts `19580`, and clicking **Continue** keeps the user on Checkout Information with:

`Error: Last Name is required`

This is treated as one defect model. The validation message itself is consistent with the verified `standard_user` baseline because Last Name is still empty; it is therefore a consequence of the input-routing failure rather than a second `problem_user` validation defect.

The `problem_user` behavior is also kept separate from the `error_user` Last Name failure already documented in the Targeted Special-User Addendum because the observable failure patterns are different.

## Evidence and traceability

Testiny keeps the formal execution result, the concise Actual comment for TC-74, and the link to SDQA-22. Jira remains the detailed defect record, including reproduction information, impact, relationships, and supporting evidence.

The previously formalized `error_user` Checkout findings remain in the separate TR-3 addendum and are not duplicated in this Checkout run.

GitHub keeps the portfolio-level interpretation rather than copying the full Testiny or Jira records.

## Regression focus

A compact Checkout regression set should prioritize:

1. completing the main order flow from Checkout Information to Checkout Complete;
2. required-field validation for First Name, Last Name, and Postal Code;
3. product and amount consistency on Checkout Overview;
4. cancellation from Checkout Information without losing the Cart item;
5. cancellation from Checkout Overview while preserving the Cart state;
6. completion-state behavior, including the cleared cart badge and return to Products;
7. PDF receipt generation and consistency with the completed order.

The `problem_user` case remains useful for targeted confirmation of SDQA-22, but it should not replace the stable `standard_user` regression baseline.

## Automation candidates

### First regression candidates

- TC-67 — checkout order completion using `standard_user`
- TC-68 to TC-71 — required-field validation using `standard_user`

These cases are deterministic and central to the purchase flow, making them strong early Playwright candidates.

### Add after the core set

- TC-72 — cancel from Checkout Information
- TC-73 — cancel from Checkout Overview

These are stable state-preservation checks and are suitable once the core completion and validation paths are automated.

### Keep manual for now

- TC-74 — targeted `problem_user` defect reproduction
- TC-75 — PDF receipt generation and content review

TC-74 reproduces known demo-specific abnormal behavior. TC-75 is also automatable, but download handling and document-content assertions are lower priority than the core browser regression flow at this stage.

This is an automation-priority decision, not a statement that these cases cannot be automated.

## Scope and residual risk

This checkpoint is limited to the planned Checkout / Order Flow functional scope. It does not cover:

- cross-browser or cross-device compatibility;
- formal accessibility testing;
- performance and load testing;
- security penetration testing;
- API/backend testing;
- database testing;
- undocumented business rules that cannot be established from the public interface.

No real payment processing or customer data is involved in this public demonstration environment.

Navigation / Logout was completed later as a separate checkpoint rather than being folded into this review.

## Related documents

- [Test Plan](test-plan.md)
- [Targeted Special-User Addendum](special-user-addendum-post-execution-review.md)
- [Navigation / Logout review](navigation-logout-post-execution-review.md)

## Conclusion

The Checkout / Order Flow checkpoint is complete for the planned manual functional scope. TR-4 provides a working `standard_user` checkout baseline and a traceable `problem_user` failure in SDQA-22, while previously documented special-user Checkout defects remain separated in their own targeted run.