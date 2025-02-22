# [1303. Find the Team Size](https://leetcode.com/problems/find-the-team-size/description)

## Description

<!-- description:start -->

<p>Table: <code>Employee</code></p>
<pre>
+---------------+---------+
| Column Name   | Type    |
+---------------+---------+
| employee_id   | int     |
| team_id       | int     |
+---------------+---------+
employee_id is the primary key for this table.
Each row of this table contains the ID of each employee and their respective team.
</pre> 

Write an  SQL query to find the team size of each of the employees.

Return result table in any order.

The query result format is in the following example:

<pre>
Employee Table:
+-------------+------------+
| employee_id | team_id    |
+-------------+------------+
|     1       |     8      |
|     2       |     8      |
|     3       |     8      |
|     4       |     7      |
|     5       |     9      |
|     6       |     9      |
+-------------+------------+
Result table:
+-------------+------------+
| employee_id | team_size  |
+-------------+------------+
|     1       |     3      |
|     2       |     3      |
|     3       |     3      |
|     4       |     1      |
|     5       |     2      |
|     6       |     2      |
+-------------+------------+
Employees with Id 1,2,3 are part of a team with team_id = 8.
Employees with Id 4 is part of a team with team_id = 7.
Employees with Id 5,6 are part of a team with team_id = 9.
</pre>

<!-- description:end -->

## Solutions

<!-- solution:start -->

<!-- tabs:start -->

#### MySQL

```sql
# Write your MySQL query statement below
-- if we do not use order by in over(), we do not get running total, just normal aggregate for all rows within that partition

select employee_id, count(*) over(partition by team_id) as team_size
from Employee
order by 1

-- amazon- 1
```

<!-- tabs:end -->

<!-- solution:end -->

