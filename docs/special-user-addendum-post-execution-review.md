# Targeted Special-User Addendum — Post-Execution Review

## Purpose

After the main Inventory / Products checkpoint, I used three additional SauceDemo accounts for a bounded follow-up: `performance_glitch_user`, `error_user`, and `visual_user`.

This was not a full regression pass for each account. I focused on behaviors that could expose different failure patterns in responsiveness, sorting, Product Details, cart actions, checkout validation, order completion, pricing, and product imagery.

## Execution checkpoint

The confirmed scenarios were formalized in Testiny after the underlying manual checks had already been executed and reconfirmed.

- Test run: `TR-3 — SauceDemo – Special Users – Targeted Addendum – 29-08-2026`
- Total test cases: 10
- Failed: 10
- Passed: 0
- Blocked: 0
- Skipped: 0
- Not Run: 0
- Run status: Closed

All 10 cases were deliberately selected to formalize already-confirmed failures. The 10/10 Failed result is therefore **not** a product-quality score and should not be read as the result of a full regression suite.

## Confirmed findings

| Test case | Account | Jira | Finding |
|---|---|---|---|
| TC-57 | `performance_glitch_user` | SDQA-10 | Login reaches Products only after a noticeable several-second delay |
| TC-58 | `error_user` | SDQA-11 | Selecting a non-default sort option displays an explicit sorting error |
| TC-59 | `error_user` | SDQA-12 | Product descriptions are missing on Product Details |
| TC-60 | `error_user` | SDQA-13 | The Last Name field does not accept input during checkout |
| TC-61 | `error_user` | SDQA-14 | Checkout continues with Last Name empty and no validation message |
| TC-62 | `error_user` | SDQA-15 | Selecting Finish produces no visible effect and does not move the order to completion |
| TC-63 | `visual_user` | SDQA-16 | Product prices on Products become inconsistent with downstream product prices |
| TC-64 | `visual_user` | SDQA-17 | The first product card can display an unrelated image after sorting |
| TC-65 | `error_user` | SDQA-19 | Add to cart fails from a valid Product Details page |
| TC-66 | `error_user` | SDQA-20 | Remove fails from Product Details after the item was added successfully |

Testiny keeps the execution result and Jira link for each representative case. Jira remains the detailed defect record for reproduction steps, affected examples, impact, relationships, and supporting evidence.

## How related failures were handled

The addendum did not create a new ticket every time another account showed an already-known failure pattern.

For `error_user`, the Products-page Add and Remove failures matched the existing observable patterns tracked in **SDQA-5** and **SDQA-6**. Those issues were extended with the additional affected-account evidence instead of being duplicated.

The Product Details Add and Remove failures were represented separately in this addendum by **TC-65 / SDQA-19** and **TC-66 / SDQA-20**.

This keeps the defect model based on the observable trigger and failure pattern rather than on account name alone.

## Responsiveness finding

TC-57 is the representative Testiny case for `performance_glitch_user`, but SDQA-10 was supported by repeated delays across several user actions:

- Login → Products;
- applying a sorting option;
- Product Details → Back to products;
- Checkout Overview → Cancel.

This is documented as a user-visible responsiveness defect. It was **not** a formal performance or load test, no response-time SLA was available, and no backend cause is inferred.

## Test-method notes

The follow-up remained manual and black-box. Expected behavior came from the visible application flow, supplied demo data, internal consistency, and the same functional expectations used elsewhere in the project.

The account names were treated only as test data. They were not used as evidence that a behavior was expected to fail.

The addendum was intentionally bounded: once the distinct confirmed failure patterns were formalized and traceable, I did not repeat the full baseline suite for every special account.

## Automation priority

These 10 cases stay manual for now because they mainly reproduce known demo-specific failures.

The first Playwright work should focus on stable regression behavior instead: successful Login, product browsing and sorting, Product Details consistency, cart operations, the stable Checkout flow, and Logout.

The addendum remains useful for manual confirmation if the public demo behavior changes or if a later fix/retest cycle becomes relevant.

## Scope and residual risk

This addendum does not establish account-by-account correctness outside the targeted scenarios. It also does not cover:

- cross-browser or cross-device compatibility;
- formal accessibility testing;
- performance and load testing;
- security penetration testing;
- API/backend testing;
- database testing.

Checkout and Navigation / Logout were completed later as separate checkpoints rather than folded into this defect-focused run.

## Related documents

- [Inventory / Products review](inventory-post-execution-review.md)
- [Checkout / Order Flow review](checkout-order-flow-post-execution-review.md)
- [Navigation / Logout review](navigation-logout-post-execution-review.md)
- [Test Plan](test-plan.md)

## Conclusion

The targeted special-user follow-up is complete for the planned manual scope. TR-3 provides traceability for 10 representative defect reproductions, while repeated instances of the same failure class were consolidated instead of being turned into duplicate cases or tickets.
