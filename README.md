# SQL-50---Leet-Code-Solutions
## Solutions for SQL 50 Study Plan on LeetCode
### *Q1. 1757. Recyclable and Low Fat Products*
```sql
SELECT product_id 
from products
where low_fats = "Y"
AND
recyclable = "Y";
```
### *Q2. 584. Find Customer Referee*
```sql
SELECT name
from Customer
where referee_id is NULL or referee_id != 2;
```
### Q3. *595. Big Countries*
```sql
SELECT name, population, area from World
where area >= 3000000 OR
population >= 25000000;
```
### *Q4. 1148. Article Views I*
```sql
SELECT DISTINCT(author_id) as id from Views
where author_id = viewer_id
order by id;
```
### Q5. 1683. Invalid Tweets*
``` sql
SELECT tweet_id from tweets
where char_length(content) > 15;
```
### *Q6. 1378. Replace Employee ID With The Unique Identifier*
```sql
SELECT eu.unique_id as unique_id, e.name as name
from Employees e
LEFT JOIN employeeUNI eu
on eu.id = e.id;
```
### *Q7. 1068. Product Sales Analysis I*
```sql
SELECT product.product_name, sales.year, sales.price 
from sales
LEFT JOIN product
ON sales.product_id = product.product_id;
```
### *Q8. 1581. Customer Who Visited but Did Not Make Any Transactions*
```sql
SELECT visits.customer_id, COUNT(customer_id) as Count_no_trans
from visits
LEFT JOIN transactions
ON visits.visit_id = transactions.visit_id
where transactions.transaction_id is NULL
GROUP BY visits.customer_id;
```
### *Q9: 197. Rising Temperature*
``` sql
SELECT w1.id
FROM weather w1
INNER JOIN weather w2
WHERE DATEDIFF (w1.recordDate , w2.recordDate) = 1
AND w1.temperature> w2.temperature;
```
### *Q10: 1661. Average Time of Process per Machine*
```sql
SELECT a1.machine_id, ROUND(AVG(a2.timestamp - a1.timestamp),3) as processing_time
FROM activity a1
INNER JOIN activity a2
ON a1.process_id = a2.process_id
AND a1.machine_id = a2.machine_id
AND a1.timestamp< a2.timestamp
GROUP BY a1.machine_id;
```
### *Q11: 577. Employee Bonus*
```sql
select employee.name, bonus.bonus
from employee
left join bonus
on employee.empId = bonus.empId
where bonus.bonus < 1000 or Bonus.bonus is NULL;
```
### *Q12: 1280. Students and Examinations*
```sql
select students.student_id, students.student_name, subjects.subject_name, count(examinations.subject_name) as attended_exams
from students
cross join subjects
left join examinations
on students.student_id = examinations.student_id
and subjects.subject_name = examinations.subject_name
group by students.student_id, students.student_name, subjects.subject_name
order by students.student_id, subjects.subject_name;
```
### *Q13: 570. Managers with at Least 5 Direct Reports*
```sql
select e1.name
from employee e1
inner join employee e2
on e1.id= e2.managerId
group by e2.managerId
having count(e2.managerId) >= 5;
```
### *Q14: 1934. Confirmation Rate*
```sql
select s.user_id, IFNULL(ROUND(SUM(action='confirmed')/count(*),2),0.00) as confirmation_rate
from signups s
left join confirmations c
on s.user_id = c.user_id
group by s.user_id;
```
### *Q15: 620. Not Boring Movies*
```sql
select * 
from Cinema
where MOD(id,2)=1 
and 
description != "boring"
order by rating desc;
```
### *Q16: 1251. Average Selling Price*
```sql
select p.product_id, IFNULL(ROUND(sum(p.price*u.units)/sum(u.units),2),0) as average_price
from prices p
left join unitsSold u
on p.product_id = u.product_id
and u.purchase_date>= p.start_date
and u.purchase_date <= p.end_date
GROUP BY p.product_id;
```
### *Q17: 1075. Project Employees I*
```sql
select p.project_id, ROUND(AVG(e.experience_years), 2) as average_years
from project p
left join employee e
on p.employee_id = e.employee_id
group by p.project_id;
```
### *Q18: 1633. Percentage of Users Attended a Contest*
```sql
select contest_id, ROUND((COUNT(distinct user_id)) *100 / (select count(user_id) from users),2) as percentage
from Register
GROUP BY contest_id
order by percentage DESC, contest_id;
```
### *Q19: 1211. Queries Quality and Percentage*
```sql
select query_name, ROUND(avg(rating/position),2) as Quality, ROUND(AVG(IF(rating <3, 1, 0))*100,2) as poor_query_percentage
from queries
group by query_name;
```
### Q20: 1193. Monthly Transactions I*
```sql
select
    date_format(trans_date, '%Y-%m') as month,
    country,
    count(id) as trans_count,
    sum(state= 'approved') as approved_count,
    sum(amount) as trans_total_amount,
    sum(if(state = 'approved', amount, 0)) as approved_total_amount
FROM transactions
GROUP BY month, country;
```
### *Q21: 1174. Immediate Food Delivery II*
```sql
SELECT ROUND(sum(if(order_date = customer_pref_delivery_date, 1, 0)) * 100/COUNT(DISTINCT customer_id),2) as immediate_percentage
from delivery
WHERE (customer_id, order_date) IN 
(SELECT customer_id, MIN(order_date) as first_order_date
from delivery
group by customer_id 
)
```
### *Q22: 550. Game Play Analysis IV*
```sql
select ROUND(COUNT(DISTINCT player_id) / (SELECT COUNT(DISTINCT player_id) from activity),2) as fraction
from activity
where (player_id, DATE_SUB(event_date, interval 1 day)) IN
(
    select player_id, MIN(event_date) as first_login
    from activity
    group by player_id
)
```
### *Q23: 2356. Number of Unique Subjects Taught by Each Teacher*
```sql
select teacher_id, count(DISTINCT subject_id) as cnt
from teacher
group by teacher_id;
```
### *Q24: 1141. User Activity for the Past 30 Days I*
```sql
select
    activity_date as day,
    COUNT(DISTINCT user_id) as active_users
from activity
where activity_date >= '2019-06-28' AND activity_date <= '2019-07-27'
group by activity_date
```
### *Q25: 1070. Product Sales Analysis III*
```sql
SELECT product_id, year as first_year, quantity, price
FROM Sales s
WHERE (product_id, year) IN(
    select product_id, MIN(year) as f_year
    from sales
    GROUP BY product_id
);
```
### *Q26: 596. Classes More Than 5 Students*
```sql
select class
from courses
GROUP BY class
HAVING count(student) >=5; 
```
### *Q27: 1729. Find Followers Count*
```sql
SELECT user_id, COUNT(DISTINCT follower_id) AS followers_count
FROM Followers
GROUP BY user_id
ORDER BY user_id ASC
```
### *Q28: 619. Biggest Single Number*
```sql
select MAX(num) as num
from MyNumbers
where num IN(
    select num
    from MyNumbers
    group by num
    having count(*) = 1
)
```
### *Q29: 1045. Customers Who Bought All Products*
```sql
select customer_id
from customer
group by customer_id
HAVING COUNT(DISTINCT product_key) = (
    select COUNT(product_key)
    from Product
)
```
### *Q30: 1731. The Number of Employees Which Report to Each Employee*
```sql
select e1.employee_id, 
    e1.name, 
    count(e2.employee_id) as reports_count, 
    ROUND(AVG(e2.age)) as average_age
from employees e1
inner join employees e2
on e1.employee_id = e2.reports_to
group by e1.employee_id, e1.name
order by employee_id
```
### *Q31: 1789. Primary Department for Each Employee*
```sql
select DISTINCT employee_id, department_id
from employee
where employee_id IN (
    select employee_id
    from employee
    group by employee_id
    having count(*) = 1
) or primary_flag = 'Y'
```
### *Q32: 610. Triangle Judgement*
```sql
select *,
    IF(x+y>z AND y+Z>x AND x+z>y, "Yes", "No") as triangle
from Triangle
```
### *Q33: 180. Consecutive Numbers*
```sql
select DISTINCT l1.num as ConsecutiveNums
from Logs l1, Logs l2, Logs l3
where l1.id=l2.id-1 AND l2.id=l3.id-1
AND l1.num= l2.num AND l2.num = l3.num
```
### *Q34: 1164. Product Price at a Given Date*
```sql
select product_id, new_price as price
from Products
where (product_id, change_date) IN (
    select product_id, max(change_date)
    from products
    where change_date <= '2019-08-16'
    group by product_id
)
UNION 

select product_id, 10 as price
from products
where product_id NOT IN
(
    select product_id
    from products
    where change_date <= '2019-08-16'
)
```
### *Q35: 1204. Last Person to Fit in the Bus*
```sql
select q1.person_name
from queue q1
inner join Queue q2
on q1.turn >= q2.turn
group by q1.turn
having sum(q2.weight) <= 1000
order by SUM(q2.weight) DESC
LIMIT 1;
```
### *Q36: 1907. Count Salary Categories*
```sql
SELECT 
    "Low Salary" as category,
    COUNT(income) As accounts_count
from Accounts
where  income <20000
UNION
SELECT 
    "Average Salary" as category,
    COUNT(income) As accounts_count
from Accounts
where  income >= 20000 AND income <=50000
UNION
SELECT 
    "High Salary" as category,
    COUNT(income) As accounts_count
from Accounts
where  income > 50000
order by accounts_count DESC
```










