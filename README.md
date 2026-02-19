# DBMS

Practical no:-1 
To design an ER model for an Employee Payroll System that captures employee details, payroll processing, and related relationships. 

a. Identifying and Listing All Required Entities 
The key entities in the system are: 
1. Employee 
2. Department 
3. Job/Designation 
4. Payroll 
5. SalaryComponent 
6. BankAccount

b. Defining Attributes for Each Entity
Entity                Attributes
employee           EmployeeID (PK), Name, DOB, Gender, ContactNo, Email, Address, DOJ, DepartmentID (FK), JobID (FK), AccountID (FK)
Department         DepartmentID (PK), DepartmentName, Location
Job/Designation    JobID (PK), JobTitle, BasicSalary
Payroll            PayrollID (PK), EmployeeID (FK), PayPeriod, GrossSalary, Deductions, NetSalary, PaymentDate
SalaryComponent    ComponentID (PK), PayrollID (FK), Type (Allowance/Deduction), Name, Amount 
BankAccount        AccountID (PK), BankName, Branch, IFSCCode, AccountNumber

c. Establishing Relationships Using ER Notations 
● Employee–Department: Many-to-One (Many employees work in one department) 
● Employee–Job: Many-to-One (Each employee has one job title) 
● Employee–Payroll: One-to-Many (An employee has multiple payroll records)
● Payroll–SalaryComponent: One-to-Many (A payroll includes multiple components)
● Employee–BankAccount: One-to-One (One employee has one bank account) 

d. Drawing the ER Diagram

                  DOB                                                                      departmentID
  contact                   Gender                                                                          department name           
 email          employee         email <------------------works in----------------------> department          yoration
departmentId                account ID                                                            
                  job                                                                       receives


            jobID                                                                          Receives     
                                                                                                       Payperiod
Job Title        Job <--------------------------------------Has--------------------------> payroll     Gross salary                      
                                                                                             
            amount                                                                          deduction


               accountID                                                                  includes
                                                                     
Bankname                      Branch
              Bank account <------------------------------- Has ----------------------> Salary Component      componentId
IFSC Code                     accountNo                                                                       type
               account                                                                     name


e. Verifying the Model for Normalization and Data Consistency 
Normalization Check: 
● All attributes are atomic → 1NF 
● Each non-key attribute is fully dependent on the primary key → 2NF
● No transitive dependencies between non-key attributes → 3NF 

Data Consistency: 
● Foreign keys are correctly assigned (e.g., Employee → Department, Job, BankAccount) 
● Entities are logically separated to avoid redundancy 

Model is normalized and ensures data consistency.


# practical no:-2
Aim: Perform the following using Oracle 10g:
1. View all databases (schemas)
2. Create a database (schema/user)

-- View all schemas
SELECT username FROM all_users;

-- Create new schema (user)
1]using GUI
Click on Administration
Click on Database Users
Click on Create
Enter schema/user(database) name : my-db
Password: mypassword
Click on Create Button

2]Using Command Line Interface
CREATE USER mydb_user IDENTIFIED BY mypassword;


#    Practical No. 3
a. Creating Tables (With and Without Constraints) 
Without Constraints
CREATE TABLE studentsdb( 
studentid NUMBER(10),
studentname VARCHAR2(50)
);
DESC studentsdb;

With Constraints
CREATE TABLE studentsdb2(
studentid NUMBER(10) PRIMARY KEY, 
studentname VARCHAR2(50) NOT NULL, 
age NUMBER(3),
email VARCHAR2(100) UNIQUE
);
DESC studentsdb2;

b. Inserting/Updating/Deleting Records in a Table 
Insert Records
CREATE TABLE studentsdb2(
studentid NUMBER(10) PRIMARY KEY, 
studentname VARCHAR2(50) NOT NULL,
age NUMBER(3),
email VARCHAR2(100) UNIQUE
);

INSERT INTO studentsdb2(studentid, studentname, age, email) 
VALUES (1, 'abc', 25, 'abc@example.com');
INSERT INTO studentsdb2(studentid, studentname, age, email) 
VALUES (2, 'xyz', 25, 'xyz@example.com');

SELECT * FROM studentsdb2;

Update Records

CREATE TABLE studentsdb2(
studentid NUMBER(10) PRIMARY KEY, 
studentname VARCHAR2(50) NOT NULL, 
age NUMBER(3),
email VARCHAR2(100) UNIQUE
);

INSERT INTO studentsdb2(studentid, studentname, age, email) 
VALUES (1, 'abc', 25, 'abc@example.com');

