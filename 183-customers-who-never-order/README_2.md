# [183. Customers Who Never Order](https://leetcode.com/problems/customers-who-never-order/description/)

## Description

<!-- description:start -->

Suppose that a website contains two tables, the Customers table and the Orders table. Write a SQL query to find all customers who never order anything.

<p>Table: <code>Customers</code></p>

<pre>
+----+-------+
| Id | Name  |
+----+-------+
| 1  | Joe   |
| 2  | Henry |
| 3  | Sam   |
| 4  | Max   |
+----+-------+
</pre>

Table: Orders.

+----+------------+
| Id | CustomerId |
+----+------------+
| 1  | 3          |
| 2  | 1          |
+----+------------+

Using the above tables as example, return the following:

+-----------+
| Customers |
+-----------+
| Henry     |
| Max       |
+-----------+

### Thinking:
* Method

```SQL
# Write your MySQL query statement below
select
    Name as Customers
from
    Customers
where
    Id
not in(
    select CustomerId from Orders
);
```
