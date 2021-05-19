# 

## subquery

### 1. simple subquery

can run independent

### 2. correlated subquery

- dependent on the main query to excute
- evaluated in loops
- significantly slow down the query runtime

### 3. nested subquery

## common table expression

- declare before main query
- named and referenced later

```{sql}
with cte1 as (
	select
	from
),
	cte2 as (
	select 
	from 
	)
```

## window functions

- perform calculations on already generated result
- aggregate calculations

extract(month from date)
extract(day from date)


## summary stats and window function

### anatomy of a windows function

function_name() over(...)
 - order by
 - partition by split the table into partitions based on a column's unique values
		- row_number will reset for each partition
		- lag will only fetch a row's previous value if its previous is in the same parition
 - rows/range preceding/following/unbounded
  
```{sql}
row_number()  
#assign unique number
rank()  			
#assign the same number to rows with identical value, skip over the next number.
dense_rank()  
#assign the same number, do not skip

```

window start at the beginning of the table and ends at current row.

`ntile()`

```{sql}
last_value(city) over (
oerder by year asc
range between
	unbounded preceding and
	unbounded following
	) as last_city
```

`rows between [start] and [finish]`

- `n preceding` : `n` rows before the current row
- `CURRENT ROW` : the current row
- `n FOLLOWING` : `n` rows after the current row
used over range between


`range between [strat] and [finish]`

- functions much the same as rows between
- range treats duplicates in over's order by subclause as a single entity,
add the together first.

```{sql}
CREATE EXTENSION IF NOT EXITS tablefunc;
SELECT * FROM CROSSTAB($$
  **
$$) AS ct (gender VARCHAR,
          "2004" INTEGER,
          )

```
