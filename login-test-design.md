# Login Test Design

## 1. Observed Login Rules

Based on the public SauceDemo login page:

- The application provides six accepted usernames:
  - `standard_user`
  - `locked_out_user`
  - `problem_user`
  - `performance_glitch_user`
  - `error_user`
  - `visual_user`
- The documented password for all users is `secret_sauce`.
- The username field is a text input.
- The password field masks entered characters.
- No explicit minimum or maximum input length was observed in the inspected HTML.
- No formal authentication requirements or field-length specification were available for this exercise.

Since no documented length boundaries are available, field length will not be treated as a Boundary Value Analysis target. Long or unusual inputs may still be explored through negative testing and error guessing.

## 2. Equivalence Partitions

### Username

**Recognized username**

- A username listed by the application

**Unrecognized username**

- A username not listed by the application

**Missing username**

- Empty username

### Password

**Documented password**

- `secret_sauce`

**Incorrect password**

- Any password other than `secret_sauce`

**Missing password**

- Empty password

A recognized username does not necessarily imply successful authentication. Account state is evaluated separately.

## 3. Observed Account States

Using the documented password `secret_sauce`, the following behavior was observed:

| Username | Observed Login Result |
|---|---|
| `standard_user` | Login successful |
| `locked_out_user` | Login blocked with locked-out message |
| `problem_user` | Login successful |
| `performance_glitch_user` | Login successful; a noticeable delay was observed |
| `error_user` | Login successful |
| `visual_user` | Login successful |

The additional delay observed with `performance_glitch_user` is recorded as an observation only. Performance testing is outside the scope of this project.

## 4. Authentication Decision Table

| Rule | Username Present | Username Recognized | Password Present | Password Correct | Account Locked | Expected Result |
|---|---|---|---|---|---|---|
| R1 | Yes | Yes | Yes | Yes | No | Login succeeds and the Products page is displayed |
| R2 | Yes | Yes | Yes | Yes | Yes | Login is denied with `Epic sadface: Sorry, this user has been locked out.` |
| R3 | Yes | Yes | Yes | No | No | Login is denied with `Epic sadface: Username and password do not match any user in this service` |
| R4 | Yes | No | Yes | Yes | N/A | Login is denied with `Epic sadface: Username and password do not match any user in this service` |
| R5 | No | N/A | Yes | N/A | N/A | Login is denied with `Epic sadface: Username is required` |
| R6 | Yes | Yes | No | N/A | No | Login is denied with `Epic sadface: Password is required` |
| R7 | No | N/A | No | N/A | N/A | Login is denied with `Epic sadface: Username is required` |

The table is based on observed application behavior. `standard_user` was used as the representative login-enabled account for the negative credential checks, while `locked_out_user` was used for the locked-account condition.

## 5. Error Guessing and Input Variations

Additional input variations were explored using `standard_user` as the reference account.

| Scenario | Test Input Variation | Observed Result |
|---|---|---|
| Leading space in username | ` standard_user` | Login denied with credential-mismatch message |
| Trailing space in username | `standard_user ` | Login denied with credential-mismatch message |
| Uppercase username | `STANDARD_USER` | Login denied with credential-mismatch message |
| Leading space in password | ` secret_sauce` | Login denied with credential-mismatch message |
| Trailing space in password | `secret_sauce ` | Login denied with credential-mismatch message |
| Uppercase password | `SECRET_SAUCE` | Login denied with credential-mismatch message |
| Very long username | 250-character username | Login denied with credential-mismatch message |
| Very long password | 250-character password | Login denied with credential-mismatch message |

For all eight scenarios, the application displayed:

`Epic sadface: Username and password do not match any user in this service`

### Observations

- Leading and trailing spaces are not ignored during authentication.
- Username matching appears to be case-sensitive.
- Password matching appears to be case-sensitive.
- Long input values are accepted by the fields but do not authenticate successfully.
- No application error, crash, or unexpected validation behavior was observed during these checks.

These scenarios are treated as negative testing and error guessing. They are not presented as Boundary Value Analysis because no documented or observable field-length boundary is available.
