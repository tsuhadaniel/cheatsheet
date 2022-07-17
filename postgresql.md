## PostgreSQL

Change default user password
```
sudo -u postgres psql -c "ALTER USER postgres PASSWORD 'postgres'"
```

Command line
```
sudo -u postgres psql
```

Database
```
CREATE DATABASE [name];
DROP DATABASE [name];
```

Table ([Data types](https://www.postgresql.org/docs/current/datatype.html))
```SQL
CREATE TABLE [name] (
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
