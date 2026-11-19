# Lab 02 — SQL injection attack, querying the database type and version on MySQL and Microsoft

## Lab Overview
| Field | Details |
|---|---|
| Platform | PortSwigger Web Security Academy |
| Vulnerability | UNION-based SQL injection; DBMS fingerprinting |
| Parameter | `category` |
| Request shape | `GET /filter?category=...` |
| Outcome | Prior conversation records explicit `LAB Solved` and congratulations markers |

## Vulnerability Description
The lab involved injecting UNION queries through the category filter to retrieve database information. Work included column compatibility tests and DBMS-specific version expressions. The evidence does not identify one definitive final successful payload, so recorded attempts are not represented as individually successful.

## Testing Methodology
1. Locate `category` in the filter request.
2. Send the request to Burp Repeater.
3. Test UNION SELECT expressions and column compatibility.
4. Try DBMS-specific version expressions.
5. Inspect response content and lab completion state.

## Step-by-Step Exploitation
The supplied DOCX shows UNION and version-query attempts. The prior conversation records the lab title, an expected MySQL version value (`8.0.42-0ubuntu0.20.04.1`), and a response containing `is-solved`, `Solved`, and “Congratulations, you solved the lab!”. An HTTP 500 was also observed, but the body contained explicit completion markers.

## HTTP Request Analysis
Observed shape:
```http
GET /filter?category=<injected-value> HTTP/2
Host: <REDACTED>
```
A specific attempted request in the DOCX:
```http
GET /filter?category='+UNION+SELECT+BANNER,+NULL+FROM+v$version-- HTTP/2
```
Complete raw headers, cookies, and the definitive successful request are unavailable.

## Payload Analysis
Recorded attempts:
```sql
' UNION SELECT 'abc','def' FROM dual--
' UNION SELECT BANNER, NULL FROM v$version--
' UNION SELECT @@version, NULL#
' UNION SELECT 'abc','def'#
' UNION SELECT 'abcdef',NULL,NULL--
```
`UNION SELECT` appends a result set; the number of columns and compatible data types must match. `dual` and `v$version` are Oracle-associated constructs. `@@version` is used by multiple DBMSs with dialect-specific behavior. `#` is a MySQL comment marker; `--` handling varies. These are recorded attempts, not a claim that each succeeded.
## Evidence and Screenshots

The following screenshots document the UNION-based SQL injection testing process.

### 1. UNION SELECT Response
![UNION SELECT response](../../Screenshots/Lab-02/01-union-select-response.png)

### 2. UNION Request
![UNION request](../../Screenshots/Lab-02/02-union-request-redacted.png)

### 3. UNION SELECT Testing
![UNION SELECT test](../../Screenshots/Lab-02/03-union-select-test.png)

### 4. Follow-up UNION Testing
![UNION SELECT follow-up](../../Screenshots/Lab-02/04-union-select-followup.png)

## Security Impact
UNION injection may expose data through the application's normal response. Version disclosure can help attackers identify DBMS-specific weaknesses.

## Risk Severity
**Suggested: High, context-dependent.** Data extraction may be high impact; version disclosure alone is generally lower impact. Production severity requires impact validation.

## Remediation
- Use parameter binding.
- Allow-list dynamic identifiers and filter choices.
- Apply least privilege.
- Suppress raw SQL errors and database banners.
- Monitor repeated SQL syntax probes.

## Lessons Learned
- UNION queries require matching column counts and compatible types.
- DBMS syntax must be validated rather than assumed.
- HTTP 500 alone does not prove failure; inspect response content and explicit lab state.
- Separate attempted payloads from confirmed successful payloads.
