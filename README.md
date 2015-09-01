# plsql-notes
Notes on PL/SQL.

Set current schema:

```sql
ALTER SESSION SET CURRENT_SCHEMA=PRODUCTS;
```

Output:

```sql
SET SERVEROUTPUT ON;
BEGIN
DBMS_OUTPUT.PUT_LINE(SYSDATE);
END;
/
```

All tables:
```sql
SELECT * FROM all_tables;
```

All columns on all non-system-owned tables:
```sql
SELECT * FROM all_tab_columns WHERE owner NOT IN ('SYS', 'SYSTEM');
```

Sources (e.g. for stored procedure or function):
```sql
select TEXT
from all_source where lower(name) = 'get_product_prices_overlap'
order by line
;
```
