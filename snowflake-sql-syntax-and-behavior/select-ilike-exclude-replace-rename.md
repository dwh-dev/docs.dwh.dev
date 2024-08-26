# SELECT \* ILIKE EXCLUDE REPLACE RENAME

Database vendors are competing to see who can come up with the most features for **SELECT \***. **Snowflake** is not lagging and supports as many as 4 modifiers for **SELECT \***:\
**ILIKE EXCLUDE REPLACE RENAME**

We all know that **SELECT \*** is bad. Now it's 4 times worse :)\
Ok, 3. You can't use them all together (either **ILIKE** or **EXCLUDE**).

But the most disgusting modifier is **REPLACE**. It allows you to replace one column with any expression. Good luck debugging, dudes :)

What happens to lineage when using these modifiers? A few examples are collected here: [in 4.select-ilike-exclude-replace-rename.1.sql](https://github.com/dwh-dev/data-lineage-challenge/blob/main/snowflake/4.select-ilike-exclude-replace-rename/sql/4.select-ilike-exclude-replace-rename.1.sql)

Take a look at one of them:

```sql
CREATE TABLE t19(
  id INT,
  c1 BOOLEAN, 
  c2 BOOLEAN,
  c3 BOOLEAN,
  c4 BOOLEAN,
  c12c BOOLEAN
);
CREATE TABLE t20(
  c5 BOOLEAN, 
  c6 BOOLEAN
);

CREATE VIEW v20 AS
  SELECT
    * 
      ILIKE 'c%'
      REPLACE (a.c1 OR b.$2 AS c1)
      RENAME c1 AS c0
  FROM t19 a, t20 b
;
```

At [**Dwh.dev**](https://dwh.dev/), we display it like this:

<figure><img src="../.gitbook/assets/image (16).png" alt=""><figcaption></figcaption></figure>
