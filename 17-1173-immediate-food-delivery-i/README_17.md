# [1173. Immediate Food Delivery I](https://leetcode.com/problems/immediate-food-delivery-i/description)

## Description

<!-- description:start -->

<p>Table: <code>Delivery</code></p>
 <pre>
+-----------------------------+---------+
| Column Name                 | Type    |
+-----------------------------+---------+
| delivery_id                 | int     |
| customer_id                 | int     |
| order_date                  | date    |
| customer_pref_delivery_date | date    |
+-----------------------------+---------+
delivery_id is the primary key of this table.
The table holds information about food delivery to customers that make orders at some date and specify a preferred delivery date (on the same order date or after it).
</pre>
 

If the preferred delivery date of the customer is the same as the order date then the order is called immediate otherwise it's called scheduled.

Write an  SQL query to find the percentage of immediate orders in the table, rounded to 2 decimal places.


The query result format is in the following example:

<pre>
Delivery table:
+-------------+-------------+------------+-----------------------------+
| delivery_id | customer_id | order_date | customer_pref_delivery_date |
+-------------+-------------+------------+-----------------------------+
| 1           | 1           | 2019-08-01 | 2019-08-02                  |
| 2           | 5           | 2019-08-02 | 2019-08-02                  |
| 3           | 1           | 2019-08-11 | 2019-08-11                  |
| 4           | 3           | 2019-08-24 | 2019-08-26                  |
| 5           | 4           | 2019-08-21 | 2019-08-22                  |
| 6           | 2           | 2019-08-11 | 2019-08-13                  |
+-------------+-------------+------------+-----------------------------+

Result table:
+----------------------+
| immediate_percentage |
+----------------------+
| 33.33                |
+----------------------+
The orders with delivery id 2 and 3 are immediate while the others are scheduled.
</pre>

<!-- description:end -->

## Solutions

<!-- solution:start -->

<!-- tabs:start -->

#### MySQL

```sql
# Write your MySQL query statement below
-- simple condition in aggregate function- count immediate, divide by total rows in the table
select round(sum(order_date = customer_pref_delivery_date) / count(*) * 100, 2) as immediate_percentage
from Delivery

-- doordash- 2
```

<!-- tabs:end -->

<!-- solution:end -->
