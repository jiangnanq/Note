## Postgresql usage

* Connect to databse
```
psql -h localhost -d database -U user -W
```

* List all tables
```
\dt
```

* Describe table
```
\d tablename
```

* Add table
```
CREATE TABLE bedrecord (
id SERIAL,
bedname TEXT NOT NULL,
status TEXT NOT NULL,
ts TIMESTAMP DEFAULT NOW())
```

* Alter table
```
ALTER TABLE bedrecord
DROP COLUMN ts;
```
