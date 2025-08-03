# Leetcode-SQL_50

Solved using PostgreSQL


-- 1757. Recyclable and Low Fat Products
SELECT product_id
FROM Products
WHERE low_fats = 'Y' AND recyclable = 'Y';

-- Find Customer Referee
SELECT name
FROM Customer
WHERE referee_id != 2 OR referee_id IS NULL;

-- Big Countries
SELECT name, population, area
FROM World
WHERE area >= 3000000 OR population >= 25000000;

-- Article Views I
SELECT author_id AS id
FROM Views
WHERE author_id = viewer_id
ORDER BY author_id ASC;

-- 1683. Invalid Tweets
SELECT tweet_id
FROM Tweets
WHERE LENGTH(content) > 15;

-- 1378. Replace Employee ID With The Unique Identifier
SELECT eu.unique_id, e.name
FROM Employees e
LEFT JOIN EmployeeUNI eu ON e.id = eu.id;

-- 1068. Product Sales Analysis I
SELECT p.Product_name, s.year, s.price
FROM Sales s
INNER JOIN Product p ON s.product_id = p.product_id;

-- 1581. Customer Who Visited but Did Not Make Any Transactions
SELECT customer_id, COUNT(visit_id) AS count_no_trans
FROM Visits
WHERE visit_id NOT IN (SELECT visit_id FROM Transactions)
GROUP BY customer_id;

-- 577. Employee Bonus
SELECT e.name, b.bonus
FROM Employee e 
LEFT JOIN Bonus b ON e.empId = b.empId
WHERE b.bonus < 1000 OR b.bonus IS NULL;

-- 1280. Students and Examinations
SELECT stu.student_id, stu.student_name, sub.subject_name, COUNT(e.subject_name) AS attended_exams
FROM Students stu
CROSS JOIN Subjects sub 
LEFT JOIN Examinations e 
    ON e.student_id = stu.student_id AND sub.subject_name = e.subject_name 
GROUP BY stu.student_id, stu.student_name, sub.subject_name
ORDER BY stu.student_id, sub.subject_name;

 9
-- 570. Managers with at Least 5 Direct Reports
SELECT m.name
FROM Employee e
JOIN Employee m ON e.managerId = m.Id
GROUP BY m.id, m.name
HAVING COUNT(m.id) >= 5;

-- 620. Not Boring Movies

SELECT *
FROM Cinema
WHERE (id%2 = 1) AND description NOT LIKE '%boring%'
ORDER BY rating DESC;

-- 1251. Average Selling Price
SELECT p.product_id, ROUND(SUM(u.units*p.price)/SUM(u.units)::numeric, 2) AS average_price
FROM Prices p
LEFT JOIN UnitsSold u ON p.product_id = u.product_id AND u.purchase_date BETWEEN p.start_date AND p.end_date
GROUP BY p.product_id;

-- 1075. Project Employees I
SELECT p.project_id, ROUND((SUM(e.experience_years)/COUNT(e.employee_id)::numeric), 2) AS average_years
FROM Employee e
JOIN Project p ON e.employee_id = p.employee_id
GROUP BY p.project_id; 

-- 1633. Percentage of Users Attended a Contest
SELECT r.contest_id, ROUND((COUNT(r.user_id)*100)/(SELECT COUNT(user_id) FROM Users)::numeric, 2) AS percentage  
FROM Register r
RIGHT JOIN Users u ON r.user_id = u.user_id
GROUP BY r.contest_id
ORDER BY percentage DESC, r.contest_id ASC;
