# Navigation / Logout — Post-Execution Review

## Execution checkpoint

The Navigation / Logout slice was formally recorded in Testiny after the underlying manual checks had already been executed and reviewed.

- Test run: `TR-5 — SauceDemo – Navigation / Logout – Initial Execution – 30-08-2026`
- Total test cases: 3
- Passed: 2
- Failed: 1
- Blocked: 0
- Skipped: 0
- Not Run: 0

The run covers two working `standard_user` navigation/session behaviors and one targeted About-navigation failure. The run was closed after the failed execution comment and Jira link were checked.

## Working baseline — standard_user

Two scenarios passed:

- selecting **All Items** from a Product Details page returns to the Products page;
- selecting **Logout** from the Products page returns to the Login page.

The Logout exploration also reconfirmed that `/inventory.html` cannot be opened after the session has ended. That protected-route behavior was already formalized in the Authentication / Login checkpoint, so it was not duplicated as another Navigation test case.

No confirmed defect was found in the covered `All Items` or Logout behavior.

## Confirmed finding — About navigation

One targeted scenario failed:

| Test case | Jira defect | Finding |
|---|---|---|
| TC-78 | SDQA-23 | Selecting **About** opens `https://saucelabs.com/error/404`, where a visible **403 Forbidden** page appears instead of accessible About content |

The same observable behavior was also confirmed with `problem_user`, but a second Testiny case was not added because the trigger and failure pattern were materially the same. Jira keeps the affected-account context and the supporting screen recording; Testiny keeps one representative failed execution linked to SDQA-23.

The visible **403 Forbidden** text is documented as page content only. No HTTP response status or backend cause is inferred from the UI.

## Scope decisions

`Reset App State` was deliberately excluded from this slice. In this portfolio it is treated as a test-support/reset utility rather than a core user workflow, so testing it would add little value to the current risk-based scope.

The About action leads outside the SauceDemo application. This checkpoint does not attempt to test the external site itself; it records only the user-visible result of choosing the in-app **About** navigation option.

## Regression focus

A compact Navigation / Logout regression set should keep:

1. Product Details → **All Items** returns to Products;
2. **Logout** ends the active session and returns to Login;
3. protected pages remain inaccessible after Logout — already represented in the Authentication suite.

The About scenario remains useful for confirmation testing of SDQA-23, but it should not replace the stable navigation/session baseline.

## Automation candidate classification

### Automate soon

- TC-77 — Logout from Products using `standard_user`

Logout is deterministic, session-sensitive, and a useful regression check around authenticated access.

### Lower-priority regression automation

- TC-76 — All Items navigation from Product Details using `standard_user`

The behavior is stable and simple to automate, but it has less regression value than Login, core shopping flows, Checkout, and Logout.

### Keep manual for now

- TC-78 — About navigation using `standard_user`

This case reproduces a known failure that leaves the application for an external destination. It is better retained as a manual confirmation case until there is a real fix cycle or a stronger reason to automate it.

## Residual risk

This checkpoint does not establish correctness for every menu state or external destination. Remaining project-level risks include broader special-account behavior, cross-browser and cross-device compatibility, and the out-of-scope accessibility, security, performance, API, database, and backend areas defined in the Test Plan.

## Conclusion

The Navigation / Logout slice is complete for the current manual functional-testing scope. The working `standard_user` navigation/session baseline is documented, the About failure is traceable from Testiny to Jira, and deliberately excluded or previously covered behavior is recorded rather than duplicated.
