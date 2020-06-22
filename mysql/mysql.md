## MySQL

```
ALTER TABLE <table_name> MODIFY <column_name> VARCHAR(255) CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
```

```
SELECT TABLE_SCHEMA, TABLE_NAME, COLUMN_NAME, COLLATION_NAME, COLUMN_TYPE 
FROM information_schema.columns 
WHERE COLLATION_NAME != 'utf8_general_ci' 
AND TABLE_SCHEMA NOT IN ('information_schema','mysql', 'performance_schema','sys') 
AND TABLE_SCHEMA = '<schema_name>'
```

```
ALTER DATABASE <database_name> DEFAULT CHARACTER SET utf8 COLLATE utf8_general_ci;
```

```
ALTER TABLE <table_name> DEFAULT CHARACTER SET utf8 COLLATE utf8_general_ci;
```

```
ALTER TABLE <table_name> ENGINE = InnoDB;
```

```
SELECT TABLE_NAME,ENGINE
FROM   information_schema.TABLES
WHERE  TABLE_SCHEMA = <database_name> and ENGINE = 'myISAM'
```

```
ALTER TABLE <table_name> CHARACTER SET utf8mb4, COLLATE utf8mb4_unicode_ci;
```

```
ALTER TABLE <table_name> CONVERT TO CHARACTER SET utf8mb4_unicode_ci;
```