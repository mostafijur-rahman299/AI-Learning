```sql
-- CREATE TABLE groceries(id INTEGER PRIMARY KEY, name text, quantity INTEGER);
-- INSERT INTO groceries VALUES(1, "Banana", 24);
-- INSERT INTO groceries VALUES(2, "Apple", 12);
-- INSERT INTO groceries VALUES(4, "Apple", 12);
-- INSERT INTO groceries VALUES(3, "Mango", 90);

-- Retrieve all columns value
-- SELECT * FROM groceries;

-- Retrieve a single column value
-- SELECT name FROM groceries;

-- Ordering
-- SELECT * FROM groceries ORDER BY name;

-- Filtering
-- SELECT * FROM groceries WHERE name="Apple";

-- Aggregating data
-- SELECT SUM(quantity) FROM groceries;
-- SELECT quantity, COUNT(quantity) FROM groceries GROUP BY name;
```
