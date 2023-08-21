# SQL- STRUCTURED QUERY LANGUAGE

# A. DDL Commands
Data Definition Language in SQL is used to define and manage the structure of database objects, such as tables, indexes, views, and schemas. 
- CREATE TABLE
- ALTER TABLE
- DROP TABLE
- CREATE INDEX
- CREATE VIEW
  
## A.1 CREATE 
The CREATE command is used to create a new database object, such as a table, view, index, or schema
```
CREATE TABLE IF NOT EXISTS mytable 
( column DataType TableConstraint DEFAULT default_value,
Column_1 INT PRIMARY KEY,
Column_2 DATE,
Column_3 DATETIME,
Column_4 MONEY,
Column_5 VARCHAR(64),
Column_6 CHAR(size)
Column_7 ENUM(val1, val2,...)
Column_8 BOOLEAN
Column_9 FLOAT(size,d)
FOREIGN KEY(Key_Name) REFERENCES Table_Name(Key_Name)
ON DELETE CASCADE --If one employee ID is deleted, every column will get deleted
)
```
Table Constraints - PRIMARY KEY, UNIQUE, NOT NULL, FOREIGN KEY, CHECK, AUTOINCREMENT
### CREATE INDEX: 
This clause is used to create an index on one or more columns of a table, which improves query performance.
```
CREATE INDEX idx_employees_name ON employees(name);
```
### VIEW
This clause is used to create a virtual table that is based on the result of a query.
```
CREATE VIEW view_name AS
SELECT column_name(s)
FROM table_name
WHERE condition
```
## A.2 ALTER 
 The ALTER command is used to modify the structure of an existing database object. It allows you to add, modify, or drop columns, constraints, indexes, and other properties.
- Add new column(s)
```
ALTER TABLE mytable
ADD column DataType OptionalTableConstraint 
    DEFAULT default_value;
```


Modify the column's DataType
```
ALTER TABLE table_name
MODIFY COLUMN column_name new_data_type;
```
Altering table name
```
ALTER TABLE mytable
RENAME TO new_table_name;
```
Create Constraints: This clause is used to define constraints on table columns, such as primary keys, foreign keys, and check constraints.
```
ALTER TABLE employees
ADD CONSTRAINT pk_employees PRIMARY KEY (id);

ALTER TABLE orders
ADD CONSTRAINT fk_orders_employee_id
FOREIGN KEY (employee_id)
REFERENCES employees(id);

ALTER TABLE customers
ADD CONSTRAINT chk_customer_age
CHECK (age >= 18);
```
Remove column(s)
```
ALTER TABLE mytable
DROP column_to_be_deleted;
```

## A.3 DROP
 The DROP command is used to remove an existing database object, such as a table, view, index, or schema.
```
DROP TABLE IF EXISTS mytable;
```
## A.4 RENAME 
This command is used to rename an existing database object, such as a table or a column. 
```
RENAME table_name TO new_table_name;
```
##  A.5 TRUNCATE 
This command is used to delete all rows from a table, effectively removing all data. It is a fast way to delete all data in a table without actually deleting the table itself.
```
TRUNCATE TABLE table_name;
```
# B. DCL COMMANDS 
Data Control Language in SQL is used to manage access privileges and permissions in a database. The following commands are commonly used in DCL:

