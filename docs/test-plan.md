# SauceDemo Functional QA — Test Plan

## 1. Project Overview

This project covers manual functional testing of the SauceDemo (Swag Labs) web application.

The purpose of the project is to validate the application's main user workflows, document test execution results, identify reproducible functional defects, and demonstrate a structured manual QA process.

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
- Advanced accessibility auditing
- Cross-browser and cross-device testing
- Real payment processing
- Systems or services outside SauceDemo

## 4. Test Approach

Testing will be performed manually using a risk-based and structured functional testing approach.

The authentication module will receive deeper test coverage and will be used to demonstrate multiple test design techniques. Other application areas will receive focused functional coverage based on their importance within the main user journey.

Testing will include both scripted test cases and exploratory testing.

### Test Types

- Smoke Testing
- Functional Testing
- Negative Testing
- Exploratory Testing
- Regression Testing
- Retesting

### Test Design Techniques

The following techniques will be applied where relevant :

- Equivalence Partitioning
- Boundary Value Analysis
- Decision Table Testing
- Error Guessing
- Positive and Negative Scenario Design

Boundary Value Analysis will only be used where an actual or observable boundary exists. No undocumented field limits will be assumed.

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

The purpose is to demonstrate structured test design rather than simply execute basic valid/invalid login cases.

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

  ## 8. Defect Management

A failed test will not automatically be considered a defect.

Before creating a defect, the unexpected behavior will be reproduced and checked against the expected behavior of the application.

Confirmed defects will be recorded in Jira and, where possible, linked to the related test case or test execution in Testiny.

Each defect report should include:

- A clear and specific title
- Test environment
- Preconditions
- Steps to reproduce
- Expected result
- Actual result
- Severity
- Reproducibility
- Screenshots or other useful evidence

If a reported issue can no longer be reproduced during the project, it will be reviewed and documented accordingly.

## 9. Test Deliverables

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

## 10. Risks and Limitations

This project is performed against a public demonstration application and has several limitations:

- No formal business requirements or product specification have been provided.
- Expected behavior is based on the visible application behavior and normal e-commerce conventions.
- Testing is performed as black-box testing without access to the source code, API, database, or server-side implementation.
- The application may be changed or become temporarily unavailable without notice.
- Testing is limited to one primary browser and desktop environment.
- Some SauceDemo test accounts may intentionally demonstrate abnormal behavior. Such behavior will be documented carefully and will not automatically be presented as an unintended production defect.
- No real customer data, payment information, or production systems are involved.

These limitations will be considered when interpreting test results and writing the final test summary.

## 11. Project Ownership

This is an independent QA portfolio project performed by Oussama MAOUCHE.

The testing, test design, execution, documentation, and reporting are carried out as part of an independent professional practice project.

Sauce Labs is not a client of this project and did not commission this testing work.
