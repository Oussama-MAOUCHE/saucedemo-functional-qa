# SauceDemo Functional QA

This repository documents a manual black-box QA cycle I carried out on SauceDemo, a public e-commerce demo application.

I combined exploratory testing with structured test design, formal execution in Testiny, defect tracking in Jira, and regression planning. The scope follows the main user journey: authentication, product browsing and cart behavior, checkout and order completion, and navigation/logout.

## Project Snapshot

**Manual · Black-box · Risk-based**

- **5** closed Testiny runs
- **57** formal test cases
- **21** confirmed defect records
- **19** consolidated regression checks

The execution results describe the planned portfolio scope and should not be interpreted as an overall product-quality score. Some runs intentionally focused on reproducing specific failure patterns.

## What This Project Demonstrates

- Risk-based functional testing of the main SauceDemo user flows.
- Exploratory testing followed by structured test design and formal execution.
- Black-box defect investigation based on observable behavior rather than assumed implementation causes.
- Traceability between Testiny execution records, Jira defects, and portfolio-level QA documentation.
- Regression planning and identification of stable, repeatable candidates for later automation.

## Start Here

- [Final Manual QA Summary](docs/final-manual-qa-summary.md) — overall results, working baseline, confirmed defect coverage, residual risks, and conclusions.
- [Test Plan](docs/test-plan.md) — objectives, scope, priorities, test approach, environment, defect-management rules, and limitations.
- [Authentication / Login Test Design](docs/login-test-design.md) — a detailed example of structured test-design reasoning.
- [Consolidated Regression Checklist](docs/regression-checklist.md) — 19 stable, high-value regression checks derived from the completed manual cycle.

## Coverage at a Glance

| Area | Formal execution | Result | Review |
|---|---:|---|---|
| Authentication / Login | 21 cases | 21 Passed | [Post-execution review](docs/login-post-execution-review.md) |
| Inventory / Products | 14 cases | 5 Passed, 9 Failed | [Post-execution review](docs/inventory-post-execution-review.md) |
| Targeted Special-User Addendum | 10 cases | 10 Failed | [Post-execution review](docs/special-user-addendum-post-execution-review.md) |
| Checkout / Order Flow | 9 cases | 8 Passed, 1 Failed | [Post-execution review](docs/checkout-order-flow-post-execution-review.md) |
| Navigation / Logout | 3 cases | 2 Passed, 1 Failed | [Post-execution review](docs/navigation-logout-post-execution-review.md) |

The Inventory run combines a stable `standard_user` baseline with targeted `problem_user` defect reproductions. The Special-User Addendum was intentionally defect-focused.

Shopping Cart coverage is distributed across the Inventory / Products and Checkout / Order Flow checkpoints rather than represented by a separate standalone run.

## Test Approach

Testing was manual, risk-based, and black-box, combining structured test cases with exploratory work.

Authentication received deeper test-design coverage, while the remaining modules received targeted functional coverage proportionate to their role in the main user journey.

Where no formal requirement was available, expected behavior was based on visible UI cues, supplied demo data, consistency across the application, and common e-commerce behavior. Findings without a sufficiently supported expected result were retained as observations rather than being forced into defect reports.

Public source code or implementation details were not used to override observed application behavior.

The full scope, test types, limitations, and defect-management rules are documented in the [Test Plan](docs/test-plan.md).

## Tools and QA Records

| Tool / environment | Use in this project |
|---|---|
| Testiny | Test-case management and formal execution records |
| Jira | Confirmed defect reports, relationships, and supporting evidence |
| GitHub | Portfolio-facing planning, test design, post-execution reviews, regression reference, and final QA documentation |
| Firefox on Windows 11 | Primary manual test environment |

Detailed Testiny and Jira records are not duplicated in GitHub unless they add clear portfolio value.

## Portfolio Note

This is an independent QA portfolio project by Oussama MAOUCHE.

Sauce Labs is not a client and did not commission this work. SauceDemo is a public demonstration/training application, and some provided test accounts intentionally expose abnormal behavior.

Findings are documented as black-box portfolio results based on observed application behavior, not as production issues discovered on a client system.
