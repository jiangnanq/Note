## MySQL usage

* Connect to databse
```
sudo mysql -u root -p
```

* List all tables
```
.table
```

* Describe table
```
.schema tablename
```

* Add table
```
CREATE TABLE bedrecord (
id PRIMARY KEY SERIAL,
bedname TEXT NOT NULL,
status TEXT NOT NULL,
ts TIMESTAMP DEFAULT NOW())
```

* Alter table
```
ALTER TABLE bedrecord
DROP COLUMN ts;
```

* query by time range
```
SELECT * FROM bedrecord WHERE extract(hour from ts) = 17;
```
