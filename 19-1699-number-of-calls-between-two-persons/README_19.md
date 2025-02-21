# [1699. Number of Calls Between Two Persons](https://leetcode.com/problems/number-of-calls-between-two-persons/description)

## Description

<!-- description:start -->

<p>Table: <code>Calls</code></p>
 <pre>
+-------------+---------+
| Column Name | Type    |
+-------------+---------+
| from_id     | int     |
| to_id       | int     |
| duration    | int     |
+-------------+---------+
This table does not have a primary key, it may contain duplicates.
This table contains the duration of a phone call between from_id and to_id.
from_id != to_id
</pre>

Write an  SQL query to report the number of  calls and the total call duration between each pair of distinct persons (person1, person2) where person1 < person2.

Return the result table in any order.

The query result format is in the following example:

<pre>
Calls table:
+---------+-------+----------+
| from_id | to_id | duration |
+---------+-------+----------+
| 1       | 2     | 59       |
| 2       | 1     | 11       |
| 1       | 3     | 20       |
| 3       | 4     | 100      |
| 3       | 4     | 200      |
| 3       | 4     | 200      |
| 4       | 3     | 499      |
+---------+-------+----------+

Result table:
+---------+---------+------------+----------------+
| person1 | person2 | call_count | total_duration |
+---------+---------+------------+----------------+
| 1       | 2       | 2          | 70             |
| 1       | 3       | 1          | 20             |
| 3       | 4       | 4          | 999            |
+---------+---------+------------+----------------+
Users 1 and 2 had 2 calls and the total duration is 70 (59 + 11).
Users 1 and 3 had 1 call and the total duration is 20.
Users 3 and 4 had 4 calls and the total duration is 999 (100 + 200 + 200 + 499).
</pre>

<!-- description:end -->

## Solutions

<!-- solution:start -->

<!-- tabs:start -->

#### MySQL

```sql
# Write your MySQL query statement below
-- union all- this gets all calls, then we put condition p1 < p2

select from_id as person1, to_id as person2, count(*) as call_count, sum(duration) as total_duration 
from
    (select from_id, to_id, duration
    from Calls
    union all
    select to_id, from_id, duration
    from Calls) t
where from_id < to_id
group by 1, 2


-- facebook- 2
-- amazon- 1
```

<!-- tabs:end -->

<!-- solution:end -->

