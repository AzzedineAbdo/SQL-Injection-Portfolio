# Secure SQL Queries — Remediation Reference

## 1. Parameterize values

Unsafe string concatenation:
```python
query = "SELECT * FROM products WHERE category = '" + category + "'"
cursor.execute(query)
```

Safer parameter binding (placeholder syntax depends on the driver):
```python
query = "SELECT * FROM products WHERE category = %s"
cursor.execute(query, (category,))
```

## 2. Allow-list identifiers
SQL parameters bind values, not usually identifiers. Map user choices to hard-coded identifiers:
```python
allowed_sort_columns = {
    "name": "product_name",
    "price": "price",
}
sort_column = allowed_sort_columns.get(user_sort, "product_name")
query = f"SELECT product_id, product_name, price FROM products ORDER BY {sort_column}"
cursor.execute(query)
```

## 3. Least privilege
- Use separate database accounts for application functions.
- Grant only required permissions.
- Do not run the application as a database administrator.
- Restrict access to system catalogs and sensitive tables.

## 4. Error handling
- Do not expose raw SQL errors, query text, schema names, or DBMS banners.
- Log diagnostics securely on the server.
- Return generic external errors.

## 5. Reduce inference channels
- Avoid distinguishable responses that disclose whether predicates are true.
- Review status codes, response body lengths, and timing.
- Do not treat response normalization as a substitute for parameterized queries.

## 6. Credential and cookie security
- Store passwords with modern adaptive password hashing and unique salts.
- Use Secure, HttpOnly, and SameSite cookie attributes as appropriate.
- Rotate credentials and invalidate sessions after suspected compromise.
- Never commit tokens or recovered passwords.

## 7. Verification checklist
- [ ] All SQL values use parameter binding.
- [ ] Dynamic identifiers use strict allow-lists.
- [ ] Database accounts follow least privilege.
- [ ] Errors do not disclose SQL internals.
- [ ] Regression tests cover boolean, UNION, and blind SQLi.
- [ ] Logs monitor suspicious SQL syntax.
- [ ] Secrets are redacted from reports, screenshots, and Git history.
