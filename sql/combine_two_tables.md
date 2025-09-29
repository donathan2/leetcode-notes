# LeetCode 175: Combine Two Tables (Easy)
### Problem Description:

Write a solution to report the first name, last name, city, and state of each person in the Person table. If the address of a personId is not present in the Address table, report null instead.

Return the result table in any order.

The result format is in the following example.





### Approach:

This is a straightforward SQL problem that we can solve with a single JOIN. To combine the tables, we join each person to their address by their respective ID column. However, we 
need to use a left join instead of an inner join as the problem requests we should include people who don't have an address.


```sql
select firstName, lastName, ad.city, ad.state
from person
left join address ad on ad.personId = person.personId
``` 
