# [1412. Find the Quiet Students in All Exams](https://leetcode.com/problems/find-the-quiet-students-in-all-exams/description/)

## Description

<!-- description:start -->

<p>Table: <code>Student</code></p>
<pre>
+---------------------+---------+
| Column Name         | Type    |
+---------------------+---------+
| student_id          | int     |
| student_name        | varchar |
+---------------------+---------+
student_id is the primary key for this table.
student_name is the name of the student.
</pre>

<p>Table: <code>Exam</code></p>
<pre>
+---------------+---------+
| Column Name   | Type    |
+---------------+---------+
| exam_id       | int     |
| student_id    | int     |
| score         | int     |
+---------------+---------+
(exam_id, student_id) is the primary key for this table.
Student with student_id got score points in exam with id exam_id.
</pre>
 
A "quite" student is the one who took at least one exam and didn't score neither the high score nor the low score.

Write an  SQL query to report the students (student_id, student_name) being "quiet" in ALL exams.

Don't return the student who has never taken any exam. Return the result table ordered by student_id.

The query result format is in the following example.

<pre>
Student table:
+-------------+---------------+
| student_id  | student_name  |
+-------------+---------------+
| 1           | Daniel        |
| 2           | Jade          |
| 3           | Stella        |
| 4           | Jonathan      |
| 5           | Will          |
+-------------+---------------+

Exam table:
+------------+--------------+-----------+
| exam_id    | student_id   | score     |
+------------+--------------+-----------+
| 10         |     1        |    70     |
| 10         |     2        |    80     |
| 10         |     3        |    90     |
| 20         |     1        |    80     |
| 30         |     1        |    70     |
| 30         |     3        |    80     |
| 30         |     4        |    90     |
| 40         |     1        |    60     |
| 40         |     2        |    70     |
| 40         |     4        |    80     |
+------------+--------------+-----------+

Result table:
+-------------+---------------+
| student_id  | student_name  |
+-------------+---------------+
| 2           | Jade          |
+-------------+---------------+

For exam 1: Student 1 and 3 hold the lowest and high score respectively.
For exam 2: Student 1 hold both highest and lowest score.
For exam 3 and 4: Studnet 1 and 4 hold the lowest and high score respectively.
Student 2 and 5 have never got the highest or lowest in any of the exam.
Since student 5 is not taking any exam, he is excluded from the result.
So, we only return the information of Student 2.
</pre>

<!-- description:end -->

## Solutions

<!-- solution:start -->

<!-- tabs:start -->

#### MySQL

```sql
# Write your MySQL query statement below
-- CTE- find highest rank and lowest rank in 2 separate columns using dense_rank()
-- pull student_id from Exam table- note that student_id is not primary key, so use distnct
-- pull name from Student table
-- use Exam as left table because we don't want students who didn't take any exams
-- use WHERE condition not in-> CTE
  
with CTE as 
    (select exam_id, student_id, score, 
        dense_rank() over(partition by exam_id order by score desc) rank_highest,
        dense_rank() over(partition by exam_id order by score asc) rank_lowest
    from Exam)

select distinct e.student_id, s.student_name
from Exam e
left join Student s
on e.student_id = s.student_id
where e.student_id not in
    (select student_id 
    from CTE
    where rank_highest = 1 or rank_lowest = 1)
order by 1


-- no companies listed
```

<!-- tabs:end -->

<!-- solution:end -->

