## SELECT Command
### Description:
The SELECT command is used to retrieve data from one or more tables in a database. It allows you to specify which columns you want to retrieve, apply filtering conditions, and control the order of the results.

#### Syntax:
```
SELECT column1, column2, ...
FROM table_name
WHERE condition
ORDER BY column_name ASC|DESC;
```

- column1, column2, ...: Names of the columns you want to retrieve data from. Use * to select all columns.
- table_name: Name of the table from which you want to retrieve data.
- condition: Optional condition to filter the rows returned by the query. It uses comparison operators (e.g., =, <, >, BETWEEN, LIKE) to specify criteria.
- ORDER BY column_name ASC|DESC: Optional clause to sort the result set in ascending (ASC) or descending (DESC) order based on the specified column.
