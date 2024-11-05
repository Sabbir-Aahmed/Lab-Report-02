# Lab Report 02
**Course:** Database Management System Sessional (CSEC-322)<br />

**Prepared By:**<br />
Md Sabbir Ahmed<br />
ID: 2222081019<br />
Batch: 57A Day<br />
Semester: Fall-2024<br />

## Create and Use Database
```sql
CREATE DATABASE onlineShoping;
USE onlineShoping;
```

## Create Tables
```sql
CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    name VARCHAR(50),
    salary DECIMAL(10, 2),
    department_id INT
);

CREATE TABLE customers (
    customer_id INT PRIMARY KEY,
    name VARCHAR(50)
);

CREATE TABLE orders (
    order_id INT PRIMARY KEY,
    customer_id INT,
    order_amount DECIMAL(10, 2),
    FOREIGN KEY (customer_id) REFERENCES customers(customer_id)
);

CREATE TABLE products (
    product_id INT PRIMARY KEY,
    product_name VARCHAR(50),
    category_id INT
);
```

## Insert Sample Data
```sql
INSERT INTO employees (employee_id, name, salary, department_id) VALUES
(1, 'Sabbir', 55000, 1),
(2, 'Shazid', 48000, 1),
(3, 'Himel', 72000, 2),
(4, 'Shimul', 60000, 2),
(5, 'Sunmun', 53000, 3),
(6, 'Ahmed', 55000, 1),
(7, 'Mahmud', 55000, 1),
(8, 'Diba', 55000, 1),
(9, 'Hena', 55000, 1),
(10, 'Rasel', 55000, 1),
(11, 'Rifat', 55000, 1),
(12, 'Abbasy', 55000, 1),
(13, 'Lotif', 55000, 1),
(14, 'Tahsin', 55000, 1);

INSERT INTO customers (customer_id, name) VALUES
(1, 'Fariha'),
(2, 'Abdur'),
(3, 'Abrar'),
(4, 'Upoma');

INSERT INTO orders (order_id, customer_id, order_amount) VALUES
(1, 1, 150.00),
(2, 2, 200.00),
(3, 3, 250.00),
(4, 1, 300.00),
(5, 4, 500.00);


INSERT INTO products (product_id, product_name, category_id) VALUES
(1, 'Laptop', 1),
(2, 'Smartphone', 2),
(3, 'Tablet', 3),
(4, 'Monitor', 4),
(5, 'Keyboard', 4);
```

## Q1: Retrieve all employees with a salary greater than 50,000.
SELECT * FROM employees
WHERE salary>50000;
```
### Output of Q1
(https://github.com/user-attachments/assets/6dae2483-ee24-4267-95ec-fd36b5c07c32)

## Q2: Retrieve all customers whose names start with 'A'.
```sql
SELECT * FROM customers
WHERE name LIKE 'A%';
```
### Output of Q2
(https://github.com/user-attachments/assets/0b7f3b90-845f-425e-8d98-ae59d4b96427)

## Q3: Group employees by department and calculate the average salary.
```sql
SELECT department_id, AVG(salary) AS average_salary
FROM employees
GROUP BY department_id;
```
### Output of Q3
(https://github.com/user-attachments/assets/4518b128-a5c5-4ef9-8861-26ef5021b889)

## Q4: Retrieve departments with an average salary greater than 60,000.
```sql
SELECT department_id, AVG(salary) AS average_salary
FROM employees
GROUP BY department_id
HAVING AVG(salary) > 60000;
```
### Output of Q4
(https://github.com/user-attachments/assets/1b1d3598-a6dc-47ae-a3c8-9a10f8bddea3)

## Q5: Retrieve all orders placed by customers with IDs 1, 2, and 3.
```sql
SELECT * FROM orders
WHERE customer_id IN (1, 2, 3);
```
### Output of Q5
(https://github.com/user-attachments/assets/b3a9c3d6-26aa-4d70-97c6-2ff733a53797)

## Q6: Retrieve all products that are not in categories 1, 2, and 3
```sql
SELECT * FROM products
WHERE category_id NOT IN (1, 2, 3);
```
### Output of Q6
(https://github.com/user-attachments/assets/1d59f13b-357e-473e-95c7-c1842251629b)

## Q7: Retrieve all employees who work in a department with more than 10 employees.
```sql
SELECT * FROM employees
WHERE department_id IN (
    SELECT department_id
    FROM employees
    GROUP BY department_id
    HAVING COUNT(employee_id) > 10
);
```
### Output of Q7
(https://github.com/user-attachments/assets/83b1d178-3b9d-43ff-ab7e-7ef7cc918b55)
