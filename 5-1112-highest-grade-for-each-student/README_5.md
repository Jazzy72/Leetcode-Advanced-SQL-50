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
 </pre>

<p>&nbsp;</p>

<p>Write a solution to find the highest grade with its corresponding course for each student. In case of a tie, you should find the course with the smallest <code>course_id</code>.</p>

<p>Return the result table ordered by <code>student_id</code> in <strong>ascending order</strong>.</p>

<p>The&nbsp;result format is in the following example.</p>

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
-- use RANK() and pull results where rank = 1

select student_id,  course_id, grade
from
    (select student_id, course_id, grade, dense_rank() over(partition by student_id order by grade desc, course_id asc) as rnk
    from Enrollments) temp1
where rnk = 1
order by 1

--------------------------------------------------------------------------------------------------------------------------------------------------------------
-- nested 
-- first get id and highest grade, then get min course_id

select student_id, min(course_id) as course_id, grade
from Enrollments
where (student_id, grade) in
    (select student_id, max(grade) as grade
    from Enrollments
    group by student_id)
group by student_id
order by student_id

-- amazon- 2
-- coursera- 1
```

<!-- tabs:end -->

<!-- solution:end -->

