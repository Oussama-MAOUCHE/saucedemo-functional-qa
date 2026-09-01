# SauceDemo — Consolidated Regression Checklist

## Purpose

This checklist consolidates the stable, high-value regression coverage established during the completed manual black-box QA cycle.

It is intended for focused re-checks after relevant application changes and as an input to later regression planning. It is **not** a new execution record and does not replace the detailed Testiny cases, Testiny runs, or Jira defect records.

The checklist favors the verified `standard_user` baseline. Known defects are handled separately through their existing Testiny/Jira reproductions rather than being mixed into a clean regression baseline.

## Regression baseline

Primary environment used for the completed manual cycle:

- Browser: Firefox
- Operating system: Windows 11
- Primary baseline account: `standard_user`
- Representative checkout product: `Sauce Labs Backpack`
- Representative checkout data: `QA / Tester / 19800`

Before using this checklist, start from a known application state appropriate to the scenario. Do not use `Reset App State` as a regression requirement; it remains outside the planned functional scope.

## Core regression checklist

### Authentication / Login

| ID | Regression check | Expected result | Source |
|---|---|---|---|
| RG-01 | Log in with valid `standard_user` credentials. | The Products page is displayed. | TC-1 |
| RG-02 | Log in with `locked_out_user`. | Login is denied and the locked-account error is displayed. | TC-2 |
| RG-03 | Use a valid username with an incorrect password. | Login is denied and the invalid-credentials error is displayed. | TC-3 |
| RG-04 | Check required credential validation: Username missing, Password missing, and both fields empty. | The relevant required-field error is displayed for each condition and Login does not proceed. | TC-5, TC-6, TC-7 |
| RG-05 | Open `/inventory.html` without an authenticated session. | Access is denied and Login is displayed with `Epic sadface: You can only access '/inventory.html' when you are logged in.` | TC-20 |
| RG-06 | After a failed Login attempt, correct the password without refreshing the page and submit again. | Login succeeds and the Products page is displayed. | TC-21 |

### Inventory / Products and Cart

| ID | Regression check | Expected result | Source |
|---|---|---|---|
| RG-07 | Apply all four available product-sorting options. | The product list is ordered correctly for each option and the selected option remains visible. | TC-43 |
| RG-08 | Open a product from Products and compare it with Product Details. | The selected product opens its corresponding Product Details page; name and price remain consistent. | TC-44 |
| RG-09 | Add a product from Products and open the Cart. | The product is added, the Cart badge updates, and the Cart shows consistent product data. | TC-45 |
| RG-10 | Remove an added product from Products. | The item is removed and the Cart state/badge updates consistently. | TC-46 |
| RG-11 | Add and remove a product from Product Details. | Both actions work and the Cart state remains consistent with the visible button/action state. | TC-47 |
| RG-12 | Navigate between Products, Product Details and Cart, then refresh while an item is in the Cart. | Cart contents remain stable through normal navigation and page refresh. | Baseline exploration |

### Checkout / Order Flow

| ID | Regression check | Expected result | Source |
|---|---|---|---|
| RG-13 | Complete the main order flow with `Sauce Labs Backpack` and `QA / Tester / 19800`. | Checkout reaches completion; the product remains consistent through Cart and Overview; `$29.99 + $2.40` is displayed as `$32.39`; the Cart badge clears; **Back Home** returns to Products with the Cart empty. | TC-67 + baseline exploration |
| RG-14 | Check Checkout Information validation with all fields empty and with First Name, Last Name, and Postal Code missing individually. | The flow stays on Checkout Information. All empty / First Name missing displays `Error: First Name is required`; Last Name missing displays `Error: Last Name is required`; Postal Code missing displays `Error: Postal Code is required`. | TC-68 to TC-71 |
| RG-15 | From Checkout Information, select **Cancel** with a product already in the Cart. | The Cart page is displayed and the product remains in the Cart. | TC-72 |
| RG-16 | From Checkout Overview, select **Cancel**. | Products is displayed and the product remains in the Cart. | TC-73 |
| RG-17 | Generate the PDF receipt after a completed order. | The receipt opens/downloads successfully and matches the completed order's recipient, product, item total, tax, and total. | TC-75 |

### Navigation / Logout

| ID | Regression check | Expected result | Source |
|---|---|---|---|
| RG-18 | From Product Details, open the menu and select **All Items**. | The Products page is displayed. | TC-76 |
| RG-19 | From Products, select **Logout**. | The Login page is displayed. Protected-page access after logout remains covered by RG-05. | TC-77 |

## Change-driven checks

The following scenarios are useful when the related area changes, but they do not need to be part of every compact regression pass:

- unrecognized username handling;
- username/password case sensitivity;
- leading and trailing whitespace behavior;
- very long username/password robustness checks;
- additional documented SauceDemo account states that are relevant to the change under test.

Use the detailed Testiny cases when these scenarios need full execution steps and expected results.

## Known-defect confirmation

Known defect reproductions are **not** included in the clean baseline above.

If the application changes in a way that could affect an existing defect, use the linked Testiny/Jira reproduction for targeted confirmation or retesting rather than adding the failure to every routine regression pass.

This applies to the confirmed Inventory/Product Details, special-user, Checkout, and About findings already tracked in Jira.

The **About** action is therefore not treated as a passing regression baseline while SDQA-23 remains unresolved.

## Explicit exclusions and limits

This checklist does not add coverage beyond the completed manual scope. It does not cover:

- `Reset App State`;
- API/backend testing;
- database testing;
- performance and load testing;
- security penetration testing;
- formal accessibility testing;
- cross-browser or cross-device compatibility;
- real payment processing;
- external systems beyond the visible result of an in-app navigation action.

## How to use this artifact

This GitHub file is a consolidated regression reference, not execution evidence.

When a formal regression run is performed:

1. use the relevant Testiny cases or create a dedicated Testiny run if formal recording is needed;
2. record actual Pass/Fail/Blocked/Skipped results in the execution tool;
3. link any confirmed defect to its canonical Jira issue;
4. update this checklist only when the stable regression scope itself changes.

## Related documents

- [Test Plan](test-plan.md)
- [Authentication / Login review](login-post-execution-review.md)
- [Inventory / Products review](inventory-post-execution-review.md)
- [Targeted Special-User Addendum](special-user-addendum-post-execution-review.md)
- [Checkout / Order Flow review](checkout-order-flow-post-execution-review.md)
- [Navigation / Logout review](navigation-logout-post-execution-review.md)
