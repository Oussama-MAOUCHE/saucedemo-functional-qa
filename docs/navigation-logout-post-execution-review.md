# Navigation / Logout — Post-Execution Review

## Execution checkpoint

TR-5 formalizes the Navigation / Logout checks that had already been executed manually and reviewed.

- Test run: `TR-5 — SauceDemo – Navigation / Logout – Initial Execution – 30-08-2026`
- Run status: Closed
- Total test cases: 3
- Passed: 2
- Failed: 1
- Blocked: 0
- Skipped: 0
- Not Run: 0

The run contains two working `standard_user` baseline cases and one representative About-navigation defect reproduction.

## Working baseline — standard_user

Two formal cases passed:

- **All Items** from a Product Details page returns to the Products page;
- **Logout** from Products returns to the Login page.

During the Logout exploration, direct access to `/inventory.html` after Logout was also denied and returned the user to Login with:

`Epic sadface: You can only access '/inventory.html' when you are logged in.`

That protected-route behavior was already formalized in the Authentication / Login suite, so it was not duplicated as another Navigation / Logout case.

No confirmed defect was found in the covered **All Items** or Logout behavior.

## Confirmed defect reproduction — About

One representative case failed:

| Test case | Jira | Finding |
|---|---|---|
| TC-78 | SDQA-23 | Selecting **About** opens `https://saucelabs.com/error/404`, where the page visibly displays **403 Forbidden** instead of accessible About content |

The same observable result was also confirmed with `problem_user`. A second Testiny case was not added because the trigger, expected behavior, and visible failure pattern were materially the same.

The **403 Forbidden** wording is recorded only as visible page content. It is not treated as a verified HTTP response status, and no backend cause is inferred.

Testiny keeps the representative failed execution and Jira link. Jira remains the detailed defect record and supporting-evidence location.

## Scope decisions

### Reset App State

`Reset App State` was deliberately excluded from this checkpoint.

For this portfolio, it is treated as a test-support/reset utility rather than a core user workflow. The risk-based manual scope therefore prioritized navigation and authenticated-session behavior instead of testing the reset utility.

This is an explicit scope decision, not an accidental omission.

### About destination

The **About** action leaves SauceDemo and opens an external destination.

This review assesses only the user-visible result of selecting the in-app **About** option. It does not treat the external website as a separate system under test.

## Regression focus

A compact Navigation / Logout regression set should retain:

1. Product Details → **All Items** returns to Products.
2. **Logout** returns the user to Login.
3. Protected pages remain inaccessible after Logout — already represented in the Authentication / Login regression set.

The About case remains useful for targeted confirmation of SDQA-23, but it should not replace the stable navigation/session baseline.

## Automation candidates

### First regression candidate

- TC-77 — Logout from Products using `standard_user`

Logout is deterministic and directly related to authenticated access, so it is a useful browser-regression check.

### Add later

- TC-76 — All Items navigation from Product Details using `standard_user`

The behavior is stable and straightforward to automate, but it has lower regression value than Login, core shopping flows, Checkout, and Logout.

### Keep manual for now

- TC-78 — About navigation using `standard_user`

This case reproduces a known failure that leaves the application for an external destination. It is more useful as a manual confirmation case until there is a real fix/retest cycle or a stronger reason to automate it.

This is an automation-priority decision, not a statement that the case cannot be automated.

## Scope and residual risk

This checkpoint does not establish correctness for every possible menu state or external destination.

Project-level limitations still include:

- account-specific behavior outside the targeted scenarios already documented;
- cross-browser and cross-device compatibility;
- formal accessibility testing;
- performance and load testing;
- security penetration testing;
- API/backend testing;
- database testing;
- undocumented business rules that cannot be established from the public interface.

## Related documents

- [Authentication / Login review](login-post-execution-review.md)
- [Test Plan](test-plan.md)
- [Targeted Special-User Addendum](special-user-addendum-post-execution-review.md)

## Conclusion

The Navigation / Logout checkpoint is complete for the planned manual functional scope. TR-5 records a working `standard_user` baseline for **All Items** and Logout, while the About failure remains traceable through TC-78 and SDQA-23. Previously covered behavior and the explicit `Reset App State` exclusion are documented without creating duplicate coverage.