INSERT INTO studentsdb2(studentid, studentname, age, email) 
VALUES (2, 'xyz', 25, 'xyz@example.com');

UPDATE studentsdb2 
SET age = 22
WHERE studentid = 1;

SELECT * FROM studentsdb2;

Delete Records
CREATE TABLE studentsdb2(
studentid NUMBER(10) PRIMARY KEY,
studentname VARCHAR2(50) NOT NULL,
age NUMBER(3),
email VARCHAR2(100) UNIQUE
);
INSERT INTO studentsdb2(studentid, studentname, age, email) 
VALUES (1, 'abc', 25, 'abc@example.com');

INSERT INTO studentsdb2(studentid, studentname, age, email) 
VALUES (2, 'xyz', 25, 'xyz@example.com');

UPDATE studentsdb2 
SET age = 22
WHERE studentid = 1;
DELETE FROM studentsdb2 
WHERE studentid = 1;

SELECT * FROM studentsdb2; 


#    Practical No 4

a. Altering a Table

CREATE TABLE students(
studentid NUMBER(10), 
studentname VARCHAR2(50), 
age NUMBER(3),
email VARCHAR2(100) 
);

INSERT INTO students(studentid, studentname, age, email) 
VALUES (1, 'abc', 25, 'abc@example.com');
INSERT INTO students(studentid, studentname, age, email) 
VALUES (2, 'xyz', 18, 'xyz@example.com');
INSERT INTO students(studentid, studentname, age, email) 
VALUES (3, 'xyz', 17, 'xyz@example.com');

SELECT * FROM students;

ALTER TABLE students
ADD gender VARCHAR2(10);

desc students;

ALTER TABLE students
MODIFY studentname VARCHAR2(100);

desc students;

ALTER TABLE students

DROP COLUMN email;

desc students;

b. Dropping/Truncating/Renaming Tables

RENAME students TO studentinfo;

TRUNCATE TABLE studentinfo;

SELECT * FROM studentinfo;

DROP TABLE studentinfo;

#    Practical No 5

CREATE TABLE EMPLOYEES (
employee_id NUMBER,
first_name VARCHAR2(50),
last_name VARCHAR2(50),
email VARCHAR2(50),
hire_date  DATE,
salary NUMBER,
commission_pct NUMBER,
department_id NUMBER
);
Sample Data:
INSERT INTO EMPLOYEES VALUES (1, 'Amit','Vora','amit@gmail.com','01-JAN-2002','100000',0,70);
INSERT INTO EMPLOYEES VALUES (1, 'Priya','Jadhav','priya@gmail.com','01-MARCH-2000','500000',10,80);
INSERT INTO EMPLOYEES VALUES (1, 'Riya','Sharma','riya@gmail.com','18-FEB-2000','50000',10,90);
INSERT INTO EMPLOYEES VALUES (1, 'Kunal','King','kunal@gmail.com','18-FEB-1990','500000',10,90);

a. Simple Queries with WHERE Operators.
This practical focuses on using comparison operators (=, != or <>, >, <, >=, <=) in the WHERE clause.
Scenario: Retrieve information about employees based on specific criteria.
Examples:
          1. Retrieve all employees with a salary greater than 5000.
              SELECT employee_id, first_name, last_name, salary
              FROM employees
              WHERE salary > 50000;
              
.          2. Find employees whose last name is 'King'.
              SELECT employee_id, first_name, last_name, email
              FROM employees
              WHERE last_name = 'King';

.          3. Get employees hired before January 1, 2000.  
                SELECT *FROM employees
                WHERE hire_date < TO_DATE('01-JAN-2000', 'DD-MON-YYYY');

.          4. List employees who are NOT in department 90.
                   SELECT * FROM employees
                   WHERE department_id <> 90;

b. WHERE with Keywords and Logical Operators
This practical involves using keywords like AND, OR, NOT, BETWEEN, LIKE, IN, and IS NULL in the WHERE clause.
Scenario: Refine employee searches using more complex conditions.
Examples:
          1. Employees with a salary between 5000 and 500000 (inclusive).
             SELECT *FROM employees
             WHERE salary BETWEEN 50000 AND 500000;
         
.         2. Employees whose first name starts with 'J'.
             SELECT employee_id, first_name, last_name
             FROM employees
             WHERE first_name LIKE 'J%';

.         3.Employees whose last name contains 'ri'.
             SELECT employee_id, first_name, last_name
             FROM employees
             WHERE first_name LIKE '%ri%';

.          4. Employees who work in department 60 or 90.  
               SELECT *FROM employees
               WHERE department_id IN (60, 90);

