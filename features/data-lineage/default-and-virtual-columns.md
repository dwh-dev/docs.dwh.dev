# Default and Virtual Columns

[**Youtube**](https://youtu.be/eLi8CnXP8LA)

**Default and Virtual Columns** also contain information about data lineage. And as usual, nobody pays attention to it :)

```sql
-- default value
CREATE TABLE t1 (
  id1 int,
  id2 int default (id1 +1)
);

CREATE VIEW v1 AS
  SELECT *
  FROM t1
;
```

If during data transformations, only the id1 column is inserted into the **T1** table, the lineage information will be lost.

At [**Dwh.dev**](https://dwh.dev/), we display it like this:

<figure><img src="../../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

With **Virtual columns**, an even more precarious situation arises. It's impossible to insert data into a virtual column, and they will ALWAYS depend on other columns in the table.

```sql
-- virtual column
CREATE TABLE T2 (
  A INT,
  B INT,
  C INT,
  D INT AS (CASE WHEN A>0 THEN B ELSE C END)
);

CREATE VIEW v2 AS
  SELECT *
  FROM t2
;
```

At [**Dwh.dev**](https://dwh.dev/), we display it like this:&#x20;

<figure><img src="../../.gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>
