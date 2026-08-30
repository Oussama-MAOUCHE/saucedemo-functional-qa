# Authentication / Login — Test Design

This document records the test-design logic used for the SauceDemo Login slice. It focuses on the observed inputs, account states, negative variations, decision rules, and exploratory additions that were later formalized in Testiny.

Formal execution results are summarized separately in the [Login post-execution review](login-post-execution-review.md).

## 1. Login Inputs and Available Accounts

The public SauceDemo Login page lists six usernames:

- `standard_user`
- `locked_out_user`
- `problem_user`
- `performance_glitch_user`
- `error_user`
- `visual_user`

The documented password for these accounts is `secret_sauce`.

From the visible Login interface and the information provided with the demo:

- the Username field accepts text input;
- the Password field masks entered characters;
- no minimum or maximum field length is stated;
- no formal authentication specification or field-length requirement was available for this project.

Because no documented or observable length boundary was available, field length was not treated as a Boundary Value Analysis target. Long inputs were still explored through negative testing and error guessing.

## 2. Equivalence Partitions

### Username

**Recognized username**
- One of the usernames listed by the application

**Unrecognized username**
- A username not listed by the application

**Missing username**
- Empty Username field

### Password

**Documented password**
- `secret_sauce`

**Incorrect password**
- Any value other than `secret_sauce`

**Missing password**
- Empty Password field

A recognized username does not by itself imply successful authentication because account state is evaluated separately.

## 3. Observed Account States

Using the documented password `secret_sauce`, the following behavior was observed:

| Username | Observed login result |
|---|---|
| `standard_user` | Login successful |
| `locked_out_user` | Login blocked with the locked-out message |
| `problem_user` | Login successful |
| `performance_glitch_user` | Login successful after a noticeable delay |
| `error_user` | Login successful |
| `visual_user` | Login successful |

The initial Login suite recorded the authentication result for `performance_glitch_user` as Passed. The delay was later investigated in the targeted Special-User Addendum, where repeated user-visible responsiveness delays were formalized separately as **SDQA-10**.

This remains a black-box responsiveness finding. No load test, response-time SLA, or backend cause is inferred.

## 4. Authentication Decision Table

In this table, **Password Correct** means the documented shared password `secret_sauce`.

| Rule | Username Present | Username Recognized | Password Present | Password Correct | Account Locked | Expected Result |
|---|---|---|---|---|---|---|
| R1 | Yes | Yes | Yes | Yes | No | Login succeeds and the Products page is displayed |
| R2 | Yes | Yes | Yes | Yes | Yes | Login is denied with `Epic sadface: Sorry, this user has been locked out.` |
| R3 | Yes | Yes | Yes | No | No | Login is denied with `Epic sadface: Username and password do not match any user in this service` |
| R4 | Yes | No | Yes | Yes | N/A | Login is denied with `Epic sadface: Username and password do not match any user in this service` |
| R5 | No | N/A | Yes | N/A | N/A | Login is denied with `Epic sadface: Username is required` |
| R6 | Yes | Yes | No | N/A | N/A | Login is denied with `Epic sadface: Password is required` |
| R7 | No | N/A | No | N/A | N/A | Login is denied with `Epic sadface: Username is required` |

The table is based on observed application behavior. `standard_user` was used as the representative login-enabled account for negative credential checks, while `locked_out_user` represented the locked-account condition.

## 5. Error Guessing and Input Variations

Additional input variations were explored with `standard_user` as the reference account.

| Scenario | Test input | Observed result |
|---|---|---|
| Leading space in username | ` standard_user` | Login denied with credential-mismatch message |
| Trailing space in username | `standard_user ` | Login denied with credential-mismatch message |
| Uppercase username | `STANDARD_USER` | Login denied with credential-mismatch message |
| Leading space in password | ` secret_sauce` | Login denied with credential-mismatch message |
| Trailing space in password | `secret_sauce ` | Login denied with credential-mismatch message |
| Uppercase password | `SECRET_SAUCE` | Login denied with credential-mismatch message |
| Very long username | 250-character username | Login denied with credential-mismatch message |
| Very long password | 250-character password | Login denied with credential-mismatch message |

All eight scenarios displayed:

`Epic sadface: Username and password do not match any user in this service`

### Observations

- Leading and trailing spaces were not ignored during authentication.
- Username matching appeared to be case-sensitive.
- Password matching appeared to be case-sensitive.
- The fields accepted the 250-character test values, but those values did not authenticate successfully.
- No application crash or additional validation failure was observed during these checks.

These scenarios are treated as negative testing and error guessing, not Boundary Value Analysis, because no field-length boundary was documented or observable.

## 6. Exploratory Additions

Exploratory checks identified two useful authentication behaviors that were not fully represented by the initial decision table and input-variation coverage.

### 6.1 Direct access to Inventory while logged out

A logged-out user navigated directly to:

`https://www.saucedemo.com/inventory.html`

The application returned the user to the Login page at:

`https://www.saucedemo.com/`

and displayed:

`Epic sadface: You can only access '/inventory.html' when you are logged in.`

This behavior was formalized in Testiny as **TC-20**.

### 6.2 Recovery after a failed login

Using `standard_user` with an incorrect password displayed the credential-mismatch error. After dismissing the error with the `X` control:

- the error message was removed;
- the entered username remained in the field;
- the entered password remained in the field;
- replacing the password with `secret_sauce` allowed Login to succeed without refreshing the page.

This behavior was formalized in Testiny as **TC-21**.

Neither behavior was classified as a defect.

## 7. Formal Execution Checkpoint

The Authentication / Login suite was formally executed in Testiny on **21 August 2026** in the primary environment defined in the Test Plan.

| Metric | Result |
|---|---:|
| Test cases executed | 21 |
| Passed | 21 |
| Failed | 0 |
| Blocked | 0 |
| Skipped | 0 |
| Not Run | 0 |

Selected execution evidence was retained for:

- TC-1 — standard successful login;
- TC-2 — locked-out account handling;
- TC-7 — both required fields empty;
- TC-20 — direct access to Inventory while logged out.

No defect was raised from TR-1 because all 21 recorded cases matched their expected results. The later `performance_glitch_user` responsiveness finding was handled separately in the targeted Special-User Addendum and does not alter the recorded TR-1 result.

## Related Documents

- [Test Plan](test-plan.md)
- [Login post-execution review](login-post-execution-review.md)
- [Targeted Special-User Addendum](special-user-addendum-post-execution-review.md)
