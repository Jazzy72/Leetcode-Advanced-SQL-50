# [1112. Highest-Grade-For-Each-Student](https://leetcode.com/problems/highest-grade-for-each-student/description)

## Description

<!-- description:start -->

<p>Table: <code>Enrollments</code></p>
 <pre>
+---------------+---------+
| Column Name   | Type    |
+---------------+---------+
| student_id    | int     |
| course_id     | int     |
| grade         | int     |
+---------------+---------+
(student_id, course_id) is the primary key (combination of columns with unique values) of this table.
grade is never NULL.
 

Write a solution to find the highest grade with its corresponding course for each student. In case of a tie, you should find the course with the smallest course_id.

Return the result table ordered by student_id in ascending order.

The result format is in the following example.
 </pre>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>
<pre>
<strong>Input:</strong> 
Enrollments table:
+------------+-------------------+
| student_id | course_id | grade |
+------------+-----------+-------+
| 2          | 2         | 95    |
| 2          | 3         | 95    |
| 1          | 1         | 90    |
| 1          | 2         | 99    |
| 3          | 1         | 80    |
| 3          | 2         | 75    |
| 3          | 3         | 82    |
+------------+-----------+-------+
<strong>Output:</strong> 
+------------+-------------------+
| student_id | course_id | grade |
+------------+-----------+-------+
| 1          | 2         | 99    |
| 2          | 2         | 95    |
| 3          | 3         | 82    |
+------------+-----------+-------+
</pre>
<!-- description:end -->

## Solutions

<!-- solution:start -->

<!-- tabs:start -->

#### MySQL

```sql
# Write your MySQL query statement below
select o.customer_id, c.customer_name
from Orders o
left join Customers c
on c.customer_id = o.customer_id
group by o.customer_id
having sum(product_name='A') > 0 and sum(product_name='B') > 0 and sum(product_name='C') = 0
order by 1

-- amazon- 2
-- facebook- 1
```

<!-- tabs:end -->

<!-- solution:end -->

