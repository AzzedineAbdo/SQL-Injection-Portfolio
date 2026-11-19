# Lab 01 — Retrieve hidden data using SQL injection

## Lab Overview
| Field | Details |
|---|---|
| Platform | PortSwigger Web Security Academy |
| Vulnerability | In-band SQL injection; boolean-condition manipulation |
| Parameter | `category` |
| Request | `GET /filter?category=...` |
| Outcome | Solved banner visible in supplied screenshot (DOCX page 1) |

## Vulnerability Description
The product filter accepted a category value that could alter the logic of the underlying SQL query. The evidence shows a boolean condition submitted through `category`, followed by the lab success banner. The exact backend SQL statement and DBMS are not known.

## Testing Methodology
1. Identify `category` in the product filter URL.
2. Intercept or inspect the GET request.
3. Modify the parameter with a boolean condition.
4. Submit the request and inspect the rendered page.
5. Confirm completion using the visible success banner.

## Step-by-Step Exploitation
The recorded test used `OR 1=1` in the category parameter. The supplied screenshot shows the product listing and a congratulations banner.

## HTTP Request Analysis
Observed request shape:
```http
GET /filter?category='+OR+1=1-- HTTP/1.1
Host: <REDACTED>
```
Full headers, cookies, and exact raw request formatting were not preserved.

## Payload Analysis
```sql
' OR 1=1--
```
- `'` attempts to close the original string literal.
- `OR 1=1` adds a condition that evaluates true.
- `--` starts an SQL comment in dialects that support it; comment syntax and whitespace requirements vary by DBMS.

## Evidence and Screenshots
Source: supplied DOCX, page 1. It includes the filter URL and a screenshot with the lab success banner. Add only a genuine, sanitized screenshot:
`![Sanitized Lab 01 evidence](../../Screenshots/Lab-01-sanitized.png)`

## Security Impact
If untrusted filter input is concatenated into SQL, an attacker may alter query logic and retrieve records outside the intended filter.

## Risk Severity
**Suggested: High, context-dependent.** Actual severity depends on reachable data, database privileges, authentication, and exploitability. This is a lab assessment, not a production finding.

## Remediation
- Use parameterized queries / prepared statements.
- Never concatenate untrusted input into SQL.
- Map user-selectable categories to server-side allow-listed values.
- Apply least-privilege database permissions.
- Add regression tests for SQL metacharacters and boolean conditions.

## Lessons Learned
- Query parameters are untrusted input.
- Boolean conditions can expose SQL injection through application behavior.
- A lab success banner is completion evidence; a payload alone is not.
