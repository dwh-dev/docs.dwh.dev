# Offline mode

[**Dwh.dev**](https://dwh.dev/) allows you to work without a direct connection to your **Snowflake** instance.

Typically, data lineage tools require information from the **INFORMATION\_SCHEMA**, which is only accessible through a direct connection to your account.

However, we independently compile the schema into an intermediate representation, requiring only the file with DDL statements. This opens up several possibilities:

* You can explore the lineage of only the part of the database that is available to you, without going through all the security procedures adopted in your company when creating a user for a direct connection.
* You can explore the lineage of a database to which you do not have access, but there is a schema description.
* You can upload schema descriptions for multiple databases at once.

To use offline mode, execute the following SQL query in your account:

```sql
SELECT GET_DDL('database', '<dbname>', TRUE);
```

and upload the result to [**Dwh.dev**](https://dwh.dev/).

However, this approach has some downsides:

1. Not all objects of interest can be obtained with this command, and some objects are returned incorrectly. For example, if a **STREAM** is created for an object from another schema, **GET\_DDL** will return an error description. We recommend enriching the results of the **GET\_DDL** function with additional functions from our collection: [https://github.com/dwh-dev/snowflake-get-ddl-tools](https://github.com/dwh-dev/snowflake-get-ddl-tools)
2. The commands in the results of the **GET\_DDL** function are sorted in alphabetical order of object names. For example, if **VIEW v1** depends on **VIEW v2**, you won't be able to run the resulting set of statements without errors. **The good news** is that we can topologically sort DDL statements before compilation. When uploading the file, specify that you are uploading the result of the **GET\_DDL** function, and we will take care of the rest :)

You can also upload files with sets of DML and DDL statements describing your **PIPELINES**. You can retrieve them from **QUERY\_HISTORY** if you do not store them separately.

If you have sets of SELECT statements describing **BI REPORTS**, you can also upload them yourself.

We will also include information about relationships and objects from these files in the overall lineage and catalog.
