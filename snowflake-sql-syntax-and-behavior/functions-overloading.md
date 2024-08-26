# Functions overloading

Snowflake support [procedures and functions overloading](https://docs.snowflake.com/en/developer-guide/udf-stored-procedure-naming-conventions#overloading-procedures-and-functions). You can create multiple UDFs with the same name but with different types of arguments..

Let's create:

```sql
CREATE TABLE A(ID INT);
CREATE TABLE B(S STRING);

CREATE OR REPLACE FUNCTION fn_overload ( _id number )
  RETURNS TABLE (id int)
  AS 'select id from a where id > _id'
;


CREATE OR REPLACE FUNCTION fn_overload ( _s string )
  RETURNS TABLE (s string)
  AS 'select s from b where s != _s'
;
```

The first one has **Table A as a source**, and the second one **Table B**.

Now let's create VIEWs depending on these functions:

```sql
CREATE VIEW V1 AS
SELECT * FROM TABLE(fn_overload(1));

CREATE VIEW V2 AS
SELECT * FROM TABLE(fn_overload('1'));
```

Here is the [**Dwh.dev**](https://dwh.dev/) result:

<figure><img src="../.gitbook/assets/image (17).png" alt=""><figcaption></figcaption></figure>