### B.1 GRANT
The GRANT command is used to grant specific privileges to users or roles on database objects. It allows you to specify which actions (such as SELECT, INSERT, UPDATE, DELETE) can be performed on specific tables, views, or other database objects.
```
GRANT privilege(s) ON object_name TO user_name;
```
```
GRANT SELECT, INSERT ON employees TO user1;
```
### B.2 REVOKE 
The REVOKE command is used to revoke or remove privileges from users or roles. It allows you to withdraw previously granted privileges from a user or role.
```
REVOKE UPDATE, DELETE ON customers FROM user2;
```
### 3 B.DENY
The DENY command is used to explicitly deny specific privileges to users or roles. It prevents users from performing certain actions on database objects, overriding any previously granted privileges.
```
DENY SELECT, INSERT ON sensitive_table TO user3;
```
# C. TCL
Transaction Control Language in SQL is used to manage transactions, which are sets of database operations that need to be executed atomically (all or nothing).
## C.1 COMMIT
The COMMIT command is used to save the changes made within a transaction. It makes all the changes permanent and releases any locks held on the affected database objects.
```
BEGIN TRANSACTION;
-- SQL statements
COMMIT;
```
## C.2 ROLLBACK 
The ROLLBACK command is used to undo the changes made within a transaction and restore the database to its previous state. It cancels all the operations performed within the transaction.
```
BEGIN TRANSACTION;
-- SQL statements
ROLLBACK;
```
##  C.3 SAVEPOINT
The SAVEPOINT command is used to create a savepoint within a transaction. A savepoint allows you to mark a specific point in a transaction to which you can later rollback, instead of rolling back the entire transaction.
``` 
BEGIN TRANSACTION;
-- SQL statements
SAVEPOINT sp1;
-- More SQL statements
ROLLBACK TO SAVEPOINT sp1;
-- Additional SQL statements
COMMIT;
```
##  C.4 SET TRANSACTION
The SET TRANSACTION command is used to specify characteristics for a transaction, such as isolation level and read/write behavior. It allows you to control how concurrent transactions interact with each other.
``` 
SET TRANSACTION [ISOLATION LEVEL isolation_level] [READ WRITE | READ ONLY];
```
```
SET TRANSACTION ISOLATION LEVEL SERIALIZABLE READ WRITE;
```

# D. DML COMMANDS
## D.1 DELETE
The DELETE command is used to delete rows of data from a table based on specified conditions.
```
DELETE FROM mytable
WHERE condition;
```
## D.2 INSERT 
 The INSERT command is used to insert new rows of data into a table.
 ```
INSERT INTO mytable
(column, another_column, …)
VALUES (value_or_expr, another_value_or_expr, …),
      (value_or_expr_2, another_value_or_expr_2, …),…;
```
## D.3 UPDATE
The UPDATE command is used to modify existing data in a table. It allows you to update values in specific columns based on specified conditions.
```
UPDATE mytable
SET column = value_or_expr, 
    other_column = another_value_or_expr,…
WHERE condition;
```
### ALTER VS UPDATE
|  Alter | Update | 
| ----------- | ----------- |
|DDL|DML|
| will perform all the actions in the table at a structural level|will perform all the actions in the table at the data level|
|adds, deletes, modifies, renames the attributes of the relation|modifies the values of the records in the relations|
|attribute or column specific|attribute-value-specific.|
|ALTER Command by default initializes values of all the tuple as NULL|UPDATE Command sets specified values in the command to the tuples|
|It works on the attributes of a relation|It works on the attribute of a particular tuple in a table|
|ALTER TABLE Students DROP COLUMN Address|UPDATE Students SET Name = ‘SAM’, City= ‘GREEN’ WHERE StudentID = 10;|
|used with MODIFY|used with SET|
### DELETE VS DROP VS TRUNCATE
|  Delete | Drop | Truncate  | 
| ----------- | ----------- | ----------- |
| DML | DDL | DDL | 
| Only some(WHERE clause)rows deleted | ALL Rows,Indexes, privileges deleted | ALL Rows deleted | 
| Slower than TRUNCATE | Quick but could lead to complications | Faster than DELETE |
| Temporary | Permanent | Permanent | 
| Text | Destroys table structure and data | Removes record of table | 

## 4 SELECT
The SELECT command is used to retrieve data from one or more tables or views. It allows you to specify the columns to be selected, apply filtering conditions, join tables, and perform aggregations.
```
SELECT  DISTINCT column, another_column,AGG_FUNC(column_or_expression), …
FROM mytable
    JOIN another_table
      ON mytable.column = another_table.column
    WHERE logicalCondition
        AND/OR another_condition
        AND/OR …;
    GROUP BY columnName
    HAVING constraint_expression
    ORDER BY columnName ASC/DESC
    LIMIT num_limit OFFSET num_offset;
```
- The remaining rows after the **WHERE** constraints are applied are then grouped based on common values in the column specified in the **GROUP BY** clause. As a result of the grouping, there will only be as many rows as there are unique values in that column. Implicitly, this means that you should only need to use this when you have aggregate functions in your query.
- If the query has a **GROUP BY** clause, then the constraints in the HAVING clause are then applied to the grouped rows, discard the grouped rows that don't satisfy the constraint. Like the **WHERE** clause, aliases are also not accessible from this step in most databases.
- **LIMIT** will reduce the number of rows to return, and the optional **OFFSET** will specify where to begin counting the number rows from.</BR>

