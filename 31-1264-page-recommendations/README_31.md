# [1264. Page Recommendations](https://leetcode.com/problems/page-recommendations/description)

## Description

<!-- description:start -->

<p>Table: <code>Friendship</code></p>
 <pre>
+---------------+---------+
| Column Name   | Type    |
+---------------+---------+
| user1_id      | int     |
| user2_id      | int     |
+---------------+---------+
(user1_id, user2_id) is the primary key for this table.
Each row of this table indicates that there is a friendship relation between user1_id and user2_id.
</pre>
 
<p>Table: <code>Likes</code></p>
<pre>
+-------------+---------+
| Column Name | Type    |
+-------------+---------+
| user_id     | int     |
| page_id     | int     |
+-------------+---------+
(user_id, page_id) is the primary key for this table.
Each row of this table indicates that user_id likes page_id.
</pre>

Write an  SQL query to recommend pages to the user with user_id = 1 using the pages that your friends liked. It should not recommend pages you already liked.

Return result table in any order without duplicates.

The query result format is in the following example:

<pre>
Friendship table:
+----------+----------+
| user1_id | user2_id |
+----------+----------+
| 1        | 2        |
| 1        | 3        |
| 1        | 4        |
| 2        | 3        |
| 2        | 4        |
| 2        | 5        |
| 6        | 1        |
+----------+----------+

Likes table:
+---------+---------+
| user_id | page_id |
+---------+---------+
| 1       | 88      |
| 2       | 23      |
| 3       | 24      |
| 4       | 56      |
| 5       | 11      |
| 6       | 33      |
| 2       | 77      |
| 3       | 77      |
| 6       | 88      |
+---------+---------+

Result table:
+------------------+
| recommended_page |
+------------------+
| 23               |
| 24               |
| 56               |
| 33               |
| 77               |
+------------------+
User one is friend with users 2, 3, 4 and 6.
Suggested pages are 23 from user 2, 24 from user 3, 56 from user 3 and 33 from user 6.
Page 77 is suggested from both user 2 and user 3.
Page 88 is not suggested because user 1 already likes it.
</pre>

<!-- description:end -->

## Solutions

<!-- solution:start -->

<!-- tabs:start -->

#### MySQL

```sql
# Write your MySQL query statement below
-- got user1=id = 1 friends in t0 and t1
-- joined t1 with Likes on 1's friends
-- where condition- page shouldn't be liked by 1

with t0 as 
    (select user1_id, user2_id
    from Friendship
    union
    select user2_id, user1_id
    from Friendship),
t1 as
    (select user1_id, user2_id
    from t0
    where user1_id = 1)
  
select distinct l.page_id as recommended_page
from t1 join Likes l
on t1.user2_id = l.user_id
where page_id not in
    (select page_id
    from Likes
    where user_id = 1)
  
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------
-- same as above but 1 less CTE and added where condition
  
with t1 as 
    (select user1_id, user2_id
    from Friendship
    union
    select user2_id, user1_id
    from Friendship)

select distinct l.page_id as recommended_page
from t1 join Likes l
on t1.user2_id = l.user_id
where t1.user1_id = 1
and page_id not in
    (select page_id
    from Likes
    where user_id = 1)


-- facebook- 1
```

<!-- tabs:end -->

<!-- solution:end -->


