# SQL Injection Portfolio — Evidence Screenshots

These screenshots were extracted from the user's original Word document and grouped by the corresponding PortSwigger lab. Host identifiers and cookie/session values have been redacted where visible. The Intruder-results screenshot was intentionally excluded because it may expose extracted credentials.

## Lab 01 — Retrieve hidden data
- `Lab-01/01-hidden-data-category-page.png` — category page after the SQLi condition.
- `Lab-01/02-lab-solved-confirmation.png` — PortSwigger lab solved banner.

## Lab 02 — UNION-based SQL injection
- `Lab-02/01-union-select-response.png` — response showing injected values.
- `Lab-02/02-union-request-redacted.png` — UNION request with host/cookie redacted.
- `Lab-02/03-union-select-test.png` and `04-union-select-followup.png` — additional test evidence.

## Lab 03 — Blind SQL injection with conditional responses
- `Lab-03/01-true-condition-response.png` — true-condition response.
- `Lab-03/02-false-condition-comparison.png` — false-condition comparison.
- `Lab-03/03-administrator-exists-check.png` — administrator existence check.
- `Lab-03/04-password-length-check.png` and `05-length-boundary-test.png` — length checks.
- `Lab-03/06-substring-condition-test.png` — substring condition test.
- `Lab-03/07-administrator-login-form.png` — login form with masked password field.

## Add screenshots inside the reports
Copy the relevant image links from the corresponding `EVIDENCE-SNIPPETS.md` file into each `Labs/Lab-XX/Report.md` under an `## Evidence` heading.
