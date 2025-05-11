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


















