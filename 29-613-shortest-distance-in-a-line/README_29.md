# [613. Shortest Distance in a Line](https://leetcode.com/problems/shortest-distance-in-a-line/description)

## Description

<!-- description:start -->

<p>Table: <code>Point</code></p>

<pre>
+-------------+------+
| Column Name | Type |
+-------------+------+
| x           | int  |
+-------------+------+
In SQL, x is the primary key column for this table.
Each row of this table indicates the position of a point on the X-axis.
</pre>

<p>&nbsp;</p>

<p>Find the shortest distance between any two points from the <code>Point</code> table.</p>

<p>The result format is in the following example.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> 
Point table:
+----+
| x  |
+----+
| -1 |
| 0  |
| 2  |
+----+
<strong>Output:</strong> 
+----------+
| shortest |
+----------+
| 1        |
+----------+
<strong>Explanation:</strong> The shortest distance is between points -1 and 0 which is |(-1) - 0| = 1.
</pre>

<p>&nbsp;</p>
<p><strong>Follow up:</strong> How could you optimize your solution if the <code>Point</code> table is ordered <strong>in ascending order</strong>?</p>

<!-- description:end -->

## Solutions

<!-- solution:start -->

<!-- tabs:start -->

#### MySQL

```sql
# Write your MySQL query statement below
select min(abs(p1.x - p2.x)) as shortest
from Point p1 cross join Point p2
where p1.x != p2.x

-- no companies listed
```

<!-- tabs:end -->

<!-- solution:end -->

