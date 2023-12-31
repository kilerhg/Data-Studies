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

## Group by

Enables groups in SQL, being able to create analytics with subgroup.

When using group by be sure that your selected non cumulative field are grouped fields.

### Simple Example

Example counting the name that each name appears at the people table.

```sql
select name, count(name) from people
group by name
```

### Multi Field Example

Example counting the name that each name appears at the people table.

```sql
select name, country, count(name) from people
group by name, country
```

### Having

The way to use where in Group by, write after the group by

Example returns only the name that has more than 10 occurrences

```sql
select names, count(names)
from person
group by names
having count(names) > 10
```

## Join

Select data from more than one table at the same time

### Inner Join

Returns data that happens at both table

```sql
select names
from person
inner join address as a
on person.id = a.person_id
```

### Left Join

Use the first table as the origin and add value to it from the second table.

OBS: Return a line from the first table even if the value it's not on the second table.

```sql
select names
from person
left join address as a
on person.id = a.person_id
```

### Using

Quick way to join tables that has the same join_field in both tables.

Example: Join the tables using the column person_id that is the same at both tables.

```sql
select names
from person
left join address as a
using (person_id)
```

### More than one field to match

A way to be more specific about what data to bring in a join.

Example: Join where the name and the birth_date is the same at both tables.

```sql
select names
from person p
left join address as a
on p.name = a.person_name
    AND p.birth_date = a.birth_date;
```

## References

* [SQL Style Guide](https://www.sqlstyle.guide/)