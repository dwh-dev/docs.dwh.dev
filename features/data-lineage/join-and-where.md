# JOIN and WHERE

Typically, data lineage tools provide information about the immediate movement of data within the database:

```sql
CREATE VIEW v1
AS 
  SELECT c1
  FROM t1
```

Data from the column **t1.c1** flows into **v1.c1**:

<figure><img src="../../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

However, this data might be insufficient when it comes to refactoring. For instance, when certain columns aren't involved in the data movement but are only involved in **JOIN** or **WHERE** clauses:

```sql
CREATE VIEW v2
AS 
  SELECT c1
  FROM t1
    JOIN t2 ON t1.id = t2.parent_id
  WHERE 
    t1.c2 > t2.f2
```

Usually, data lineage tools won't provide information about columns **t1.id, t1.c2, t2.parent\_id, t2.f2**, but at [**Dwh.dev**](https://dwh.dev/), we've made them visible!

<figure><img src="../../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>
