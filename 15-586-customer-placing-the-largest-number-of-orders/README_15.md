# [586. Customer Placing The Largest Number Of Orders](https://leetcode.com/problems/customer-placing-the-largest-number-of-orders/description)

## Description

<!-- description:start -->

<p>Table: <code>Orders</code></p>
<pre>
+-----------------+----------+
| Column Name     | Type     |
+-----------------+----------+
| order_number    | int      |
| customer_number | int      |
+-----------------+----------+
order_number is the primary key (column with unique values) for this table.
This table contains information about the order ID and the customer ID.
</pre>

Write a solution to find the customer_number for the customer who has placed the largest number of orders.

The test cases are generated so that exactly one customer will have placed more orders than any other customer.

The result format is in the following example.

<pre>
Orders table:
+--------------+-----------------+
| order_number | customer_number |
+--------------+-----------------+
| 1            | 1               |
| 2            | 2               |
| 3            | 3               |
| 4            | 3               |
+--------------+-----------------+

Result table:
+-----------------+
| customer_number |
+-----------------+
| 3               |
+-----------------+
Explanation: 
The customer with number 3 has two orders, which is greater than either customer 1 or 2 because each of them only has one order. 
So the result is customer_number 3.
</pre>

<!-- description:end -->

## Solutions

<!-- solution:start -->

<!-- tabs:start -->

#### MySQL

```sql
# Write your MySQL query statement below
-- the the cusotmer with maximum order count, order by, limit

select customer_number
from Orders
group by 1
order by count(order_number) desc
limit 1


-- adobe- 2
-- google- 3
-- apple- 2
-- uber- 2
-- twitter- 1
```

<!-- tabs:end -->

<!-- solution:end -->


