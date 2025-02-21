# [1965. Employees With Missing Information](https://leetcode.com/problems/employees-with-missing-information/description)

## Description

<!-- description:start -->

<p>Table: <code>Employees</code></p>
 <pre>
+-------------+---------+
| Column Name | Type    |
+-------------+---------+
| employee_id | int     |
| name        | varchar |
+-------------+---------+
employee_id is the column with unique values for this table.
Each row of this table indicates the name of the employee whose ID is employee_id.
</pre>
 
<p>Table: <code>Salaries</code></p>
<pre>
+-------------+---------+
| Column Name | Type    |
+-------------+---------+
| employee_id | int     |
| salary      | int     |
+-------------+---------+
employee_id is the column with unique values for this table.
Each row of this table indicates the salary of the employee whose ID is employee_id.
</pre>
 

Write a solution to report the IDs of all the employees with missing information. The information of an employee is missing if:

* The employee's name is missing, or
* The employee's salary is missing.
Return the result table ordered by employee_id in ascending order.

The result format is in the following example.

<pre>
Employees table:
+-------------+----------+
| employee_id | name     |
+-------------+----------+
| 2           | Crew     |
| 4           | Haven    |
| 5           | Kristian |
+-------------+----------+
  
Salaries table:
+-------------+--------+
| employee_id | salary |
+-------------+--------+
| 5           | 76071  |
| 1           | 22517  |
| 4           | 63539  |
+-------------+--------+
  
Result table:
+-------------+
| employee_id |
+-------------+
| 1           |
| 2           |
+-------------+
Explanation: 
Employees 1, 2, 4, and 5 are working at this company.
The name of employee 1 is missing.
The salary of employee 2 is missing.
</pre>

<!-- description:end -->

## Solutions

<!-- solution:start -->

<!-- tabs:start -->

#### MySQL

```sql
# Write your MySQL query statement below
-- select all employees from Employees not in Salaries, UNION select all employees from Salaries not in Employees

select employee_id
from Employees
where employee_id not in 
    (select employee_id
    from Salaries)
union 
select employee_id
from Salaries
where employee_id not in 
    (select employee_id
    from Employees)
order by 1

----------------------------------------------------------------------------------------------------------------------------------------------------------------
-- first get a table of all employees bu doing a UNION on the 2 tables
-- then select those emeployees which are in above table but not in respective tables- UNION

with all_employees as 
    (select employee_id 
    from Employees
    union
    select employee_id 
    from Salaries)

select employee_id
from all_employees 
where employee_id not in (select employee_id from Employees)
union
select employee_id
from all_employees 

-- adobe- 2
    
-- alternate    
where employee_id not in (select employee_id from Salaries)
order by 1
```

<!-- tabs:end -->

<!-- solution:end -->


