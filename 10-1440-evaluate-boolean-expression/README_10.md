# [1440. Evaluate Boolean Expression](https://leetcode.com/problems/evaluate-boolean-expression/description)

## Description

<!-- description:start -->

<p>Table: <code>Variables</code></p>
 <pre>
+---------------+---------+
| Column Name   | Type    |
+---------------+---------+
| name          | varchar |
| value         | int     |
+---------------+---------+
name is the primary key for this table.
This table contains the stored variables and their values.
</pre>
 
<p>Table: <code>Expressions</code></p>
<pre>
+---------------+---------+
| Column Name   | Type    |
+---------------+---------+
| left_operand  | varchar |
| operator      | enum    |
| right_operand | varchar |
+---------------+---------+
(left_operand, operator, right_operand) is the primary key for this table.
This table contains a boolean expression that should be evaluated.
operator is an enum that takes one of the values ('<', '>', '=')
The values of left_operand and right_operand are guaranteed to be in the Variables table.
</pre>
 

Write an  SQL query to evaluate the boolean expressions in Expressions table.

Return the result table in any order.

The query result format is in the following example.

<pre>
Variables table:
+------+-------+
| name | value |
+------+-------+
| x    | 66    |
| y    | 77    |
+------+-------+

Expressions table:
+--------------+----------+---------------+
| left_operand | operator | right_operand |
+--------------+----------+---------------+
| x            | >        | y             |
| x            | <        | y             |
| x            | =        | y             |
| y            | >        | x             |
| y            | <        | x             |
| x            | =        | x             |
+--------------+----------+---------------+

Result table:
+--------------+----------+---------------+-------+
| left_operand | operator | right_operand | value |
+--------------+----------+---------------+-------+
| x            | >        | y             | false |
| x            | <        | y             | true  |
| x            | =        | y             | false |
| y            | >        | x             | true  |
| y            | <        | x             | false |
| x            | =        | x             | true  |
+--------------+----------+---------------+-------+
As shown, you need find the value of each boolean exprssion in the table using the variables table.
</pre>

<!-- description:end -->

## Solutions

<!-- solution:start -->

<!-- tabs:start -->

#### MySQL

```sql
# Write your MySQL query statement below
-- create 2 value tables- l for left operand, r for right operand
-- use join to join it to the main table
-- write case statements using l.value and r.value

select e.left_operand, e.operator, e.right_operand,
    (case when operator = '>' and l.value > r.value then 'true'
    when operator = '<' and l.value < r.value then 'true'
    when operator = '=' and l.value = r.value then 'true'
    else 'false' end) as value
from Expressions e
join Variables l
on l.name = e.left_operand
join Variables r
on r.name = right_operand

-- point72-1 
```

<!-- tabs:end -->

<!-- solution:end -->


