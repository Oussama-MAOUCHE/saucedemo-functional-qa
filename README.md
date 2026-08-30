# SauceDemo Functional QA

Manual functional QA portfolio project for the SauceDemo / Swag Labs web application.

The project demonstrates a structured black-box testing workflow using risk-based test design, exploratory testing, formal test execution, defect reporting, and traceability across Testiny and Jira.

## Current coverage

### Authentication / Login

- 21 structured Testiny test cases
- Formal execution completed and closed
- 21 Passed, 0 Failed
- Focused coverage of valid/invalid credentials, required fields, account states, input variations, protected-page access, and recovery after a failed login

See: [`login-test-design.md`](login-test-design.md) and [`docs/login-post-execution-review.md`](docs/login-post-execution-review.md)

### Inventory / Products

- 14 structured Testiny test cases
- Formal execution completed and closed
- 5 Passed baseline scenarios for `standard_user`
- 9 Failed targeted scenarios for `problem_user`
- All nine failed executions linked to confirmed Jira defects with supporting evidence

The Inventory run intentionally combines a stable baseline with defect-reproduction scenarios, so its pass/fail ratio is not presented as an overall product-quality score.

See: [`docs/inventory-post-execution-review.md`](docs/inventory-post-execution-review.md)

### Targeted Special-User Addendum

- 10 focused Testiny cases covering `performance_glitch_user`, `error_user`, and `visual_user`
- Formal execution completed and closed
- 10 targeted defect-reproduction cases, all recorded as Failed and linked to their canonical Jira defects
- Coverage includes response delays, sorting error handling, Product Details content, checkout input and validation, order completion, price consistency, image consistency, and Product Details cart actions

This was a bounded defect-focused addendum rather than a full regression run for every account. Its failure count is not an overall product-quality score.

See: [`docs/special-user-addendum-post-execution-review.md`](docs/special-user-addendum-post-execution-review.md)

### Checkout / Order Flow

- 9 structured Testiny test cases
- Formal execution completed and closed
- 8 Passed `standard_user` baseline scenarios
- 1 Failed targeted `problem_user` scenario linked to SDQA-22
- Coverage includes order completion, required-field validation, cancellation and cart-state preservation, and PDF receipt generation

No confirmed functional defect was found in the covered `standard_user` checkout baseline. The failed `problem_user` case documents a distinct Last Name input-routing problem that prevents checkout from continuing.

See: [`docs/checkout-order-flow-post-execution-review.md`](docs/checkout-order-flow-post-execution-review.md)

## Tools

- Testiny — test case management and formal execution records
- Jira — confirmed defect tracking and evidence
- GitHub — portfolio documentation and later automation/CI work
- Firefox on Windows 11 — primary manual test environment

## Test approach

Testing is performed manually using a risk-based functional approach. Expected behavior is derived from observable UI behavior, available user-facing information, internal consistency, and defensible functional expectations.

Manual black-box execution is authoritative for defect decisions. Public source code or technical material may be used only as secondary corroboration and does not define expected behavior or invalidate an observed defect.

See the full [`Test Plan`](docs/test-plan.md).

## Project status

Completed checkpoints:

- Authentication / Login
- Inventory / Products
- Targeted Special-User Addendum
- Checkout / Order Flow

Next work will continue with Navigation / Logout and the remaining high-value SauceDemo functional flows before targeted Playwright automation is introduced for stable regression scenarios.

## Portfolio note

This is an independent QA portfolio project. Sauce Labs is not a client and did not commission this testing work. SauceDemo is a public demonstration/training application, and some provided test accounts intentionally expose abnormal behavior.
