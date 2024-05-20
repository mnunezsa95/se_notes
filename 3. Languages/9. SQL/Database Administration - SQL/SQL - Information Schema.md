See [[SQL - Introduction to SQL]]

Resources
* The [information schema](https://postgrespro.com/docs/postgresql/9.5/information-schema) official documentation

---
#### The information schema
The information schema contains more than fifty tables, each belonging to a specific object or group of objects
- `information_schema.tables` --> stores information about all tables
- `information_schema.columns` --> stores information about all fields in all tables
- `information_schema.constraint_column_usage` --> stores information about field constraints
- `constraint_schema` field --> stores the name of the schema that contains a constraint.

* Examples
```SQL
--- using information schema to print all the tables in the `mobile_app` schema
SELECT *
FROM information_schema.tables t 
WHERE table_schema = 'mobile_app'; 
```

```sql
--- using information schema to print primary keys
SELECT *
FROM information_schema.table_constraints tc
WHERE table_schema = 'mobile_app' 
          AND constraint_type = 'PRIMARY KEY'; 
```

```SQL 
--- using information schema to check field constraints
SELECT *
FROM information_schema.constraint_column_usage
WHERE table_schema = 'mobile_app'; 
```

```sql
-- finding exact constraints using `check_constraints` table
SELECT constraint_schema, 
       constraint_name,
       check_clause
FROM information_schema.check_constraints cc2 
WHERE constraint_schema = 'mobile_app'; 
```

#### Examples from Exercise
```SQL
SELECT data_type,
       character_octet_length,
       numeric_precision,
       numeric_precision_radix,
       numeric_scale,
       datetime_precision
FROM information_schema.columns 
WHERE table_schema = 'mobile_app'; 
```