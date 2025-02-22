# [1285. Find the Start and End Number of Continuous Ranges](https://leetcode.com/problems/find-the-start-and-end-number-of-continuous-ranges/description)

## Description

<!-- description:start -->

<p>Table: <code>Logs</code></p>
<pre>
+---------------+---------+
| Column Name   | Type    |
+---------------+---------+
| log_id        | int     |
+---------------+---------+
log_id is the column of unique values for this table.
Each row of this table contains the ID in a log Table.
</pre>

Write a solution to find the start and end number of continuous ranges in the table Logs.

Return the result table ordered by start_id.

The result format is in the following example.

<pre>
Logs table:
+------------+
| log_id     |
+------------+
| 1          |
| 2          |
| 3          |
| 7          |
| 8          |
| 10         |
+------------+

Result table:
+------------+--------------+
| start_id   | end_id       |
+------------+--------------+
| 1          | 3            |
| 7          | 8            |
| 10         | 10           |
+------------+--------------+
Explanation: 
The result table should contain all ranges in table Logs.
From 1 to 3 is contained in the table.
From 4 to 6 is missing in the table
From 7 to 8 is contained in the table.
Number 9 is missing from the table.
Number 10 is contained in the table.
</pre>

<!-- description:end -->

## Solutions

<!-- solution:start -->

<!-- tabs:start -->

#### MySQL

```sql
# Write your MySQL query statement below
-- row number- created just to look at what it looks like
-- continuous ranges have same differences from row number
-- so pick min as start, max as end and group by diff

select min(log_id) as start_id, max(log_id) as end_id
from
    (select log_id, 
        row_number() over(order by log_id) as rn, 
        log_id - row_number() over(order by log_id) as diff
    from Logs) temp
group by diff


-- microsoft- 1
```

<!-- tabs:end -->

<!-- solution:end -->