## THE “BIG 6” ELEMENTS OF A SQL SELECT STATEMENT 

| Clause | Description | Syntax |
| --- | --- |---|
|SELECT|Identifies the column(s) you want your query to select for your results| SELECT columnName |
|FROM|Identifies the table(s) your query will pull data from| FROM tableName |
|WHERE|) Specifies record-filtering criteria for filtering your results| WHERE logicalCondition |
|GROUP BY| Specifies how to group the data in your results| GROUP BY columnName |
|HAVING| Specifies group-filtering criteria for filtering your results| HAVING logicalCondition |
|ORDER BY| Specifies the order in which your query results are displayed| ORDER BY columnName |

### JOINS
| JOIN | Description |
| --- | --- |
|JOIN| combine rows from two or more tables, based on a related column between them. |
|Inner Join| Returns only the matching rows between two tables based on a specified condition,and excludes unmatched records from either table|
|Left Join| Returns all rows from the left table and matching rows from the right table.|
|Right Join| Returns all rows from the right table and matching rows from the left table.|
|Full Outer Join| Returns all rows from both tables, including unmatched rows.|
|Self Join| Joins a table to itself based on a relationship between columns within the same table.|

### Constraints 
| Operator | Condition | Example |
| ----------- | ----------- | ----------- |
| = | Case sensitive exact string comparison (notice the single equals) | col_name = "abc" |
| != or <> | Case sensitive exact string inequality comparison | col_name != "abcd" |
| LIKE |	Case insensitive exact string comparison|	col_name LIKE "ABC" |
|NOT LIKE	|Case insensitive exact string inequality comparison |	col_name NOT LIKE "ABCD" |
|% |	Used anywhere in a string to match a sequence of zero or more characters (only with LIKE or NOT LIKE) | col_name LIKE "%AT%" (matches "AT", "ATTIC", "CAT" or even "BATS") |
| _ |	Used anywhere in a string to match a single character (only with LIKE or NOT LIKE) | col_name LIKE "AN_" (matches "AND", but not "AN") |
| IN (…) | String exists in a list | col_name IN ("A", "B", "C") |
| NOT IN (…) | String does not exist in a list | col_name NOT IN ("D", "E", "F") |
|[]	|Represents any single character within the brackets	|h[oa]t finds hot and hat, but not hit|
|^	|Represents any character not in the brackets|	h[^oa]t finds hit, but not hot and hat|
|-	|Represents any single character within the specified range	|c[a-b]t finds cat and cbt|
.
Determine nth highest slary
```
SELECT salary FROM employee ORDER BY salary desc LIMIT n-1,1;
```
```
SELECT salary FROM employee ORDER BY salary desc LIMIT 1, OFFSET 3;
```
# SQL Functions
|  Function | Description  |  
|---|---|
| EXISTS |  check for the existence of records in a subquery. It returns a boolean value (true or false) based on whether the subquery returns any rows. The subquery can be correlated or uncorrelated. |
| IN | compare a value with a set of values in a list or the result of a subquery. It returns a boolean value (true or false) based on whether the value matches any of the values in the list or subquery result.IN |
| BETWEEN |  selects values within a given range |
| AS | give a table, or a column in a table, a temporary name. |


String Functions