.          5. Employees with a salary greater than 10000 AND in department 90.
              SELECT *FROM employees
              WHERE salary > 50000 AND department_id = 90

.          6. Employees who have a commission percentage (i.e., commission_pct is NOT NULL).
                SELECT employee_id, first_name, last_name, commission_pct
                FROM employees
                WHERE commission_pct IS NOT NULL;

c.  Simple Queries with Aggregate Functions
This practical demonstrates the use of aggregate functions (COUNT, SUM, AVG, MIN, MAX) to summarize data.
Scenario: Get overall statistics about employees.
Examples:
          1. Count the total number of employees.
            -- SELECT COUNT(*) AS total_employees FROM employees;

.         2.  Calculate the sum of all employee salaries.
              SELECT SUM(salary) AS total_salary_expense
              FROM employees;

.         3.Find the average salary of all employees.
              SELECT AVG(salary) AS average_salary
              FROM employees;

.         4. Determine the minimum salary in the company.
               SELECT MIN(salary) AS minimum_salary
              FROM employees;

.         5. Determine the maximum salary in the company.
                SELECT MAX(salary) AS maximum_salary
                FROM employees;

d. Queries with Aggregate Functions (GROUP BY and HAVING Clause)
This practical combines aggregate functions with GROUP BY to perform calculations on subsets of data, and HAVING to filter those grouped results.

1. Count the number of employees in each department.

SQL
SELECT department_id, COUNT(employee_id) AS num_employees
FROM employees
GROUP BY department_id
ORDER BY department_id;

2.  Find the total salary expense for departments where the total expense is greater than 50000.

SELECT department_id, SUM(salary) AS total_department_salary
FROM employees
GROUP BY department_id
HAVING SUM(salary) > 50000
ORDER BY total_department_salary DESC;

3. Count the number of employees for each department
   SELECT department_id, COUNT(employee_id) AS num_employees
   FROM employees
   GROUP BY department_id

# Practical no:- 6
1. Date Functions in Oracle 10g

Function                    Purpose                              Example Query
SYSDATE              Current date and time                  sql SELECT SYSDATE FROM dual;
ADD_MONTHS           Add/subtract month                     sql SELECT ADD_MONTHS(SYSDATE, 2) AS after_2_months FROM dual;
NEXT_DAY             Next occurrence of given weekday       sql SELECT NEXT_DAY(SYSDATE, 'FRIDAY') AS next_friday FROM dual;
LAST_DAY             Last day of month                      sql SELECT LAST_DAY(SYSDATE) AS last_of_month FROM dual;

Input:- SELECT SYSDATE AS current_date_time FROM dual;

Input:-  SELECT ADD_MONTHS(SYSDATE, 2) AS after_2_months FROM dual;

Input:- SELECT NEXT_DAY(SYSDATE, 'FRIDAY') AS next_friday FROM dual;

Input:- SELECT LAST_DAY(SYSDATE) AS last_of_month FROM dual;

2. String Functions in Oracle 10g
Function                Purpose                                Example Query
UPPER              Convert to uppercase              sql SELECT UPPER('oracle database') AS upper_case FROM dual;
LOWER              Convert to lowercase              sql SELECT LOWER('Oracle Database') AS lower_case FROM dual;
INITCAP            First letter uppercase            sql SELECT INITCAP('oracle database') AS init_cap FROM dual;
SUBSTR             Extract part of string            sql SELECT SUBSTR('INFORMATION', 2, 5) AS sub_str FROM dual;
LENGTH             Length of string                  sql SELECT LENGTH('Oracle') AS str_length FROM dual;

Input:-SELECT UPPER('oracle database') AS upper_case FROM dual;

Input:-SELECT LOWER('Oracle Database') AS lower_case FROM dual;

Input:- SELECT INITCAP('oracle database') AS init_cap FROM dual;

Input:- SELECT SUBSTR('INFORMATION', 2, 5) AS sub_str FROM dual;

Input:- SELECT LENGTH('Oracle') AS str_length FROM dual;

Input:-SELECT CONCAT('Hello ', 'World') AS concat_result FROM dual;

3. Math Functions in Oracle 10g
Function                    Purpose                    Example Query
ROUND                Round to nearest value        sql SELECT ROUND(123.456, 2) AS rounded FROM dual;
TRUNC                Remove decimal places         sql SELECT TRUNC(123.456, 1) AS truncated FROM dual;
MOD                  Find remainder                sql SELECT MOD(10, 3) AS remainder FROM dual;
POWER                Raise to a power              sql SELECT POWER(2, 5) AS power_result FROM dual;
SQRT                 Square root                   sql SELECT SQRT(81) AS sqrt_result FROM dual;
ABS                  Absolute value                sql SELECT ABS(-15) AS abs_result FROM dual;

