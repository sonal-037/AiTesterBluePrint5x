***Context***

Validate the VWO login module against the stated requirements: registered users can log in with valid credentials; invalid credentials do not grant access; email and password are mandatory; successful login opens the authenticated dashboard.

Assumption: Test execution is authorized in a QA/staging environment or another environment explicitly approved by the application owner. Do not use real customer credentials.

***Limits***

Only the supplied requirements are treated as approved behavior.

No password complexity/length rules, exact error messages, account lockout, CAPTCHA, MFA, session timeout, remember-me, or email normalization rules are assumed.

Email/password boundary limits and supported browser matrix are not specified; related cases are marked Requires clarification.

Dashboard direct URL behavior should be confirmed; test only if the route is known and access is authorized.

***Examples***

Data ID

Test data

Use

TD-01

Registered test email + correct password

Valid login

TD-02

Registered test email + incorrect password

Invalid password

TD-03

Confirmed unregistered email + arbitrary password

Invalid/unregistered account

TD-04

Blank email

Mandatory-field check

TD-05

Blank password

Mandatory-field check

TD-06

Whitespace-only email/password

Input handling; expected behavior Requires clarification

TD-07

Email/password at or beyond limits

Boundary checks; limits Requires clarification

Replace placeholders with controlled QA test data. Store credentials securely; do not include passwords in screenshots, defect comments, or this document.

***Action ***

Test Case ID

Type

Title

Steps

Expected Result

TC-LOGIN-001

Positive

Verify login with valid registered credentials

1. Open login page. 2. Enter TD-01 email and password. 3. Submit.

User is authenticated and the authenticated dashboard opens.

TC-LOGIN-002

Negative

Verify login is rejected with incorrect password

1. Open login page. 2. Enter registered email and TD-02 password. 3. Submit.

Access is denied; user remains unauthenticated. Exact error message Requires clarification.

TC-LOGIN-003

Negative

Verify login is rejected for unregistered email

1. Open login page. 2. Enter TD-03 email and password. 3. Submit.

Access is denied; user remains unauthenticated. Exact error message Requires clarification

TC-LOGIN-004

Negative

Verify email is mandatory

1. Open login page. 2. Leave email blank. 3. Enter a valid test password. 4. Submit.

Login is not completed; email is treated as mandatory. Validation UI/text Requires clarification

TC-LOGIN-005

Negative

Verify password is mandatory

1. Open login page. 2. Enter TD-01 email. 3. Leave password blank. 4. Submit.

Login is not completed; password is treated as mandatory. Validation UI/text Requires clarification

TC-LOGIN-006

Negative

Verify both fields are mandatory

1. Open login page. 2. Leave email and password blank. 3. Submit.

Login is not completed; both required fields are identified/handled. Exact messages Requires clarification

TC-LOGIN-007

Negative

Verify whitespace-only email does not authenticate

1. Enter whitespace-only email and a valid test password. 2. Submit.

No authenticated access is granted. Trimming/validation behavior Requires clarification

TC-LOGIN-008

Negative

Verify whitespace-only password does not authenticate

1. Enter TD-01 email and whitespace-only password. 2. Submit.

No authenticated access is granted. Whitespace handling Requires clarification

TC-LOGIN-009

Negative

Verify both credentials invalid

1. Enter an unregistered email and incorrect password. 2. Submit.

Access is denied; user remains unauthenticated

TC-LOGIN-010

Positive

Verify dashboard after successful login

1. Complete TC-LOGIN-001. 2. Observe destination URL/page. 3. Verify dashboard content/controls are available.

Authenticated dashboard is displayed. Dashboard indicators/expected content should be agreed

TC-LOGIN-011

Negative / access

Verify dashboard is not accessible after failed login

1. Submit invalid credentials. 2. If approved dashboard URL is known, open it directly in same browser.

Unauthenticated user is not granted dashboard access. Redirect/response behavior Requires clarification

TC-LOGIN-012

Boundary – clarification

Verify email at maximum supported length

1. Use email value at documented maximum. 2. Submit with controlled password.

Expected result Requires clarification: email length limit and acceptance rules

TC-LOGIN-013

Boundary – clarification

Verify email exceeding maximum supported length

1. Enter email exceeding documented maximum. 2. Submit.

Expected result Requires clarification: limit and whether UI prevents input or rejects submission

TC-LOGIN-014

Boundary – clarification

Verify password at minimum/maximum supported login length

1. Enter registered email and password at documented boundary. 2. Submit.

Requires clarification: login input limits; do not infer password policy

TC-LOGIN-015

Boundary – clarification

Verify email with leading/trailing spaces

1. Enter TD-01 email with spaces around it and correct password. 2. Submit.

Requires clarification: trimming/normalization; outcome must follow agreed requirement

TC-LOGIN-016

Negative

Verify repeated invalid attempts never authenticate

1. Submit invalid credentials multiple times within approved test limits. 2. Observe each response and access state.

Every failed attempt remains unauthenticated. Lockout/throttle behavior Requires clarification; stop if protection is triggered

R — Review

Recommended execution review

Confirm the environment and authorization before testing.

Confirm valid, invalid, and unregistered test data are available.

Execute all non-clarification cases and record Actual Result, Status (Pass/Fail/Blocked), tester, date, and evidence reference.

Raise defects for deviations from approved requirements; include steps, expected/actual result, environment, and sanitized evidence.

Obtain decisions for all Requires clarification items before finalizing boundary expectations.

Review scenario coverage, defects, and residual risks with QA/product owner.

Recommended pass/exit criteria

All approved test cases executed or formally dispositioned.

Valid login and dashboard navigation pass.

Invalid and incomplete credentials never grant authenticated access.

No open Critical/High severity login defects, unless formally accepted by the release owner.

Test results and unresolved clarifications are documented.