# [603. Consecutive Available Seats](https://leetcode.com/problems/consecutive-available-seats/description)

## Description

<!-- description:start -->

<pre>
Several friends at a cinema ticket office would like to reserve consecutive available seats.
Can you help to query all the consecutive available seats order by the seat_id using the following cinema table?
 
Cinema table:
+----------------+
| seat_id | free |
|---------|------|
| 1       | 1    |
| 2       | 0    |
| 3       | 1    |
| 4       | 1    |
| 5       | 1    |
+----------------+

Your query should return the following result for the sample case above.
Result table:
+---------+
| seat_id |
|---------|
| 3       |
| 4       |
| 5       |
+---------+
</pre>

<!-- description:end -->

## Solutions

<!-- solution:start -->

<!-- tabs:start -->

#### MySQL

```sql
# Write your MySQL query statement below
select seat_id
from Cinema
where free = 1 and
     (seat_id - 1 in (select seat_id
                      from Cinema
                      where free = 1)
    or
    seat_id + 1 in (select seat_id
                      from Cinema
                      where free = 1))


-- amazon- 4
```

<!-- tabs:end -->

<!-- solution:end -->


