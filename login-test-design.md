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