|  Function | Description  |  
|---|---|
|  ASCII | Returns the ASCII value for the specific character |   
| CHAR_LENGTH | Returns the length of a string (in characters) |
| CHARACTER_LENGTH | Returns the length of a string (in characters) |
| CONCAT | Adds two or more expressions together |
| CONCAT_WS | Adds two or more expressions together with a separator |
| FIELD | Returns the index position of a value in a list of values |
| FIND_IN_SET | Returns the position of a string within a list of strings |
| FORMAT | Formats a number to a format like "#,###,###.##", rounded to a specified number of decimal places |
| INSERT | Inserts a string within a string at the specified position and for a certain number of characters |
| INSTR | Returns the position of the first occurrence of a string in another string |
| LCASE | Converts a string to lower-case |
| LEFT | Extracts a number of characters from a string (starting from left) |
| LENGTH | Returns the length of a string (in bytes) |
| LOCATE | Returns the position of the first occurrence of a substring in a string |
| POSITION | Returns the position of the first occurrence of a substring in a string |
| LOWER | Converts a string to lower-case |
| LPAD | Left-pads a string with another string, to a certain length |
| LTRIM | Removes leading spaces from a string |
| MID | Extracts a substring from a string (starting at any position) |
| REPEAT | Repeats a string as many times as specified |
| REPLACE | Replaces all occurrences of a substring within a string, with a new substring |
| REVERSE | Reverses a string and returns the result |
| RIGHT | Extracts a number of characters from a string (starting from right) |
| RPAD | Right-pads a string with another string, to a certain length |
| RTRIM | Removes trailing spaces from a string |
| SPACE | Returns a string of the specified number of space characters |
| STRCMP | Compares two strings |
| SUBSTR | Extracts a substring from a string (starting at any position) |
| SUBSTRING | Extracts a substring from a string (starting at any position) |
| SUBSTRING_INDEX | Returns a substring of a string before a specified number of delimiter occurs |
| TRIM | Removes leading and trailing spaces from a string |
| UCASE | Converts a string to upper-case |
| UPPER | Converts a string to upper-case |

MySQL Numeric Functions

| Function | Description |
| --- | --- |
|ABS|	Returns the absolute value of a number|
|ACOS|	Returns the arc cosine of a number|
|ASIN|	Returns the arc sine of a number|
|ATAN|	Returns the arc tangent of one or two numbers|
|ATAN2	|Returns the arc tangent of two numbers|
|AVG	|Returns the average value of an expression|
|CEIL|	Returns the smallest integer value that is >= to a number|
|CEILING|	Returns the smallest integer value that is >= to a number|
|COS|	Returns the cosine of a number|
|COT|	Returns the cotangent of a number|
|COUNT|	Returns the number of records returned by a select query|
|DEGREES|	Converts a value in radians to degrees|
|DIV|	Used for integer division|
|EXP|	Returns e raised to the power of a specified number|
|FLOOR	|Returns the largest integer value that is <= to a number|
|GREATEST|	Returns the greatest value of the list of arguments|
|AUTO_INCREMENT=100| allows a unique number to be generated automatically when a new record is inserted into a table |
|IDENTITY(10,5)| column should start at value 10 and increment by 5 |
|LEAST|	Returns the smallest value of the list of arguments|
|LN|	Returns the natural logarithm of a number|
|LOG|	Returns the natural logarithm of a number, or the logarithm of a number to a specified base|
|LOG10|	Returns the natural logarithm of a number to base 10|
|LOG2|	Returns the natural logarithm of a number to base 2|
|MAX	|Returns the maximum value in a set of values|
|MIN|	Returns the minimum value in a set of values|
|MOD|	Returns the remainder of a number divided by another number|
|PI	|Returns the value of PI|
|POW|	Returns the value of a number raised to the power of another number|
|POWER	|Returns the value of a number raised to the power of another number|
|RADIANS|	Converts a degree value into radians|
|RAND|	Returns a random number|
|ROUND|	Rounds a number to a specified number of decimal places|
|SIGN|	Returns the sign of a number|
|SIN	|Returns the sine of a number|
|SQRT|	Returns the square root of a number|
|SUM|	Calculates the sum of a set of values|
|TAN|	Returns the tangent of a number|
|TRUNCATE|	Truncates a number to the specified number of decimal places|

MySQL Date Functions

