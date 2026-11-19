# SQL Injection – Practical Penetration Testing Portfolio

A portfolio of three PortSwigger Web Security Academy SQL injection labs, documented from prior practical work and the supplied six-page DOCX.

## Completed labs

| ID | Lab | Vulnerability | Completion evidence |
|---|---|---|---|
| Lab-01 | Retrieve hidden data using SQL injection | In-band SQL injection / boolean condition | Supplied page 1 screenshot shows the lab success banner |
| Lab-02 | SQL injection attack, querying the database type and version on MySQL and Microsoft | UNION-based SQL injection / DBMS fingerprinting | Prior conversation records `LAB Solved` and congratulations markers |
| Lab-03 | Blind SQL injection with conditional responses | Blind SQL injection / conditional response oracle | User reached the account page showing username `administrator` |

## Repository structure

```text
SQL-Injection-Portfolio/
├── README.md
├── Labs/Lab-01/Report.md
├── Labs/Lab-02/Report.md
├── Labs/Lab-03/Report.md
├── Screenshots/README.md
├── Payloads/SQLi-Payloads.md
└── Remediation/Secure-SQL-Queries.md
```

## Evidence policy

Only the three labs above are listed as completed based on the available lab records. Other exploratory payloads (such as `ORDER BY` and column-count tests) are not treated as separate completed labs. Exact full HTTP headers and some final successful payloads were not preserved; each report distinguishes attempts from confirmed outcomes.

The extracted lab password, cookie values, session identifiers, and active lab URLs are intentionally redacted. Review and sanitize screenshots before publishing.

## Scope

All techniques were practiced in intentionally vulnerable PortSwigger training labs. Do not test systems without explicit authorization.
