# [1350. Students With Invalid Departments](https://leetcode.com/problems/students-with-invalid-departments/description)

## Description

<!-- description:start -->

<p>Table: <code>Departments</code></p>
<pre>
+---------------+---------+
| Column Name   | Type    |
+---------------+---------+
| id            | int     |
| name          | varchar |
+---------------+---------+
In SQL, id is the primary key of this table.
The table has information about the id of each department of a university.
</pre>
 
<p>Table: <code>Students</code></p>
<pre>
+---------------+---------+
| Column Name   | Type    |
+---------------+---------+
| id            | int     |
| name          | varchar |
| department_id | int     |
+---------------+---------+
In SQL, id is the primary key of this table.
The table has information about the id of each student at a university and the id of the department he/she studies at.
</pre>
 
Find the id and the name of all students who are enrolled in departments that no longer exist.

Return the result table in any order.

The result format is in the following example.

<pre>
Departments table:
+------+--------------------------+
| id   | name                     |
+------+--------------------------+
| 1    | Electrical Engineering   |
| 7    | Computer Engineering     |
| 13   | Bussiness Administration |
+------+--------------------------+
Students table:
+------+----------+---------------+
| id   | name     | department_id |
+------+----------+---------------+
| 23   | Alice    | 1             |
| 1    | Bob      | 7             |
| 5    | Jennifer | 13            |
| 2    | John     | 14            |
| 4    | Jasmine  | 77            |
| 3    | Steve    | 74            |
| 6    | Luis     | 1             |
| 8    | Jonathan | 7             |
| 7    | Daiana   | 33            |
| 11   | Madelynn | 1             |
+------+----------+---------------+

Result table:
+------+----------+
| id   | name     |
+------+----------+
| 2    | John     |
| 7    | Daiana   |
| 4    | Jasmine  |
| 3    | Steve    |
+------+----------+
Explanation: 
John, Daiana, Steve, and Jasmine are enrolled in departments 14, 33, 74, and 77 respectively. department 14, 33, 74, and 77 do not exist in the Departments table.
</pre>

<!-- description:end -->

## Solutions

<!-- solution:start -->

<!-- tabs:start -->

#### MySQL

```sql
# Write your MySQL query statement below
-- subquery- use WHERE

select id, name
from Students
where department_id not in 
    (select id
    from Departments)

------------------------------------------------------------------------------------------------------------------------------------------------------------------------

-- join- use WHERE id is null

select s.id, s.name
from Students s
left join Departments d
on d.id = s.department_id
where d.id is null


-- amazon- 1
```

<!-- tabs:end -->

<!-- solution:end -->