Input:- SELECT ROUND(123.456, 2) AS rounded FROM dual;

Input:- SELECT TRUNC(123.456, 1) AS truncated FROM dual;

Input:- SELECT MOD(10, 3) AS remainder FROM dual;

Input:- SELECT POWER(2, 5) AS power_result FROM dual;

Input:- SELECT SQRT(81) AS sqrt_result FROM dual;

Input:- SELECT ABS(-15) AS abs_result FROM dual;

#   Practical no:-7
1. Create Sample Tables
   CREATE TABLE departments (
    dept_id     NUMBER(5) PRIMARY KEY,
    dept_name   VARCHAR2(50)
);

-- Insert sample data into departments
INSERT INTO departments VALUES (101, 'HR');
INSERT INTO departments VALUES (102, 'IT');
INSERT INTO departments VALUES (103, 'Finance');

-- Insert sample data into employees
INSERT INTO employees VALUES (1, 'Alice', 101, 50000);
INSERT INTO employees VALUES (2, 'Bob', 102, 60000);
INSERT INTO employees VALUES (3, 'Charlie', 103, 55000);
INSERT INTO employees VALUES (4, 'David', NULL, 45000);

2. INNER JOIN Example
   SELECT e.emp_id, e.emp_name, d.dept_name, e.salary
   FROM employees e
   INNER JOIN departments d
   ON e.dept_id = d.dept_id;

3. LEFT OUTER JOIN Example (All employees even if no department)
   SELECT e.emp_id, e.emp_name, d.dept_name, e.salary
   FROM employees e
   LEFT OUTER JOIN departments d
   ON e.dept_id = d.dept_id;

4. RIGHT OUTER JOIN Example (All departments even if no employees)
   sql
   CopyEdit
   SELECT e.emp_id, e.emp_name, d.dept_name
   FROM employees e
   RIGHT OUTER JOIN departments d
   ON e.dept_id = d.dept_id;

5. FULL OUTER JOIN Example (All employees and all departments)
   sql
   CopyEdit
   SELECT e.emp_id, e.emp_name, d.dept_name
   FROM employees e
   FULL OUTER JOIN departments d
   ON e.dept_id = d.dept_id;

# - Practical No. 8: Views in Oracle 10g
1. Create sample table
   CREATE TABLE employees (
    emp_id      NUMBER(5) PRIMARY KEY,
    emp_name    VARCHAR2(50),
    dept_id     NUMBER(5),
    salary      NUMBER(10,2)
);

2. Insert sample data
  INSERT INTO employees VALUES (1, 'Alice', 101, 50000);
  INSERT INTO employees VALUES (2, 'Bob', 102, 60000);
  INSERT INTO employees VALUES (3, 'Charlie', 101, 55000);
  INSERT INTO employees VALUES (4, 'David', 103, 45000);

COMMIT;

3. Create a view for Department 101 employees
    CREATE VIEW dept101_employees AS
    SELECT emp_id, emp_name, salary
    FROM employees
    WHERE dept_id = 101;

4. Select from the created view
    SELECT * FROM dept101_employees;

5. Drop the view
    DROP VIEW dept101_employees;

Example 2 – View for High Salary Employees
            1. Create a view for employees earning more than 55,000
                CREATE VIEW high_salary_employees AS
                SELECT emp_id, emp_name, dept_id, salary
                FROM employees
                WHERE salary > 55000;

,           2. Select from the created view
                SELECT * FROM high_salary_employees;

.           3. Drop the view
                DROP VIEW high_salary_employees;

# Practical no:-9 

Step 1: Create a user
    CREATE USER student IDENTIFIED BY stud123;
    
Step 2: Grant Permissions
    GRANT CREATE SESSION TO student;
    GRANT CREATE TABLE TO student;
    
Step 3: Create Table
      CREATE TABLE emp(
      employeeid NUMBER(10),
      employeename VARCHAR2(50)
);

Step 4: Grant Permissions
        GRANT SELECT, INSERT, UPDATE ON emp TO student;
        
Step 5: Revoke Permissions
          REVOKE INSERT, UPDATE ON emp FROM student;
          REVOKE CREATE TABLE FROM student;
          
