# SQL Notes

Notes from more specific knowledge of sql for data

## Style

SELECT, FROM - Key Words always capitalized
tables, customers - tables always lower case, collective name or at last case plural
student, number - fields always singular and lower case

## View

### Create a View

You can easily create a view (kind of a virtual table) from a query using the following snippet.

```sql
CREATE VIEW name_view AS
SELECT column1, column2
FROM table;
```

### Select a View

Select and handle the data from the view just as a normal physical table from sql

```sql
SELECT * FROM name_view;
```

## Using count and Distinct together

Using these both together can be tricky, following a right and wrong example:

### Select all unique counts (Wrong)

This query will not remove the duplicates

```sql
SELECT DISTINCT COUNT(column) FROM TABLE;
```

### Select Counts all unique values (Right)

```sql
SELECT COUNT(DISTINCT column) FROM TABLE;
```

## String Filtering

### Like

`%` to match 0 or n
`_` to match exactly one

#### Example Like

Select everyone that starts with the Letter `L`

```sql
SELECT * FROM people
WHERE name_person = 'L%'
```

Select everyone that starts with the Letter `L` and has a length of 5

## NULL

* `NULL` value are missing values

Filter null using `IS NULL` or `IS NOT NULL`

### NULL with COUNT

When using count and reference the name of the column it will return only not null records, example:

`select count(name) from people;`

But when used with `*` it returns all values, example:

`select count(*) from people;`

## Aggregations

* `SUM` - Sumarize values, only in numeric fields
* `AVG` - Average of the values, only in numeric fields
* `COUNT` - Count how many values
* `MIN` - Get the lowest value (Alphabetical order when dealing with VARCHAR)
* `MAX` - Get the highest value (Alphabetical order when dealing with VARCHAR)

## Numerical Functions

Some very useful functions when handling with numbers

### Round

Structure: `ROUND(column, digits)`

Can only be used in numerical fields

#### Example Round

Round the column salary with 2 digits

`ROUND(salary, 2)`

INPUT - 1000.153
OUTPUT - 1000.15

#### Example Negative Round

You can also round to the left, not only digits:

`ROUND(anual_spending, -3)`

INPUT - 123456.56
OUTPUT - 123000

## References

* [SQL Style Guide](https://www.sqlstyle.guide/)