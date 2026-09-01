# Inventory / Products — Post-Execution Review

## Execution checkpoint

TR-2 formally records the Inventory / Products scenarios that had already been executed manually and repeatedly reconfirmed.

- Test run: `TR-2 — SauceDemo – Inventory / Products – Initial Execution – 24-08-2026`
- Closed: **24 August 2026, 18:55**
- Total test cases: 14
- Passed: 5
- Failed: 9
- Blocked: 0
- Skipped: 0
- Not Run: 0

The run combines five `standard_user` baseline cases with nine targeted `problem_user` defect-reproduction cases. Its 5 Passed / 9 Failed result is therefore not an overall product-quality score.

All nine failed cases are linked to confirmed Jira defects.

## Working baseline — standard_user

The five formal baseline cases passed and covered:

- all available product-sorting options;
- Products → Product Details name and price consistency;
- adding a product from Products and confirming it in the Cart;
- removing an added product from Products;
- adding and removing a product from Product Details.

The broader baseline exploration also checked Cart data consistency, **Back to products** / **Continue Shopping** navigation, and Cart-state persistence through navigation and page refresh. These exploratory checks are not included in the 14-case TR-2 count.

No confirmed functional defect was found for `standard_user` within this Inventory / Products scope.

Two visible content anomalies were retained as observations rather than defects because no requirement supported a stronger classification:

- `carry.allTheThings()` wording in the Sauce Labs Backpack description;
- `Test.allTheThings() T-Shirt (Red)` as a product name.

## Confirmed defect reproductions — problem_user

Nine targeted cases failed:

| Test case | Jira | Finding |
|---|---|---|
| TC-48 | SDQA-4 | All six product cards display the same incorrect image |
| TC-49 | SDQA-3 | Non-default sorting options cannot be applied |
| TC-50 | SDQA-1 | Selecting a product opens details for a different product |
| TC-51 | SDQA-2 | Sauce Labs Fleece Jacket opens an `ITEM NOT FOUND` state with an invalid price |
| TC-52 | SDQA-5 | Add to cart from Products fails for some products |
| TC-53 | SDQA-6 | Remove from Products fails for successfully added products |
| TC-54 | SDQA-7 | Add to cart fails from some valid Product Details pages |
| TC-55 | SDQA-8 | Remove fails from Product Details after a successful add |
| TC-56 | SDQA-9 | `ITEM NOT FOUND` increments the Cart badge without adding a visible Cart item |

The defects are separated by observable failure pattern rather than an assumed implementation cause.

This table reflects the `problem_user` reproductions recorded in TR-2. Later targeted testing added `error_user` as an additional affected account to SDQA-5 through SDQA-8 where the same failure classes were confirmed; the original TR-2 results and links remain unchanged.

## Evidence and traceability

The closed Testiny report records all 14 results and the nine Jira links. Jira remains the detailed defect record; GitHub keeps the portfolio-level interpretation instead of duplicating the full execution and evidence set.

## Regression focus

A compact Inventory / Products regression set should prioritize:

1. All sorting options reorder the list correctly and retain the selected option.
2. Selecting a product opens the corresponding Product Details page.
3. Product name and price remain consistent between Products and Product Details.
4. A product added from Products appears in the Cart with consistent data.
5. Removing a product from Products updates the Cart state correctly.
6. Add and Remove work from Product Details.
7. Cart badge count remains consistent with visible Cart contents.
8. Cart state remains stable through normal in-app navigation and page refresh.

Known special-account defect reproductions remain useful for confirmation testing, but they do not replace the stable `standard_user` regression baseline.

## Automation candidates

### First regression candidates

- TC-43 — sorting with all available options
- TC-44 — selected product opens the corresponding Product Details page
- TC-45 — add to cart from Products
- TC-46 — remove from Products
- TC-47 — add and remove from Product Details

These cases are deterministic, central to the shopping flow, and suitable for an early Playwright regression slice.

### Keep manual for now

- TC-48 to TC-56 — targeted `problem_user` defect reproductions

They remain useful for defect confirmation and portfolio traceability, but the public demo project has no controlled fix cycle. Early automation is better spent on stable regression behavior than on encoding known demo-specific failures.

## Scope and residual risk

This review covers the Inventory / Products checkpoint only. Checkout, order completion, and Navigation / Logout were tested separately, while the later Special-User Addendum expanded account-specific coverage without becoming a full regression suite for every account.

Broader project-level limits — cross-browser/device compatibility, formal accessibility, performance/load, security penetration testing, API/backend testing, database testing, and undocumented business rules — are documented in the [Test Plan](test-plan.md).

SauceDemo is a public demonstration/training application. These findings are black-box portfolio results, not production defects discovered for a client.

## Related documents

- [Test Plan](test-plan.md)
- [Targeted Special-User Addendum](special-user-addendum-post-execution-review.md)
- [Checkout / Order Flow review](checkout-order-flow-post-execution-review.md)
- [Navigation / Logout review](navigation-logout-post-execution-review.md)

## Conclusion

TR-2 establishes a stable `standard_user` Inventory / Products baseline and traceable `problem_user` defect reproductions. Later account-specific findings remain documented separately instead of being folded back into the original run.