Step 6: Verification
        SELECT * FROM emp;
        INSERT INTO emp(employeeid, employeename) VALUES(1234, &#39;Test&#39;);
        SELECT * FROM emp;

# practical no:- 10

Aim: To implement an Employee Payroll System using SQL concepts – DDL, DML, and DCL
statements.

Entities Identified (Employee Payroll System):
          1. Department – Stores department details.
          2. Employee – Stores employee personal and job details.
          3. Payroll – Stores salary and payroll details.

Step 1: Define & Create Database and Tables with Constraints (DDL)

-- Create Department Table
CREATE TABLE Department (
    DeptID INT PRIMARY KEY,
    DeptName VARCHAR(50) NOT NULL,
    Location VARCHAR(50)
);

-- Create Employee Table
CREATE TABLE Employee (
    EmpID INT PRIMARY KEY,
    EmpName VARCHAR(50) NOT NULL,
    JobTitle VARCHAR(50),
    DeptID INT,
    HireDate DATE,
    CONSTRAINT fk_dept FOREIGN KEY (DeptID) REFERENCES Department(DeptID)
);

-- Create Payroll Table
CREATE TABLE Payroll (
    PayrollID INT PRIMARY KEY,
    EmpID INT,
    BasicSalary NUMBER(10,2) CHECK (BasicSalary > 0),
    Allowance NUMBER(10,2) DEFAULT 0,
    Deductions NUMBER(10,2) DEFAULT 0,
    NetSalary NUMBER(10,2),
    CONSTRAINT fk_emp FOREIGN KEY (EmpID) REFERENCES Employee(EmpID)
);

Step 2: Insert Records (DML)

-- Insert Departments
INSERT INTO Department VALUES (1, 'HR', 'Mumbai');
INSERT INTO Department VALUES (2, 'IT', 'Pune');
INSERT INTO Department VALUES (3, 'Finance', 'Delhi');

-- Insert Employees
INSERT INTO Employee VALUES (101, 'Rajesh Kumar', 'Manager', 1, '2020-01-15');
INSERT INTO Employee VALUES (102, 'Priya Sharma', 'Analyst', 2, '2021-03-12');
INSERT INTO Employee VALUES (103, 'Amit Verma', 'Developer', 2, '2019-07-25');
INSERT INTO Employee VALUES (104, 'Sneha Patil', 'Accountant', 3, '2018-11-30');
INSERT INTO Employee VALUES (105, 'Kiran Joshi', 'HR Executive', 1, '2022-06-10');

-- Insert Payroll Records
INSERT INTO Payroll VALUES (1001, 101, 50000, 10000, 5000, 55000);
INSERT INTO Payroll VALUES (1002, 102, 40000, 8000, 3000, 45000);
INSERT INTO Payroll VALUES (1003, 103, 35000, 5000, 2000, 38000);
INSERT INTO Payroll VALUES (1004, 104, 30000, 4000, 1000, 33000);
INSERT INTO Payroll VALUES (1005, 105, 25000, 3000, 2000, 26000);

Step 3: Simple Queries using Operators & Functions
-- List all employees working in IT department
SELECT EmpName, JobTitle FROM Employee WHERE DeptID = 2;

-- Find employees with salary greater than 40000
SELECT e.EmpName, p.NetSalary 
FROM Employee e JOIN Payroll p ON e.EmpID = p.EmpID
WHERE p.NetSalary > 40000;

-- Display employee name in uppercase
SELECT UPPER(EmpName) FROM Employee;

-- Find total salary expenditure
SELECT SUM(NetSalary) AS Total_Salary FROM Payroll;

-- Find average salary of IT department
SELECT AVG(p.NetSalary) 
FROM Payroll p JOIN Employee e ON p.EmpID = e.EmpID
WHERE e.DeptID = 2;

Step 4: Create Views and Perform Drop & Select

-- Create a view to show employee salary details
CREATE VIEW EmpSalaryView AS
SELECT e.EmpID, e.EmpName, d.DeptName, p.NetSalary
FROM Employee e 
JOIN Department d ON e.DeptID = d.DeptID
JOIN Payroll p ON e.EmpID = p.EmpID;

-- Select from the view
SELECT * FROM EmpSalaryView;

-- Drop the view
DROP VIEW EmpSalaryView;


Step 5: Perform DCL Commands (GRANT & REVOKE)

-- Create a new user
CREATE USER payroll_user IDENTIFIED BY pay123;

-- Grant permission to select and insert on Payroll
GRANT SELECT, INSERT ON Payroll TO payroll_user;

-- Revoke insert permission
REVOKE INSERT ON Payroll FROM payroll_user;


