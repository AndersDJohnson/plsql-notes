# plsql-notes
PL/SQL notes.

Originally from https://gist.github.com/AndersDJohnson/6253340/.

## Group by concat
```sql
SELECT LISTAGG(myCol, ', ') WITHIN GROUP (ORDER BY myCol) myCols
/* ... */
GROUP BY
/* ... */
```

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
SELECT * FROM all_tab_columns WHERE owner NOT IN ('SYS', 'SYSTEM')
-- AND lower(table_name) = 'product_refcode_master'
ORDER BY owner, table_name, column_name;
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

## Row Timestamps
```
http://docs.oracle.com/cd/B19306_01/server.102/b14200/functions142.htm
```

## Character Encoding
```
SELECT * FROM NLS_DATABASE_PARAMETERS
WHERE PARAMETER IN ('NLS_CHARACTERSET', 'NLS_NCHAR_CHARACTERSET');
```
