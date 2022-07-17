## PostgreSQL

### Configuration

Change default user password
```
sudo -u postgres psql -c "ALTER USER postgres PASSWORD 'postgres'"
```

Command line
```
sudo -u postgres psql
```

### Basic commands

Database
```
CREATE DATABASE [name];
DROP DATABASE [name];
```

Table ([Data types](https://www.postgresql.org/docs/current/datatype.html))
```SQL
CREATE TABLE [table] (
  type_serial SERIAL, --autoincrementing four-byte integer
  type_varchar VARCHAR(255), --variable-length character string
  type_char CHAR(10), --fixed-length character string
  type_text TEXT, --variable-length character string
  type_integer INTEGER, --signed four-byte integer
  type_numeric NUMERIC(5,2), --exact numeric of selectable precision (99999,99)
  type_real REAL, --single precision floating-point number (4 bytes)
  type_boolean BOOLEAN, --logical Boolean (true/false)
  type_date DATE, --calendar date (year, month, day) (2000-12-31)
  type_time TIME, --time of day (no time zone) (23:59:59.999)
  type_timestamp TIMESTAMP --date and time (no time zone) (2000-12-31 23:59:59)
);
```

Insert
```SQL
INSERT INTO [table] (field_1, field_2, field_3)
VALUES ('value_1', 'value_2', 'value_3');
```

Update
```SQL
UPDATE [table]
SET
  field_1 = 'new_value_1',
  field_2 = 'new_value_2'
WHERE
  id = 1;
```

Select where
```SQL
SELECT
  field_1 AS "Field 1",
  field_2 AS field_2_name
FROM [table]
WHERE
  id = 1
  AND field_1 <> 'value' --different
  AND field_2 != 'value' --different
  AND field_3 LIKE 'va_ue' --any character
  AND field_4 LIKE '%ue' --any string
  AND field_5 NOT LIKE 'va_ue'
  AND field_6 IS NULL
  AND field_7 IS NOT NULL
  AND field_8 > 10 --comparators (>, >=, <, <=)
  AND field_10 BETWEEN 10 AND 20;
```
```SQL
SELECT * FROM [table] WHERE field = 'value_1' OR field = 'value_2';
```

### Relationships

Primary key
```SQL
CREATE TABLE [table] (
  id SERIAL PRIMARY KEY,
  field VARCHAR(10)
);
```

Foreing key
```SQL
CREATE TABLE [table] (
  id_a INTEGER,
  id_b INTEGER,
  PRIMARY KEY (id_a, id_b),
  FOREIGN KEY (id_a) REFERENCES table_a (id) ON UPDATE [RESTRICT|CASCADE],
  FOREIGN KEY (id_b) REFERENCES table_b (id) ON DELETE[RESTRICT|CASCADE]
);
```
