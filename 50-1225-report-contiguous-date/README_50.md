# [1225. Report Contiguous Dates](https://leetcode.com/problems/report-contiguous-dates/description/)

## Description

<!-- description:start -->

<p>Table: <code>Failed</code></p>
<pre>
+--------------+---------+
| Column Name  | Type    |
+--------------+---------+
| fail_date    | date    |
+--------------+---------+
Primary key for this table is fail_date.
Failed table contains the days of failed tasks.
</pre>
 
<p>Table: <code>Succeeded</code></p>
<pre>
+--------------+---------+
| Column Name  | Type    |
+--------------+---------+
| success_date | date    |
+--------------+---------+
Primary key for this table is success_date.
Succeeded table contains the days of succeeded tasks.
</pre>

A system is running one task every day. Every task is independent of the previous tasks. The tasks can fail or succeed.

Write an  SQL query to generate a report of period_state for each continuous interval of days in the period from 2019-01-01 to 2019-12-31.


period_state is 'failed' if tasks in this interval failed or 'succeeded' if tasks in this interval succeeded. Interval of days are retrieved as start_date and end_date.

Order result by start_date.

The query result format is in the following example:

<pre>
Failed table:
+-------------------+
| fail_date         |
+-------------------+
| 2018-12-28        |
| 2018-12-29        |
| 2019-01-04        |
| 2019-01-05        |
+-------------------+

Succeeded table:
+-------------------+
| success_date      |
+-------------------+
| 2018-12-30        |
| 2018-12-31        |
| 2019-01-01        |
| 2019-01-02        |
| 2019-01-03        |
| 2019-01-06        |
+-------------------+
 
Result table:
+--------------+--------------+--------------+
| period_state | start_date   | end_date     |
+--------------+--------------+--------------+
| succeeded    | 2019-01-01   | 2019-01-03   |
| failed       | 2019-01-04   | 2019-01-05   |
| succeeded    | 2019-01-06   | 2019-01-06   |
+--------------+--------------+--------------+
The report ignored the system state in 2018 as we care about the system in the period 2019-01-01 to 2019-12-31.
From 2019-01-01 to 2019-01-03 all tasks succeeded and the system state was "succeeded".
From 2019-01-04 to 2019-01-05 all tasks failed and system state was "failed".
From 2019-01-06 to 2019-01-06 all tasks succeeded and system state was "succeeded".
</pre>

<!-- description:end -->

## Solutions

<!-- solution:start -->

<!-- tabs:start -->

#### MySQL

```sql
# Write your MySQL query statement below
with cte1 as
    ((select fail_date as event_date, 'failed' as status
    from Failed)
    union all
    (select success_date as event_date, 'succeeded' as status
    from Succeeded)),
    cte2 as
    (select *,
        row_number() over(order by event_date) as rn,
        dense_rank() over (partition by status order by event_date) as rnk,
        row_number() over(order by event_date) - dense_rank() over (partition by status order by event_date) as diff   
    from cte1
    where event_date between '2019-01-01' and '2019-12-31'
    order by 1)

select status as period_state, min(event_date) as start_date, max(event_date) as end_date
from cte2
group by status, diff
order by 2

-- facebook- 1
```

<!-- tabs:end -->

<!-- solution:end -->

