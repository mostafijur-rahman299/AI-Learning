
## SQL Advance Topics

### AND/OR/IN Operators

```sql
CREATE TABLE exercise_logs
    (id INTEGER PRIMARY KEY AUTOINCREMENT,
    type TEXT,
    minutes INTEGER, 
    calories INTEGER,
    heart_rate INTEGER);


INSERT INTO exercise_logs(type, minutes, calories, heart_rate) VALUES ("biking", 30, 100, 110);
INSERT INTO exercise_logs(type, minutes, calories, heart_rate) VALUES ("biking", 10, 30, 105);
INSERT INTO exercise_logs(type, minutes, calories, heart_rate) VALUES ("dancing", 15, 200, 120);
INSERT INTO exercise_logs(type, minutes, calories, heart_rate) VALUES ("tree climbing", 30, 70, 90);
INSERT INTO exercise_logs(type, minutes, calories, heart_rate) VALUES ("tree climbing", 25, 72, 80);
INSERT INTO exercise_logs(type, minutes, calories, heart_rate) VALUES ("rowing", 30, 70, 90);
INSERT INTO exercise_logs(type, minutes, calories, heart_rate) VALUES ("hiking", 60, 80, 85);


SELECT * FROM exercise_logs WHERE calories > 50 ORDER BY calories;

-- AND
SELECT * FROM exercise_logs WHERE calories > 50 AND minutes < 30;

-- OR
SELECT * FROM exercise_logs WHERE calories > 50 OR heart_rate > 200;

-- IN / NOT IN
SELECT * FROM exercise_logs WHERE type IN("biking", "dancing");
SELECT * FROM exercise_logs WHERE type NOT IN("biking", "dancing");
```

### Subqueries
```sql
CREATE TABLE drs_favorites
    (id INTEGER PRIMARY KEY,
    type TEXT,
    reason TEXT);

INSERT INTO drs_favorites(type, reason) VALUES ("biking", "Improves endurance and flexibility.");
INSERT INTO drs_favorites(type, reason) VALUES ("hiking", "Increases cardiovascular health.");

SELECT type FROM drs_favorites;

SELECT * FROM exercise_logs WHERE type IN ("biking", "hiking");

-- Subqueries
SELECT * FROM exercise_logs WHERE type IN (SELECT type FROM drs_favorites);

-- LIKE Operator Which is acting as like contains
SELECT * FROM exercise_logs WHERE type IN (
  SELECT type FROM drs_favorites WHERE reason LIKE("%help%"));

```

### HAVING With Aggregate
```sql
SELECT type, SUM(calories) AS total_calories FROM exercise_logs GROUP BY type;

SELECT type, SUM(calories) AS total_calories FROM exercise_logs GROUP BY type HAVING total_calories > 550;

SELECT type FROM exercise_logs GROUP BY type HAVING COUNT(*) >= 2;

```

### WHEN/CASE
```sql
SELECT COUNT(*), type, heart_rate,
    CASE 
        WHEN heart_rate > 220-30 THEN "above max"
        WHEN heart_rate > ROUND(0.90 * (220-30)) THEN "above target"
        WHEN heart_rate > ROUND(0.50 * (220-30)) THEN "within target"
        ELSE "below target"
    END as "hr_zone"
FROM exercise_logs
GROUP BY hr_zone;
```