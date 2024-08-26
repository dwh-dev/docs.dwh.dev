# Strong and Weak dependencies

[**Youtube**](https://youtu.be/jQeVVlqxjj8)

In the [**JOIN and WHERE section**](join-and-where.md), we discussed displaying columns used in JOIN and WHERE clauses. But we wanted to go further :)

Even if columns are data sources, it makes sense to divide them into 2 categories: columns that are direct data sources and columns that only influence them.

For example:

```sql
SELECT
  ROUND(a, b)
FROM t
```

Here, column A is a direct data source, while B is not. B influences the result, but A is the primary source.

Another example:

```sql
SELECT
  CASE
    WHEN A IS NULL
      THEN B
    ELSE C 
  END
FROM t
```

Here, the value from A doesn't appear in the result but affects it.

At [**Dwh.dev**](https://dwh.dev/), we divided such dependencies into classes: **STRONG** and **WEAK**. We annotated all core functions to determine which argument belongs to which class. We also analyze CASE WHEN and other cases. You can disable any of these classes in the settings panel:

<figure><img src="../.gitbook/assets/image (2).png" alt=""><figcaption><p>Weak dependencies</p></figcaption></figure>
