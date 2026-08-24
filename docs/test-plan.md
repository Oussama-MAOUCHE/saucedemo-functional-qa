# SauceDemo Functional QA — Test Plan

**Author:** Oussama MAOUCHE  
**Version:** 1.1  
**Last updated:** 24 August 2026

## 1. Project Overview

This project covers manual functional testing of the SauceDemo (Swag Labs) web application.

The purpose of the project is to validate the application's main user workflows, document test execution results, identify reproducible functional defects, and maintain a structured and traceable manual QA process.

Application under test: https://www.saucedemo.com/

## 2. Test Objectives

The objectives of this testing effort are to :

- Verify that the main user workflows behave as expected.
- Validate positive and negative user scenarios.
- Apply structured test design techniques to the authentication module.
- Verify shopping cart and checkout behavior.
- Identify and document reproducible functional defects.
- Perform retesting and basic regression testing where applicable.
- Produce clear and traceable test documentation.

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
- Test automation
- Performance and load testing
- Security penetration testing
- Formal accessibility testing / WCAG audit
- Cross-browser and cross-device testing
- Real payment processing
- Systems or services outside SauceDemo

## 4. Test Approach

Testing will be performed manually using a risk-based and structured functional testing approach.

The authentication module will receive deeper coverage so that multiple test design techniques can be applied in a focused area. Other application areas will receive focused functional coverage based on their importance within the main user journey.

Testing will include both scripted test cases and exploratory testing.

### Test Types

- Smoke Testing
- Functional Testing
- Negative Testing
- Exploratory Testing
- Regression Testing
- Confirmation Testing (Retesting)

### Test Design Techniques

The following techniques will be applied where relevant :

- Equivalence Partitioning
- Boundary Value Analysis
- Decision Table Testing
- Error Guessing

Boundary Value Analysis will only be used where an actual or observable boundary exists. No undocumented field limits will be assumed.

### Risk Focus and Test Priorities

Testing effort will be prioritized according to the impact of each function on the main user journey.

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

Authentication will receive additional depth as a focused test-design exercise, while cart and checkout flows remain critical from a user-journey perspective.

### Authentication Deep-Dive

The Login functionality will receive extended coverage compared with the other modules.

Testing will include :

- Valid and invalid credential combinations
- Empty mandatory fields
- Input variations
- Error-message behavior
- User/account states available in the application
- Session and logout behavior
- Exploratory authentication scenarios

The Login functionality receives deeper coverage because it provides a focused area for applying multiple test design techniques, input variations, and user-state scenarios.

## 5. Test Environment

### Application

- Application: SauceDemo / Swag Labs
- URL: https://www.saucedemo.com/
- Application type: Web application
- Test environment: Public demonstration environment

### Client Environment

- Operating system : Windows 11
- Browser : Firefox
- Browser version : 153.0.4 (64 bits)
- Screen resolution : 1920 x 1080

Testing for this project will be performed on one primary browser and environment. Cross-browser and cross-device compatibility testing are outside the current scope.

### Test Data

- Public demo accounts and credentials provided by the application
- Synthetic checkout information created only for testing
- No real personal, customer, or payment data will be used

## 6. Entry Criteria

Testing can begin when :

- The SauceDemo application is accessible.
- Valid test credentials are available.
- The selected test environment is operational.
- The test scope has been defined.
- The initial test cases are ready for execution.

## 7. Exit Criteria

The planned testing cycle can be considered complete when:

- All planned test cases have been executed.
- Critical user workflows have been covered.
- Failed tests have been reviewed and reproducible defects documented.
- Retesting has been performed where applicable.
- Basic regression testing has been completed after relevant changes or retesting.
- Test execution results have been recorded.
- A final test summary has been prepared.

## 8. Test Result Criteria

- **Passed:** The actual result matches the expected result.
- **Failed:** The actual result differs from the expected result and the behavior can be reproduced.
- **Blocked:** The test cannot be completed because a required condition, dependency, or environment is unavailable.

## 9. Defect Management

A failed test will not automatically be considered a defect.

Before creating a defect, the unexpected behavior will be reproduced and checked against the expected behavior of the application.

Confirmed defects will be recorded in Jira and, where possible, linked to the related test case or test execution in Testiny.

Each defect report should include, where relevant:

- A clear and specific title
- Test environment
- Preconditions
- Steps to reproduce
- Expected result
- Actual result
- Reproducibility
- User/business impact
- Priority or severity only when justified by the project workflow
- Screenshots, video, or other useful evidence

If a reported issue can no longer be reproduced during the project, it will be reviewed and documented accordingly.

## 10. Test Deliverables

The project will produce the following testing artifacts:

- Test Plan
- Test Cases
- Test Execution Results
- Defect Reports
- Supporting Screenshots and Evidence
- Regression Checklist
- Final Test Summary Report

Test cases and execution results will be managed in Testiny.

Confirmed defects will be tracked in Jira.

Final portfolio documentation and selected test evidence will be stored in the GitHub project repository.

## 11. Risks and Limitations

This project is performed against a public demonstration application and has several limitations:

- No formal business requirements or product specifications have been provided.
- Expected behavior is derived from available UI cues, supplied demo data, and common e-commerce conventions. Where expected behavior is unclear, the finding will be documented as an observation rather than automatically reported as a defect.
- Manual execution and defect decisions are performed using a black-box approach. Public source code or technical documentation may be consulted separately as secondary corroboration or investigation support, but they do not define expected behavior or determine whether an observed black-box failure is a defect.
- The application may be changed or become temporarily unavailable without notice.
- Testing is limited to one primary browser and desktop environment.
- Some SauceDemo test accounts may intentionally expose abnormal behavior because SauceDemo is a demo/training application. Confirmed black-box failures may still be documented as defects in this portfolio context, but they will not be misrepresented as production defects or client-reported issues.
- No real customer data, payment information, or production systems are involved.

These limitations will be considered when interpreting test results and writing the final test summary.

## 12. Project Ownership

This is an independent QA portfolio project by Oussama MAOUCHE.

Sauce Labs is not a client and did not commission this testing work.
