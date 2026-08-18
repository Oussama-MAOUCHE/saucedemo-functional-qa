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
- No formal authentication requirements or field-length specification are available.

Because no documented length boundaries are available, Boundary Value Analysis will not be applied to arbitrary username or password lengths. Long or unusual inputs may still be explored through negative testing and error guessing.

## 2. Equivalence Partitions

### Username

**Valid / recognized input**
- A username listed by the application

**Invalid / unrecognized input**
- A username not listed by the application

**Missing input**
- Empty username

### Password

**Valid input**
- `secret_sauce`

**Invalid input**
- Any password other than `secret_sauce`

**Missing input**
- Empty password

- A recognized username does not necessarily imply successful authentication. Account state is evaluated separately.

## 3. Observed Account States

Using the documented password `secret_sauce`, the following behavior was observed:

| Username | Observed Login Result |
|---|---|
| `standard_user` | Login successful |
| `locked_out_user` | Login blocked with locked-out message |
| `problem_user` | Login successful |
| `performance_glitch_user` | Login successful with a noticeable delay |
| `error_user` | Login successful |
| `visual_user` | Login successful |

The additional delay observed with `performance_glitch_user` is recorded as an observation only. Performance testing is outside the scope of this project.

## 4. Authentication Decision Table

| Rule | Username Condition | Password Condition | Account State | Expected Result |
|---|---|---|---|---|
| R1 | Recognized username | Valid | Active/demo account | Login succeeds and Products page is displayed |
| R2 | `locked_out_user` | Valid | Locked | Login is denied with `Epic sadface: Sorry, this user has been locked out.` |
| R3 | Recognized username | Invalid | Active/demo account | Login is denied with `Epic sadface: Username and password do not match any user in this service` |
| R4 | Unrecognized username | Valid | Unknown | Login is denied with `Epic sadface: Username and password do not match any user in this service` |
| R5 | Empty | Valid | Not applicable | Login is denied with `Epic sadface: Username is required` |
| R6 | Valid recognized username | Empty | Active/demo account | Login is denied with `Epic sadface: Password is required` |
| R7 | Empty | Empty | Not applicable | Login is denied with `Epic sadface: Username is required` |

The decision table above is based on observed application behavior. Combinations that were not executed are not presented as confirmed behavior.
