# plsql-notes
PL/SQL notes.

Originally from https://gist.github.com/AndersDJohnson/6253340/.

## Set current schema
```sql
ALTER SESSION SET CURRENT_SCHEMA=PRODUCTS;
```

## Output
```sql
SET SERVEROUTPUT ON;
BEGIN
DBMS_OUTPUT.PUT_LINE(SYSDATE);
END;
/
```

## All tables
```sql
SELECT * FROM all_tables;
```

## All columns non-system
```sql
SELECT * FROM all_tab_columns WHERE owner NOT IN ('SYS', 'SYSTEM');
```

## Sources
e.g. for stored procedure or function
```sql
select TEXT
from all_source where lower(name) = 'get_product_prices_overlap'
order by line
;
```

## Catch exceptions
e.g. when adding a column that already exists:
```sql
DECLARE
    column_exists exception;
    pragma exception_init (column_exists , -01430); -- ORA-XXXXX e.g. ORA-01430: column being added already exists in table
BEGIN
    EXECUTE IMMEDIATE 'ALTER TABLE ORDERS.ORDER_ITEMS ADD (EVENT_CUSTOMER_JUNS_NUMBER VARCHAR2(50))';
    EXCEPTION
        WHEN column_exists THEN null;
END;
```

## Drop If Exists

http://stackoverflow.com/a/1801453/851135