| Function | Description |
| --- | --- |
|ADDDATE	|Adds a time/date interval to a date and then returns the date|
|ADDTIME	|Adds a time interval to a time/datetime and then returns the time/datetime|
|CURDATE	|Returns the current date|
|CURRENT_DATE	|Returns the current date|
|CURRENT_TIME	|Returns the current time|
|CURRENT_TIMESTAMP	|Returns the current date and time|
|CURTIME	|Returns the current time|
|DATE		|Extracts the date part from a datetime expression|
|DATEDIFF	|Returns the number of days between two date values|
|DATE_ADD	|Adds a time/date interval to a date and then returns the date|
|DATE_FORMAT	|Formats a date|
|DATE_SUB	|Subtracts a time/date interval from a date and then returns the date|
|DAY		|Returns the day of the month for a given date|
|DAYNAME	|Returns the weekday name for a given date|
|DAYOFMONTH	|Returns the day of the month for a given date|
|DAYOFWEEK	|Returns the weekday index for a given date|
|DAYOFYEAR	|Returns the day of the year for a given date|
|EXTRACT	|Extracts a part from a given date|
|FROM_DAYS	|Returns a date from a numeric datevalue|
|HOUR		|Returns the hour part for a given date|
|LAST_DAY	|Extracts the last day of the month for a given date|
|LOCALTIME	|Returns the current date and time|
|LOCALTIMESTAMP	|Returns the current date and time|
|MAKEDATE	|Creates and returns a date based on a year and a number of days value|
|MAKETIME	|Creates and returns a time based on an hour, minute, and second value|
|MICROSECOND	|Returns the microsecond part of a time/datetime|
|MINUTE		|Returns the minute part of a time/datetime|
|MONTH		|Returns the month part for a given date|
|MONTHNAME	|Returns the name of the month for a given date|
|NOW		|Returns the current date and time|
|PERIOD_ADD	|Adds a specified number of months to a period|
|PERIOD_DIFF	|Returns the difference between two periods|
|QUARTER	|Returns the quarter of the year for a given date value|
|SECOND		|Returns the seconds part of a time/datetime|
|SEC_TO_TIME	|Returns a time value based on the specified seconds|
|STR_TO_DATE	|Returns a date based on a string and a format|
|SUBDATE	|Subtracts a time/date interval from a date and then returns the date|
|SUBTIME	|Subtracts a time interval from a datetime and then returns the time/datetime|
|SYSDATE	|Returns the current date and time|
|TIME		|Extracts the time part from a given time/datetime|
|TIME_FORMAT	|Formats a time by a specified format|
|TIME_TO_SEC	|Converts a time value into seconds|
|TIMEDIFF	|Returns the difference between two time/datetime expressions|
|TIMESTAMP	|Returns a datetime value based on a date or datetime value|
|TO_DAYS	|Returns the number of days between a date and date "0000-00-00"|
|WEEK		|Returns the week number for a given date|
|WEEKDAY	|Returns the weekday number for a given date|
|WEEKOFYEAR	|Returns the week number for a given date|
|YEAR		|Returns the year part for a given date|
|YEARWEEK	|Returns the year and week number for a given date|

MySQL Advanced Functions

| Function | Description |
| --- | --- |
|BIN		|Returns a binary representation of a number|
|BINARY		|Converts a value to a binary string|
|CASE		|Goes through conditions and return a value when the first condition is met|
|CAST		|Converts a value (of any type) into a specified datatype ``CAST(expression AS datatype(length))`` |
|COALESCE	|Returns the first non-null value in a list``COALESCE(val1, val2, ...., val_n)``|
|CONNECTION_ID	|Returns the unique connection ID for the current connection|
|CONV		|Converts a number from one numeric base system to another|
|CONVERT	|Converts a value into the specified datatype or character set``CONVERT(data_type(length), expression, style)``|
|CURRENT_USER	|Returns the user name and host name for the MySQL account that the server used to authenticate the current client|
|DATABASE	|Returns the name of the current database|
|IF/IFF		|Returns a value if a condition is TRUE, or another value if a condition is FALSE ``IIF(condition, value_if_true, value_if_false)``|
|IFNULL		|Return a specified value if the expression is NULL, otherwise return the expression|
|ISNULL		|Returns 1 or 0 depending on whether an expression is NULL|
|LAST_INSERT_ID	|Returns the AUTO_INCREMENT id of the last row that has been inserted or updated in a table|
|NULLIF		|Compares two expressions and returns NULL if they are equal. Otherwise, the first expression is returned``NULLIF(expr1, expr2)``|
|SESSION_USER	|Returns the current MySQL user name and host name|
|SYSTEM_USER	|Returns the current MySQL user name and host name|
|USER		|Returns the current MySQL user name and host name|
|VERSION	|Returns the current version of the MySQL database|
