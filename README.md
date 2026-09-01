# SauceDemo Functional QA

This repository documents a manual black-box QA cycle I carried out on SauceDemo, a public e-commerce demo application. I combined exploratory testing with structured test cases, formal execution in Testiny, and defect tracking in Jira.

The scope follows the main user journey: authentication, product browsing and cart behavior, checkout and order completion, and navigation/logout. I also used selected SauceDemo test accounts to investigate distinct failure patterns without repeating the full suite for every account.

## Coverage at a glance

| Area | Formal execution | Result | Review |
|---|---:|---|---|
| Authentication / Login | 21 cases | 21 Passed | [Post-execution review](docs/login-post-execution-review.md) |
| Inventory / Products | 14 cases | 5 Passed, 9 Failed | [Post-execution review](docs/inventory-post-execution-review.md) |
| Targeted Special-User Addendum | 10 cases | 10 Failed | [Post-execution review](docs/special-user-addendum-post-execution-review.md) |
| Checkout / Order Flow | 9 cases | 8 Passed, 1 Failed | [Post-execution review](docs/checkout-order-flow-post-execution-review.md) |
| Navigation / Logout | 3 cases | 2 Passed, 1 Failed | [Post-execution review](docs/navigation-logout-post-execution-review.md) |

These results should not be read as an overall product-quality score. The Inventory run mixes a stable baseline with targeted defect-reproduction cases, and the Special-User Addendum was intentionally defect-focused.

Shopping Cart coverage is distributed across the Inventory / Products and Checkout / Order Flow checkpoints rather than represented by a separate standalone run.

## Work represented here

- Risk-based manual functional testing of the main SauceDemo user flows.
- Exploratory testing followed by focused formalization of reusable scenarios and confirmed defect reproductions.
- Traceability between Testiny execution records and Jira defects without duplicating the same evidence across tools.
- Black-box defect decisions based on observable behavior rather than assumed implementation intent.
- Regression and automation-candidate decisions for stable, repeatable flows.

Key design and planning artifacts:

- [Test Plan](docs/test-plan.md)
- [Login Test Design](docs/login-test-design.md)

## Tools and environment

| Tool / environment | Use in this project |
|---|---|
| Testiny | Test-case management and formal execution records |
| Jira | Confirmed defect reports, relationships, and supporting evidence |
| GitHub | Portfolio documentation and project reviews |
| Firefox on Windows 11 | Primary manual test environment |

## Test approach

Testing was manual, risk-based, and black-box, using both scripted and exploratory work. Where no formal requirement was available, expected behavior was based on visible UI cues, supplied demo data, consistency across the application, and common e-commerce behavior. Ambiguous findings were kept as observations rather than being forced into defect reports.

Public source code or implementation details were not used to override the observed behavior of the application. The full scope, test types, limitations, and defect-management rules are documented in the [Test Plan](docs/test-plan.md).

## Current status

The planned risk-based manual functional scope is complete. The repository is now going through a staged portfolio audit before the consolidated regression checklist and final manual QA summary are added. Targeted Playwright automation will follow for selected stable regression scenarios.

## Portfolio note

This is an independent QA portfolio project. Sauce Labs is not a client and did not commission this work. SauceDemo is a public demonstration/training application, and some provided test accounts intentionally expose abnormal behavior. Findings are documented as black-box portfolio results, not as production issues discovered on a client system.
