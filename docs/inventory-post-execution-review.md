# Inventory / Products — Post-Execution Review

## Execution checkpoint

The Inventory / Products suite was formally recorded in Testiny on 24 August 2026 after the underlying manual scenarios had already been executed and repeatedly reconfirmed.

- Test run: `TR-2 — SauceDemo – Inventory / Products – Initial Execution – 24-08-2026`
- Total test cases: 14
- Passed: 5
- Failed: 9
- Blocked: 0
- Skipped: 0
- Not Run: 0

The run intentionally combines a `standard_user` baseline with targeted `problem_user` defect-reproduction scenarios. The 5/14 pass count should therefore not be interpreted as an overall quality score for SauceDemo.

## Baseline result — standard_user

The five baseline scenarios passed:

- product sorting using all available options;
- Products → Product Details consistency;
- add to cart from the Products page;
- remove from the Products page;
- add and remove from Product Details.

Within this focused Inventory scope, no confirmed functional defect was found for `standard_user`.

## Confirmed defects — problem_user

Nine targeted scenarios failed and were linked to confirmed Jira defects:

| Test case | Jira defect | Summary |
|---|---|---|
| TC-48 | SDQA-4 | All product images display the same incorrect image |
| TC-49 | SDQA-3 | Non-default sorting options cannot be applied |
| TC-50 | SDQA-1 | Selecting a product opens details for a different product |
| TC-51 | SDQA-2 | Sauce Labs Fleece Jacket opens an `ITEM NOT FOUND` state with an invalid price |
| TC-52 | SDQA-5 | Add to cart from the Products page fails for some products |
| TC-53 | SDQA-6 | Remove from the Products page does not remove successfully added products |
| TC-54 | SDQA-7 | Add to cart from some displayed Product Details pages fails |
| TC-55 | SDQA-8 | Remove from successfully added Product Details items fails |
| TC-56 | SDQA-9 | `ITEM NOT FOUND` can create a cart badge count without a visible cart item |

The defect grouping is based on observable behavior rather than assumed implementation or root cause. Detailed reproduction steps and supporting evidence are maintained in Jira, while Testiny preserves the execution-to-defect traceability.

## Selected portfolio evidence

Evidence was kept selective and tied to the defects rather than duplicated across tools.

- The closed Testiny TR-2 report records all 14 results and the nine Jira links.
- Jira contains the detailed defect reports and supporting screenshots or short videos for SDQA-1 through SDQA-9.
- No additional evidence was added to passing Inventory cases because the baseline behavior had already been repeatedly confirmed and the portfolio does not need evidence for every pass.

## Regression focus

A compact Inventory regression set should prioritize the main product-browsing and cart-entry flow:

1. All sorting options reorder products correctly and keep the selected option visible.
2. Selecting a product opens the corresponding Product Details page.
3. Product name and price remain consistent between Products and Product Details.
4. A product can be added from the Products page and appears in the Cart with the correct data.
5. A product can be removed from the Products page and the cart state updates correctly.
6. A product can be added and removed from Product Details.
7. Cart badge count remains consistent with visible Cart contents.

The `problem_user` scenarios remain useful for targeted confirmation testing of the linked defects, but they should not replace the stable `standard_user` regression baseline.

## Automation candidate classification

### High-Value Regression Automation

- TC-43 — product sorting using all available options
- TC-44 — selected product opens the corresponding Product Details page
- TC-45 — add to cart from the Products page
- TC-46 — remove from the Products page
- TC-47 — add and remove from Product Details

These cases are stable, deterministic, central to the shopping flow, and suitable for an early Playwright regression slice.

### Keep Manual

- TC-48 to TC-56 — targeted `problem_user` defect-reproduction scenarios

These cases are valuable for defect verification and portfolio evidence, but they are not the best first automation investment. The current project has no real fix cycle for the public demo application's special account behavior, so early automation should focus on stable business flows rather than codifying known demo-specific failures.

### Automate Soon

None beyond the five baseline cases already classified as high-value regression candidates.

### Not Worth Automating Yet

None are permanently excluded. The current decision is about priority and portfolio value, not technical feasibility.

## Residual risk

This checkpoint does not establish correctness outside the tested Inventory scope. Remaining risks include:

- checkout and order-completion behavior;
- navigation and session flows outside the Inventory scenarios;
- broader special-account behavior not covered by a targeted charter;
- cross-browser and cross-device compatibility;
- accessibility, performance, security, API, database, and backend correctness.

The application is also a public demonstration environment, and some provided accounts intentionally expose abnormal behavior. The portfolio therefore documents black-box findings accurately without presenting Sauce Labs as a client or implying that these are production defects discovered on a customer system.

## Conclusion

The Inventory / Products slice is complete for the current manual functional-testing scope. The baseline behavior for `standard_user` is documented, nine reproducible `problem_user` defects are traceable from Testiny to Jira, and the highest-value stable Inventory flows have been identified for later Playwright automation.
