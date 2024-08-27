# In-query lineage

we realized that no matter how accurately we display column-level lineage between objects, on the **"last mile"** (**within CTAS/VIEW queries**), SQL developers are left without help and spend a lot of time exploring complex queries.

We couldn't let this happen, so we developed a new&#x20;

Now you can go deeper into a selected object's logic and get column-level lineage for the internals of a **SELECT query** with **a** unique feature - **IN-QUERY LINEAGE.**

<figure><img src="https://media.dwh.dev/blog/posts/inquery.gif" alt=""><figcaption><p>In-query lineage</p></figcaption></figure>

In the current "preview" stage, we highlight CTEs, sub-queries, pivots, joins, and unions. We allow collapsing/expanding each sub-query to control the level of detail.

**This functionality is also available for DBT projects.**

\
