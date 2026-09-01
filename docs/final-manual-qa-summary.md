# SauceDemo — Final Manual QA Summary

## Summary

This project covered a risk-based manual black-box QA cycle for SauceDemo, a public e-commerce demonstration application.

The planned functional scope was completed across Authentication / Login, Inventory / Products, Product Details, sorting, Cart behavior, Checkout / Order Flow, Navigation, and Logout. Testing combined structured Testiny cases with exploratory work, while confirmed defects were tracked in Jira and portfolio-level decisions were documented in GitHub.

Across five closed Testiny runs, **57 formal test cases** were recorded: **36 Passed and 21 Failed**. These totals must not be interpreted as an overall product-quality score. Two runs intentionally contained targeted defect reproductions, and the Special-User Addendum was entirely defect-focused.

The main `standard_user` shopping flow behaved as expected in the covered scenarios: Login, product browsing and sorting, Product Details consistency, Cart operations, Checkout validation, order completion, receipt generation, All Items navigation, and Logout. The About navigation action remained a confirmed failure.

## Scope and approach

Testing was manual, risk-based, and black-box. Expected behavior was based on the visible application flow, supplied demo data, internal consistency, and common e-commerce behavior where no formal requirement was available.

The completed manual scope included:

- Authentication / Login
- Product inventory and sorting
- Product Details
- Shopping Cart behavior
- Checkout Information and validation
- Checkout Overview
- Order completion
- Navigation menu actions covered by the plan
- Logout

The primary execution environment was:

- Windows 11
- Firefox 153.0.4 (64-bit)
- 1920 × 1080 desktop resolution

Formal execution ran from **21 August to 30 August 2026**. The public SauceDemo accounts were treated as test data; account names were not used as evidence that a failure was expected.

## Formal execution summary

| Checkpoint | Formal cases | Result | Main interpretation |
|---|---:|---|---|
| Authentication / Login | 21 | 21 Passed | Working authentication baseline for the covered scenarios |
| Inventory / Products | 14 | 5 Passed, 9 Failed | Stable `standard_user` baseline plus targeted `problem_user` defect reproductions |
| Targeted Special-User Addendum | 10 | 10 Failed | Deliberately defect-focused follow-up; not a regression score |
| Checkout / Order Flow | 9 | 8 Passed, 1 Failed | Working `standard_user` checkout baseline plus one `problem_user` defect reproduction |
| Navigation / Logout | 3 | 2 Passed, 1 Failed | Working All Items/Logout baseline plus the About failure |

All formal runs were closed. Failed cases were linked to their canonical Jira defects.

## Working baseline established

The completed cycle established a repeatable baseline for the main user journey.

### Authentication

The covered Login scenarios passed, including valid credentials, locked-out handling, invalid credentials, required fields, protected-page access while logged out, and recovery after a failed Login attempt.

### Inventory, Product Details, and Cart

With `standard_user`:

- all four sorting options behaved correctly;
- selected products opened the corresponding Product Details page;
- product name and price remained consistent between Products and Product Details;
- Add and Remove worked from Products and Product Details;
- Cart badge and visible Cart contents remained consistent;
- Cart state remained stable through normal navigation and page refresh.

Two unusual content strings were retained as observations rather than defects because no available requirement supported a stronger classification.

### Checkout and order completion

The `standard_user` checkout baseline covered:

- successful end-to-end order completion;
- required-field validation;
- cancellation from Checkout Information and Checkout Overview;
- Cart-state preservation through cancellation;
- Checkout Overview product/amount consistency;
- receipt generation and content consistency;
- completion-state behavior, including clearing the Cart badge and returning to Products with an empty Cart.

For the representative Backpack order, the displayed values were `$29.99` item price, `$2.40` tax, and `$32.39` total. These values are reported only as observed flow consistency; no undocumented tax rule or backend calculation is inferred.

### Navigation and session handling

**All Items** returned from Product Details to Products, and **Logout** returned the user to Login. Protected Inventory access after Logout was denied and remains formally covered in the Authentication suite.

## Confirmed defect coverage

The 21 failed formal cases map to **21 canonical confirmed defect records** across the completed checkpoints.

The main observed failure classes included:

- incorrect Product Details routing and an `ITEM NOT FOUND` state;
- sorting failures;
- incorrect or inconsistent product imagery;
- Add/Remove failures across Products and Product Details;
- Cart badge/content inconsistency;
- repeated user-visible responsiveness delays for `performance_glitch_user`;
- explicit sorting error behavior for `error_user`;
- missing Product Details descriptions;
- Checkout input/validation and Finish failures for special accounts;
- inconsistent Products-page pricing for `visual_user`;
- `problem_user` Last Name input being routed into First Name during Checkout;
- About navigation opening an error destination with visible **403 Forbidden** content.

Defects were separated or consolidated according to observable trigger and failure pattern rather than assumed implementation cause. Repeated instances of the same failure class were not turned into duplicate tickets solely because another test account exposed them.

No controlled development/fix cycle was part of this portfolio project, so this summary does not claim defect resolution or retest closure.

## Regression readiness

A separate [Consolidated Regression Checklist](regression-checklist.md) now captures **19 stable, high-value regression checks** across the completed functional scope.

The checklist favors the verified baseline and keeps known-defect reproductions separate. Detailed Testiny cases remain the source for formal execution steps and expected results when a recorded regression run is needed.

## Evidence and traceability

Tool responsibilities were kept intentionally separate:

- **Testiny:** test cases and formal execution records
- **Jira:** canonical confirmed defect reports and supporting evidence
- **GitHub:** planning, test design, post-execution reviews, regression reference, and this final manual QA summary

Evidence was selective rather than duplicated across every tool. Failed/unusual behavior received the strongest evidence focus, while representative passing evidence was retained where it added portfolio value.

## Residual risk and limitations

The manual cycle does not establish correctness outside its planned scope. Remaining limitations include:

- cross-browser and cross-device compatibility;
- formal accessibility testing;
- performance and load testing;
- security penetration testing;
- API/backend testing;
- database testing;
- real payment processing;
- undocumented business rules that cannot be established from the public interface;
- exhaustive regression of every special account across every feature.

`Reset App State` remains an explicit exclusion because it was treated as a test-support/reset utility rather than a core business workflow.

For the **About** action, only the visible result of the in-app navigation was assessed. The external destination was not treated as a separate system under test, and the visible **403 Forbidden** text was not interpreted as a verified HTTP response status.

## Deliverables completed

The manual QA track now contains:

- Test Plan
- Authentication / Login Test Design
- five closed Testiny execution checkpoints
- Jira defect records for confirmed findings
- module-level post-execution reviews
- Consolidated Regression Checklist
- Final Manual QA Summary

## Related documents

- [Test Plan](test-plan.md)
- [Authentication / Login — Test Design](login-test-design.md)
- [Authentication / Login review](login-post-execution-review.md)
- [Inventory / Products review](inventory-post-execution-review.md)
- [Targeted Special-User Addendum](special-user-addendum-post-execution-review.md)
- [Checkout / Order Flow review](checkout-order-flow-post-execution-review.md)
- [Navigation / Logout review](navigation-logout-post-execution-review.md)
- [Consolidated Regression Checklist](regression-checklist.md)

## Conclusion

The planned risk-based manual functional QA scope is complete and documented with traceable execution, confirmed defect reporting, and a consolidated regression baseline.

The results support a credible portfolio demonstration of manual functional testing, exploratory investigation, test design, defect classification, execution traceability, and regression planning. They do not claim exhaustive product coverage, production-client testing, or defect resolution beyond the evidence recorded in this project.
