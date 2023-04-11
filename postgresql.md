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

### Basic

Functions ([Documentation](https://www.postgresql.org/docs/current/functions.html))

Database
```
CREATE DATABASE database_name;
DROP DATABASE database_name;
```

Table ([Data types](https://www.postgresql.org/docs/current/datatype.html))
```SQL
CREATE TABLE table_name (
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
  type_timestamp TIMESTAMP --date and time (no time zone) (2000-12-31 23:59:59),
  unique_value VARCHAR(255) UNIQUE,
  not_null_value VARCHAR(255) NOT NULL
);
```

Insert
```SQL
INSERT INTO table_name (field_1, field_2, field_3)
VALUES ('value_1a', 'value_2b', 'value_3c'),
VALUES ('value_1a', 'value_2b', 'value_3c');
```

Update
```SQL
UPDATE table_name
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
FROM table_name
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
  AND field_10 BETWEEN 10 AND 20
ORDER BY
  field_1 ASC
  field_2 DESC
LIMIT 5
OFFSET 2;
```
```SQL
SELECT * FROM table_name WHERE field = 'value_1' OR field = 'value_2';
```
```SQL
SELECT * FROM table_name WHERE field IN ('value_1', 'value_2'); --OR
```
```SQL
SELECT * FROM (subquery) AS subquery_table_name WHERE field IN (subquery);
```

### Relationships

Primary key
```SQL
CREATE TABLE table_name (
  id SERIAL PRIMARY KEY,
  field VARCHAR(10)
);
```

Foreing key
```SQL
CREATE TABLE table_name (
  id_a INTEGER,
  id_b INTEGER,
  id_c INTEGER REFERENCES table_c (id),
  PRIMARY KEY (id_a, id_b),
  FOREIGN KEY (id_a) REFERENCES table_a (id) ON UPDATE [RESTRICT|CASCADE],
  FOREIGN KEY (id_b) REFERENCES table_b (id) ON DELETE [RESTRICT|CASCADE]
);
```

Join
```SQL
CREATE TABLE table_a (
  id SERIAL PRIMARY KEY,
  field_a VARCHAR(10)
);

CREATE TABLE table_b (
  id SERIAL PRIMARY KEY,
  id_a INTEGER REFERENCES table_a (id),
  field_b VARCHAR(10)
);

SELECT * FROM table_b
JOIN table_a ON table_a.id = table_b.id_a;
```

```SQL
CREATE TABLE table_a (
  id SERIAL PRIMARY KEY,
  field_a VARCHAR(10)
);

CREATE TABLE table_b (
  id SERIAL PRIMARY KEY,
  field_b VARCHAR(10)
);

CREATE TABLE relationship (
  id_a INTEGER REFERENCES table_a (id),
  id_b INTEGER REFERENCES table_b (id),
  PRIMARY KEY (id_a, id_b)
);

SELECT table_a.field_a, table_b.field_b
FROM table_a
JOIN relationship ON relationship.id_a = table_a.id
JOIN table_b ON table_b.id = relationship.id_b;
```

```SQL
CREATE TABLE table_a (
  id INTEGER PRIMARY KEY,
  field_a VARCHAR(10) UNIQUE
);

CREATE TABLE table_b (
  id INTEGER PRIMARY KEY,
  field_b VARCHAR(10) NOT NULL
);

INSERT INTO table_a VALUES (1, 'a_1');
INSERT INTO table_a VALUES (2, 'a_2');
INSERT INTO table_a VALUES (3, 'a_3');
INSERT INTO table_a VALUES (4, 'a_4');

INSERT INTO table_b VALUES (3, 'b_3');
INSERT INTO table_b VALUES (4, 'b_4');
INSERT INTO table_b VALUES (5, 'b_5');
INSERT INTO table_b VALUES (6, 'b_6');

SELECT * FROM table_a;
SELECT * FROM table_b;

SELECT * FROM table_a
JOIN table_b ON table_b.id = table_a.id;

SELECT * FROM table_a
LEFT JOIN table_b ON table_b.id = table_a.id;

SELECT * FROM table_a
RIGHT JOIN table_b ON table_b.id = table_a.id;

SELECT * FROM table_a
FULL JOIN table_b ON table_b.id = table_a.id; --left join + right joint

SELECT * FROM table_a
CROSS JOIN table_b; --cartesian product
```

### Aggregation

Functions ([List](https://www.postgresql.org/docs/9.5/functions-aggregate.html))
```SQL
SELECT
  COUNT(field),
  SUM(field),
  MAX(field),
  MIN(field),
  ROUND(AVG(field), 2) --decimal digits
FROM table_name;
```

Distinct
```SQL
SELECT DISTINCT field FROM table_name; --exclude duplications for selected fields (Do not use with GROUP BY)
```

Group by
```SQL
SELECT field FROM table_name
GROUP BY field;
```

```SQL
SELECT field, count(field)
FROM table_name
GROUP BY field;
```

```SQL
SELECT field, count(field)
FROM table_name
GROUP BY field
HAVING COUNT(field) = 1; --same WHERE statements
```

