# SauceDemo Functional QA — Test Plan

**Author:** Oussama MAOUCHE  
**Version:** 1.5  
**Last updated:** 1 September 2026  
**Document status:** Manual execution, portfolio audit, and regression checklist complete; final manual QA summary pending

## 1. Project Overview

This plan defines the manual functional testing scope for the SauceDemo (Swag Labs) web application.

The project focuses on the application's main user workflows, reproducible functional defects, and traceable QA documentation across Testiny, Jira, and GitHub.

Application under test: https://www.saucedemo.com/

## 2. Test Objectives

The objectives are to:

- Verify the main user workflows.
- Cover positive and negative functional scenarios.
- Apply structured test design techniques in greater depth to Authentication / Login.
- Verify shopping cart, checkout, and order-completion behavior.
- Identify and document reproducible functional defects.
- Perform confirmation testing and targeted regression where applicable.
- Maintain clear traceability between test design, execution results, and confirmed defects.

## 3. Scope

### In Scope

- Authentication / Login
- Product inventory
- Product details
- Product sorting
- Shopping cart
- Checkout information
- Checkout overview
- Order completion
- Navigation menu
- Logout

### Out of Scope

- API and backend testing
- Database testing
- Test automation during the manual testing phase
- Performance and load testing
- Security penetration testing
- Formal accessibility testing / WCAG audit
- Cross-browser and cross-device testing
- Real payment processing
- External systems or services beyond the visible result of an in-app navigation action

## 4. Test Approach

Testing is manual and black-box, combining structured test cases with exploratory testing. Effort is prioritized according to risk and importance within the main user journey.

Authentication / Login receives deeper coverage so that multiple test design techniques can be applied in one focused area. Other modules receive targeted functional coverage proportionate to their role in the end-to-end flow.

### Test Types

- Smoke Testing
- Functional Testing
- Negative Testing
- Exploratory Testing
- Regression Testing
- Confirmation Testing (Retesting)

### Test Design Techniques

The following techniques are used where relevant:

- Equivalence Partitioning
- Boundary Value Analysis
- Decision Table Testing
- Error Guessing

Boundary Value Analysis is used only when an actual or observable boundary exists. Undocumented field limits are not assumed.

### Risk Focus and Test Priorities

Testing effort is prioritized according to the impact of each function on the main user journey.

**High priority:**
- Authentication
- Shopping cart
- Checkout
- Order completion

**Medium priority:**
- Product inventory
- Product details
- Product sorting
- Navigation
- Logout

Authentication receives additional depth as a focused test-design exercise, while cart and checkout remain critical to the main shopping flow.

### Authentication Deep-Dive

The Login functionality receives extended coverage compared with the other modules.

Coverage includes:

- Valid and invalid credential combinations
- Empty mandatory fields
- Input variations
- Error-message behavior
- Available user/account states
- Protected-page access while logged out
- Recovery after a failed login
- Exploratory authentication scenarios

Logout is covered separately under the Navigation / Logout scope.

## 5. Test Environment

### Application

- Application: SauceDemo / Swag Labs
- URL: https://www.saucedemo.com/
- Application type: Web application
- Test environment: Public demonstration environment

### Client Environment

- Operating system: Windows 11
- Browser: Firefox
- Browser version: 153.0.4 (64-bit)
- Screen resolution: 1920 x 1080

Testing is limited to one primary desktop browser and environment. Cross-browser and cross-device compatibility are outside the current manual scope.

### Test Data

- Public demo accounts and credentials provided by the application
- Synthetic checkout information created only for testing
- No real personal, customer, or payment data

## 6. Entry Criteria

Testing can begin when:

- SauceDemo is accessible.
- Valid test credentials are available.
- The selected test environment is operational.
- The test scope has been defined.
- The initial test cases are ready for execution.

## 7. Exit Criteria

The planned testing cycle can be considered complete when:

- All planned test cases have been executed.
- Critical user workflows have been covered.
- Failed tests have been reviewed and reproducible defects documented.
- Confirmation testing has been performed where applicable.
- Targeted regression has been completed where relevant.
- Test execution results have been recorded.
- A final test summary has been prepared.

**Current status:** the planned manual functional execution, staged portfolio audit, and consolidated regression checklist are complete. The final manual QA summary remains pending, so the wider documentation milestone is still open.

## 8. Test Result Criteria

- **Passed:** The actual result matches the expected result.
- **Failed:** The actual result differs from the expected result and the behavior can be reproduced.
- **Blocked:** The test cannot be completed because a required condition, dependency, or environment is unavailable.
- **Skipped:** The test is intentionally not executed for the current run.
- **Not Run:** No execution result has yet been recorded for the test.

A failed test is reviewed before it is classified as a confirmed defect.

## 9. Defect Management

Unexpected behavior is reproduced and compared with the expected behavior before a Jira defect is created.

Confirmed defects are recorded in Jira and, where relevant, linked to the related Testiny execution.

A defect report should include, where applicable:

- A clear and specific title
- Test environment
- Relevant test data
- Preconditions
- Steps to reproduce
- Expected result
- Actual result
- Reproducibility
- User/business impact
- Priority only when justified by the project workflow
- Screenshots, video, or other useful evidence

If a reported behavior can no longer be reproduced, it is reviewed and documented rather than silently removed.

## 10. Test Deliverables and Tool Roles

The manual QA phase produces:

- Test Plan
- Test Cases
- Test Execution Results
- Defect Reports
- Selected supporting evidence
- Regression Checklist
- Final Manual QA Summary

Tool responsibilities are kept separate:

- **Testiny:** test cases and formal execution records
- **Jira:** confirmed defect reports, relationships, and detailed evidence
- **GitHub:** portfolio-facing planning, design, post-execution reviews, and final QA documentation

Detailed Jira or Testiny records are not duplicated in GitHub unless they add clear portfolio value.

## 11. Risks and Limitations

This project is performed against a public demonstration application and has several limitations:

- No formal business requirements or product specifications were provided.
- Expected behavior is derived from visible UI cues, supplied demo data, internal consistency, and common e-commerce behavior. If expected behavior cannot be established confidently, the finding remains an observation rather than being forced into a defect report.
- Manual execution and defect decisions follow a black-box approach. Public source code or technical material may be consulted only as secondary investigation support; it does not override observed application behavior or define expected behavior.
- The public demo application may change or become temporarily unavailable without notice.
- Testing is limited to one primary desktop browser and environment.
- Some provided test accounts may intentionally expose abnormal behavior. Reproducible black-box failures can still be documented in this portfolio, but they are not presented as production defects or client-reported issues.
- No real customer data, payment information, or production systems are involved.

These limitations must be considered when interpreting the results and the final QA summary.

## 12. Project Ownership

This is an independent QA portfolio project by Oussama MAOUCHE.

Sauce Labs is not a client and did not commission this testing work.
