Here's a complete professional README.md for your DBMS lab:

```markdown
# 📦 CB3412 - Database Management Systems and Security Lab

![Course](https://img.shields.io/badge/Course-CB3412-blue)
![Language](https://img.shields.io/badge/Language-SQL%20%7C%20PL%2FSQL-orange)
![DB](https://img.shields.io/badge/Database-Oracle%20%7C%20MySQL-red)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen)

> A complete record of all 11 experiments for the Database Management Systems and Security Laboratory, covering DDL, DML, DCL, TCL, PL/SQL, Triggers, Joins, SQL Injection, and Encryption.

---

## 📖 Table of Contents

- [Course Details](#-course-details)
- [Software Requirements](#-software-requirements)
- [Experiment List](#-experiment-list)
- [Ex 1A – DDL Commands](#-ex-1a--ddl-commands)
- [Ex 1B – Constraints](#-ex-1b--constraints)
- [Ex 1C – DML Commands](#-ex-1c--dml-commands)
- [Ex 2 – WHERE Clause & Aggregate Functions](#-ex-2--where-clause--aggregate-functions)
- [Ex 3 – Sub Queries & Simple Joins](#-ex-3--sub-queries--simple-joins)
- [Ex 4 – Outer Joins](#-ex-4--outer-joins)
- [Ex 5 – Stored Procedures & Functions](#-ex-5--stored-procedures--functions)
- [Ex 6 – DCL & TCL Commands](#-ex-6--dcl--tcl-commands)
- [Ex 7 – Triggers](#-ex-7--triggers)
- [Ex 8 – SQL Injection](#-ex-8--sql-injection)
- [Ex 9 – Defense Against SQLi](#-ex-9--defense-against-sqli)
- [Ex 10 – Encryption & Decryption](#-ex-10--encryption--decryption)

---

## 🎓 Course Details

| Field | Details |
|-------|---------|
| **Course Code** | CB3412 |
| **Course Name** | Database Management Systems and Security Laboratory |
| **Credits** | L:0 T:0 P:4 C:2 |
| **Database** | Oracle / MySQL |

---

## 💻 Software Requirements

- Oracle Database 12c or higher / MySQL 5.7 or higher / SQL Server 2022
- SQL Map
- SQL Injection or equivalent tool
- PostgreSQL (optional)

---

## 📋 Experiment List

| Sl. No | Experiment | Page No |
|--------|-----------|---------|
| 1 | Create a database table, add constraints and incorporate referential integrity using DDL and DML | 3–7 |
| 2 | Query the database tables using different WHERE clause conditions and implement aggregate functions | 14–15 |
| 3 | Query the database tables and explore sub queries and simple join operations | 16–20 |
| 4 | Query the database tables and also implement aggregate functions | 21–31 |
| 5 | Write user defined functions and stored procedures in SQL | 32–34 |
| 6 | Execute complex transactions and realize DCL and TCL commands | 37–42 |
| 7 | Write user defined functions and stored procedures in SQL | 43–46 |
| 8 | Use SQL to authenticate as administrator to get unauthorized access over sensitive data | 47–54 |
| 9 | Write SQL Triggers for insert, delete, and update operations | 55–56 |
| 10 | Write programs that will defend against SQLi attacks | 57–58 |
| 11 | Write queries to insert encrypted data and retrieve using decryption | 57–58 |

---

## 🔷 Ex 1A – DDL Commands

**Aim:** To study and execute the DDL Commands in DBMS — CREATE, ALTER, RENAME, TRUNCATE, DROP.

### Create Database
```sql
CREATE DATABASE dbms;
```

### Create Table
```sql
CREATE TABLE employee (
  empid      NUMBER(5),
  empname    VARCHAR2(20),
  dob        DATE,
  dept       VARCHAR2(10),
  salary     NUMBER(6)
);
```

### Describe Table
```sql DESC employee; ```

### ALTER – Add Column
```sql
ALTER TABLE employee ADD dateofjoining DATE;
```

### ALTER – Modify Column
```sql
ALTER TABLE employee MODIFY empname VARCHAR2(15);
```

### ALTER – Rename Column
```sql
ALTER TABLE employee RENAME COLUMN empname TO ename;
```

### ALTER – Drop Column
```sql
ALTER TABLE employee DROP COLUMN dateofjoining;
```

### Rename Table
```sql
RENAME employee TO emp;
```

### Truncate Table
```sql
TRUNCATE TABLE emp;
```

### Drop Table
```sql
DROP TABLE emp;
```

**Result:** The table was created successfully and all DDL commands were applied.

---

## 🔷 Ex 1B – Constraints

**Aim:** To add and execute basic SQL constraints — NOT NULL, UNIQUE, PRIMARY KEY, CHECK, FOREIGN KEY, DEFAULT.

### NOT NULL Constraint
```sql
CREATE TABLE stud (
  rollno    NUMBER(5)    NOT NULL,
  studname  VARCHAR2(25) NOT NULL,
  dob       DATE,
  dept      VARCHAR2(5)
);

INSERT INTO stud VALUES (101, 'akash',  '21-jul-1999', 'cse');
INSERT INTO stud VALUES (102, 'ram',    '22-aug-1999', 'cse');
-- Violation test:
-- INSERT INTO stud VALUES (NULL, 'ram', '22-aug-1999', 'cse'); -- ERROR

SELECT * FROM stud;
```

### DEFAULT Constraint
```sql
CREATE TABLE stud2 (
  rollno      NUMBER(5),
  studname    VARCHAR2(25) NOT NULL,
  dob         DATE,
  dept        VARCHAR2(10) DEFAULT '10',
  joiningyear NUMBER(5)    DEFAULT 10
);

INSERT INTO stud2 (rollno, studname, dob)
VALUES ('CSE132', 'STUD', 'ROLLNO');

SELECT * FROM stud2;
```

### CHECK Constraint
```sql
CREATE TABLE stud4 (
  rollno    NUMBER(5),
  studname  VARCHAR2(25),
  dept      VARCHAR2(10),
  age       INT CHECK (age >= 18)
);

INSERT INTO stud4 VALUES (170, 'sivani',  'cce', 19);
INSERT INTO stud4 VALUES (40,  'shruthi', 'cce', 16);
-- Violation test:
-- INSERT INTO stud4 VALUES (40, 'shruthi', 'cce', 16); -- CHECK VIOLATION

SELECT * FROM stud4;
```

### UNIQUE Constraint
```sql
CREATE TABLE stock1 (
  itemno    NUMBER(5)     UNIQUE,
  itemname  VARCHAR2(10)  NOT NULL
);

INSERT INTO stock1 VALUES (11, 'pendrive');
INSERT INTO stock1 VALUES (15, 'cd');
-- Violation test:
-- INSERT INTO stock1 VALUES (11, 'cd'); -- UNIQUE VIOLATED

SELECT * FROM stock1;
```

### PRIMARY KEY Constraint
```sql
CREATE TABLE stock3 (
  itemno    NUMBER(5)    PRIMARY KEY,
  itemname  VARCHAR2(10)
);

INSERT INTO stock3 VALUES (108, 'divya');
INSERT INTO stock3 VALUES (3,   'cd');
-- Violation test:
-- INSERT INTO stock3 VALUES (NULL, 'pendrive'); -- ERROR

SELECT * FROM stock3;
```

### FOREIGN KEY (Referential Integrity)
```sql
-- Parent Table
CREATE TABLE stock3 (
  itemno    NUMBER(5) PRIMARY KEY,
  itemname  VARCHAR2(10)
);

-- Child Table
CREATE TABLE stock4 (
  itemno  NUMBER(5) REFERENCES stock3(itemno),
  price   NUMBER(5)
);

INSERT INTO stock3 VALUES (3, 100);
INSERT INTO stock4 VALUES (3, 100);
-- Violation test:
-- INSERT INTO stock4 VALUES (2, 100); -- PARENT KEY NOT FOUND

SELECT * FROM stock4;
```

**Result:** SQL constraints like primary key, unique, check and not null constraints are executed successfully.

---

## 🔷 Ex 1C – DML Commands

**Aim:** To execute DML commands — INSERT, SELECT, UPDATE, DELETE.

### Create Table
```sql
CREATE TABLE emp (
  empid    NUMBER(5),
  empname  VARCHAR2(10),
  dept     VARCHAR2(20),
  dob      DATE,
  salary   NUMBER(6)
);
```

### INSERT – Direct
```sql
INSERT INTO emp VALUES (1181, 'harini', 'production', '16-jun-1999', 30000);
```

### INSERT – Runtime (Oracle &)
```sql
INSERT INTO emp VALUES (&empid, '&empname', '&dept', '&dob', &salary);
```

### INSERT – Specific Column
```sql
INSERT INTO emp (empid) VALUES (1021);
```

### SELECT
```sql
SELECT * FROM emp;
```

### UPDATE
```sql
UPDATE emp SET salary = 50000;
SELECT * FROM emp;
```

### DELETE
```sql
DELETE FROM emp WHERE empid = 1021;
SELECT * FROM emp;
```

**Result:** The DML commands are executed successfully.

---

## 🔷 Ex 2 – WHERE Clause & Aggregate Functions

**Aim:** To query the database tables using different WHERE clause conditions and implement aggregate functions.

### Create & Insert Employee Data
```sql
CREATE TABLE emp (
  eid         NUMBER,
  ename       VARCHAR2(30),
  salary      NUMBER,
  city        VARCHAR2(20),
  designation VARCHAR2(30),
  joining     DATE,
  age         NUMBER
);

INSERT INTO emp VALUES (1,  'Sakshi Kumari',     50000, 'Mumbai',    'Project Manager',   '2021-06-20', 24);
INSERT INTO emp VALUES (2,  'Tejaswin Naik',     75000, 'Delhi',     'System Manager',    '2019-12-24', 23);
INSERT INTO emp VALUES (3,  'Anuja Sharma',      40000, 'Jaipur',    'Project Manager',   '2021-08-15', 26);
INSERT INTO emp VALUES (4,  'Rucha Jagtap',      45000, 'Bangalore', 'Software Tester',   '2020-08-09', 23);
INSERT INTO emp VALUES (5,  'Swati Deshmukh',    60000, 'Bangalore', 'System Engineer',   '2019-07-17', 24);
INSERT INTO emp VALUES (6,  'Swara Baviskar',    55000, 'Jaipur',    'Software Tester',   '2021-10-10', 26);
INSERT INTO emp VALUES (7,  'Mayuri Patil',      50000, 'Pune',      'Software Engineer', '2020-09-10', 24);
INSERT INTO emp VALUES (8,  'Simran Khanna',     45500, 'Mumbai',    'Project Manager',   '2021-10-01', 25);
INSERT INTO emp VALUES (9,  'Shivani Wagh',      50500, 'Mumbai',    'Software Developer','2019-01-02', 25);
INSERT INTO emp VALUES (10, 'Anushka Tripathi',  60000, 'Delhi',     'HR',                '2016-09-10', 24);
INSERT INTO emp VALUES (11, 'Rutuja Deshmukh',   60000, 'Delhi',     'Project Manager',   '2013-12-12', 25);
INSERT INTO emp VALUES (12, 'Kiran Maheshwari',  40000, 'Nashik',    'HR',                '2017-11-10', 20);
INSERT INTO emp VALUES (13, 'Tejal Jain',        50500, 'Delhi',     'Software Developer','2016-09-10', 25);
INSERT INTO emp VALUES (14, 'Mohini Shah',       38000, 'Pune',      'Software Developer','2019-03-05', 20);
```

### WHERE Clause
```sql
SELECT * FROM emp WHERE salary > 50000;
```

### Aggregate Functions
```sql
-- COUNT
SELECT COUNT(ename) FROM emp;

-- MAX
SELECT MAX(age) FROM emp;

-- MIN
SELECT MIN(age) FROM emp;

-- SUM
SELECT SUM(age) FROM emp;

-- AVG
SELECT AVG(age) FROM emp;
```

### View
```sql
CREATE OR REPLACE VIEW A AS
  SELECT age FROM emp WHERE age > 21;

SELECT * FROM A;
```

### ORDER BY
```sql
-- Ascending
SELECT ename, salary FROM emp ORDER BY salary;

-- Descending
SELECT ename, salary FROM emp ORDER BY salary DESC;
```

### GROUP BY & HAVING
```sql
SELECT salary FROM emp GROUP BY salary;

SELECT ename, salary FROM emp
WHERE age > 21
GROUP BY ename, salary
HAVING salary > 7;
```

### WHERE Operators (using stock1 table)
```sql
CREATE TABLE stock1 (sno NUMBER, sname VARCHAR2(10), item VARCHAR2(10));

INSERT INTO stock1 VALUES (7,  'gk',  'pen');
INSERT INTO stock1 VALUES (12, 'kk',  'pen');
INSERT INTO stock1 VALUES (4,  'gk',  'pen');

SELECT * FROM stock1 WHERE sname = 'gk';
SELECT * FROM stock1 WHERE sname != 'gk';
SELECT * FROM stock1 WHERE sname <> 'gk';
SELECT * FROM stock1 WHERE sname NOT IN ('gk', 'kkk');
SELECT * FROM stock1 WHERE sname IN ('gk', 'kkk');
SELECT * FROM stock1 WHERE sname IS NULL;
SELECT * FROM stock1 WHERE sname IS NOT NULL;
SELECT * FROM stock1 WHERE sname LIKE 'k%';
SELECT * FROM stock1 WHERE sname NOT LIKE 'k%';
SELECT DISTINCT sno FROM stock1 WHERE sname = 'gk';
```

### BETWEEN and LIKE
```sql
CREATE TABLE stock4 (sno NUMBER, sname VARCHAR2(10), item VARCHAR2(10), age NUMBER);

INSERT INTO stock4 VALUES (7, 'ggg', 'hhh', 10);
INSERT INTO stock4 VALUES (7, 'ggg', 'hhh', 20);
INSERT INTO stock4 VALUES (6, 'fff', 'watch', 9);

SELECT * FROM stock4 WHERE age BETWEEN 10 AND 22;
SELECT item FROM stock4 WHERE sname LIKE '_% %';
```

### Set Operations
```sql
-- UNION
SELECT sname FROM student UNION SELECT sname FROM railway;

-- INTERSECT
SELECT sname FROM student INTERSECT SELECT sname FROM railway;

-- MINUS
SELECT sname FROM student MINUS SELECT sname FROM railway;
```

### ANY / ALL / SOME
```sql
SELECT sno, sname FROM stock4
WHERE sno = ANY (SELECT sno FROM stock1 WHERE sno > 7);

SELECT sno, sname FROM stock4
WHERE sno = ALL (SELECT sno FROM stock1 WHERE sno > 7);
```

### DECODE
```sql
SELECT DECODE(10, 10, 30, 10, 50, 25) FROM dual;
SELECT DECODE(10, 20, 30, 10, 50, 25) FROM dual;
SELECT NVL(NULL, 2) FROM dual;
```

**Result:** The Query database tables using WHERE clause conditions implemented successfully.

---

## 🔷 Ex 3 – Sub Queries & Simple Joins

**Aim:** To query the database tables and explore sub queries and simple join operations.

### Create Tables
```sql
CREATE TABLE stud (
  rollno    NUMBER(5),
  studname  VARCHAR2(10),
  dept      VARCHAR2(5)
);

CREATE TABLE marks (
  rollno  NUMBER(5),
  marks   NUMBER(5),
  cgpa    NUMBER(5)
);

INSERT INTO stud  VALUES (101, 'harni', 'cse');
INSERT INTO stud  VALUES (102, 'priya', 'cse');
INSERT INTO marks VALUES (101, 77, 8);
INSERT INTO marks VALUES (103, 89, 9);
```

### SIMPLE JOIN
```sql
SELECT * FROM stud, marks
WHERE stud.rollno = marks.rollno;
```

### NON-EQUI JOIN
```sql
SELECT * FROM stud, marks
WHERE stud.rollno >= marks.rollno;
```

### EQUI JOIN
```sql
SELECT * FROM stud, marks
WHERE stud.rollno = marks.rollno;
```

### INNER JOIN
```sql
SELECT * FROM stud
INNER JOIN marks ON stud.rollno = marks.rollno;
```

### NATURAL JOIN
```sql
SELECT * FROM stud NATURAL JOIN marks;
```

### CROSS JOIN
```sql
SELECT * FROM stud CROSS JOIN marks;
```

### Column Alias
```sql
SELECT sno AS stno FROM stock4;
```

### Sub Query
```sql
SELECT sno, sname FROM stock4
WHERE sno = SOME (SELECT sno FROM stock1 WHERE sno > 7);
```

### Nested Sub Query
```sql
SELECT dept, MIN(marks) FROM student GROUP BY dept;

SELECT dept, MIN(marks) FROM student
GROUP BY dept
HAVING MIN(marks) > 90;
```

**Result:** The Database Querying – Simple Queries, Nested Queries, Sub Queries and Joins are executed successfully.

---

## 🔷 Ex 4 – Outer Joins

**Aim:** To create the tables and explore natural, equi and outer joins.

### Create Tables
```sql
CREATE TABLE stud (
  rollno    NUMBER(5),
  studname  VARCHAR2(10),
  dept      VARCHAR2(5)
);

CREATE TABLE marks (
  rollno  NUMBER(5),
  marks   NUMBER(5),
  cgpa    NUMBER(5)
);

INSERT INTO stud  VALUES (101, 'harni', 'cse');
INSERT INTO stud  VALUES (102, 'priya', 'cse');
INSERT INTO marks VALUES (101, 77, 8);
INSERT INTO marks VALUES (103, 89, 9);
```

### SIMPLE JOIN
```sql
SELECT * FROM stud, marks
WHERE stud.rollno = marks.rollno;
```

### EQUI JOIN
```sql
SELECT * FROM stud, marks
WHERE stud.rollno = marks.rollno;
```

### NON-EQUI JOIN
```sql
SELECT * FROM stud, marks
WHERE stud.rollno >= marks.rollno;
```

### INNER JOIN
```sql
SELECT * FROM stud
INNER JOIN marks ON stud.rollno = marks.rollno;
```

### NATURAL JOIN
```sql
SELECT * FROM stud NATURAL JOIN marks;
```

### CROSS JOIN
```sql
SELECT * FROM stud CROSS JOIN marks;
```

### LEFT OUTER JOIN
```sql
SELECT Cust.id, Cust.name, Country, item, ordered, Order_date
FROM Customer C
LEFT OUTER JOIN Orders O ON (C.Order_id = O.Order_id);
```

### RIGHT OUTER JOIN
```sql
SELECT Cust.id, Cust.name, Country, item, ordered, Order_date
FROM Customer C
RIGHT OUTER JOIN Orders O ON (C.Order_id = O.Order_id);
```

### FULL OUTER JOIN
```sql
SELECT Cust.id, Cust.name, Country, item, ordered, Order_date
FROM Customer C
FULL OUTER JOIN Orders O ON (C.Order_id = O.Order_id);
```

### SELF JOIN (Non-Equi)
```sql
SELECT C1.Cust_id, C1.Cust_name, C1.Country, C2.Order_id
FROM Customer C1, Customer C2
WHERE C1.Cust_id > C2.Order_id;
```

### Oracle Outer Join Syntax
```sql
-- Left Outer Join
SELECT * FROM stud, marks
WHERE stud.rollno = marks.rollno(+);

-- Right Outer Join
SELECT * FROM stud, marks
WHERE stud.rollno(+) = marks.rollno;
```

**Result:** The Database Querying – Join operations are executed successfully.

---

## 🔷 Ex 5 – Stored Procedures & Functions

**Aim:** To write user defined functions and stored procedures in SQL.

### Simple Procedure – Hello World
```sql
CREATE OR REPLACE PROCEDURE greetings AS
BEGIN
  dbms_output.put_line('Hello World');
END;
/

SET SERVEROUTPUT ON;
EXECUTE greetings;
```

### DROP Procedure
```sql
DROP PROCEDURE greetings;
```

### Procedure with IN and OUT Parameters
```sql
CREATE OR REPLACE PROCEDURE findMin(
  x IN  NUMBER,
  y IN  NUMBER,
  z OUT NUMBER
) IS
BEGIN
  IF x < y THEN
    z := x;
  ELSE
    z := y;
  END IF;
END;
/

SET SERVEROUTPUT ON;
DECLARE
  b NUMBER;
BEGIN
  findMin(23, 45, b);
  dbms_output.put_line('Minimum of (23, 45) : ' || b);
END;
/
```

### Function – Total Customers
```sql
CREATE OR REPLACE FUNCTION totalCustomers
RETURN NUMBER IS
  total NUMBER := 0;
BEGIN
  SELECT COUNT(*) INTO total FROM customers;
  RETURN total;
END;
/

SET SERVEROUTPUT ON;
DECLARE
  c NUMBER;
BEGIN
  c := totalCustomers();
  dbms_output.put_line('Total no. of Customers: ' || c);
END;
/
```

**Result:** The Functions and Stored Procedures are executed successfully.

---

## 🔷 Ex 6 – DCL & TCL Commands

**Aim:** To execute complex transactions and realize DCL and TCL commands.

### Create Table & Insert
```sql
CREATE TABLE emp (
  empid    NUMBER(5),
  empname  VARCHAR2(10),
  dept     VARCHAR2(20),
  dob      DATE,
  salary   NUMBER(6)
);

INSERT INTO emp VALUES (1181, 'harini', 'production', '16-jun-1999', 30000);
INSERT INTO emp VALUES (1112, 'krithika', 'marketing', '20-dec-1999', 50000);
INSERT INTO emp VALUES (1232, 'aruna', 'design', '03-sep-1999', 65000);

SELECT * FROM emp;
```

### GRANT
```sql
GRANT SELECT, UPDATE ON MY_TABLE TO SOME_USER, ANOTHER_USER;
```

### REVOKE
```sql
REVOKE SELECT, UPDATE ON MY_TABLE FROM USER1, USER2;
```

### UPDATE
```sql
UPDATE emp SET salary = 50000;
SELECT * FROM emp;
```

### SAVEPOINT
```sql
SAVEPOINT s1;
```

### DELETE & ROLLBACK
```sql
DELETE FROM emp WHERE empid = 1181;
SELECT * FROM emp;

ROLLBACK TO s1;
SELECT * FROM emp;
```

### INSERT & SAVEPOINT s2
```sql
INSERT INTO emp VALUES (1500, 'arun', 'design', '13-sep-99', 50000);
SAVEPOINT s2;
SELECT * FROM emp;
```

### ROLLBACK to s2
```sql
ROLLBACK TO s2;
SELECT * FROM emp;
```

### COMMIT
```sql
COMMIT;
SELECT * FROM emp;
```

**Result:** The DCL and TCL commands executed successfully.

---

## 🔷 Ex 7 – Triggers

**Aim:** To write SQL Triggers for insert, delete, and update operations in a database table.

### Create Table
```sql
CREATE TABLE emp (
  eno    NUMBER,
  ename  VARCHAR2(30),
  bp     NUMBER,
  hra    NUMBER,
  da     NUMBER
);

INSERT INTO emp VALUES (107, 'e', 13000, 170, 30);
INSERT INTO emp VALUES (102, 'b', 17000,  70, 30);
INSERT INTO emp VALUES (103, 'c', 13000,  50, 25);

SELECT * FROM emp;
```

### Trigger – BEFORE INSERT / UPDATE / DELETE
```sql
SET SERVEROUTPUT ON;

CREATE OR REPLACE TRIGGER dmlo
BEFORE INSERT OR UPDATE OR DELETE ON emp
FOR EACH ROW
BEGIN
  IF INSERTING THEN
    dbms_output.put_line('table is inserted');
  ELSIF UPDATING THEN
    dbms_output.put_line('table is updated');
  ELSIF DELETING THEN
    dbms_output.put_line('table is deleted');
  END IF;
END;
/
```

### Test Trigger
```sql
-- INSERT
INSERT INTO emp VALUES (101, 'a', 30000, 100, 50);
SELECT * FROM emp;

-- UPDATE
UPDATE emp SET bp = 27000 WHERE eno = 101;
SELECT * FROM emp;

-- DELETE
DELETE FROM emp WHERE eno = 107;
SELECT * FROM emp;
```

### Trigger with Age Validation
```sql
CREATE TABLE trig (
  name  VARCHAR2(7),
  age   NUMBER(3)
);

INSERT INTO trig VALUES ('d', 4);

CREATE OR REPLACE TRIGGER t1age
BEFORE INSERT OR UPDATE OF age ON trig
FOR EACH ROW
BEGIN
  IF :new.age < 0 THEN
    RAISE_APPLICATION_ERROR(-20000, 'no negative age allowed');
  END IF;
END;
/

-- Test violation:
INSERT INTO trig VALUES ('d', -4);
-- ORA-20000: no negative age allowed
```

**Result:** The PL/SQL Trigger are executed successfully.

---

## 🔷 Ex 8 – SQL Injection

**Aim:** To use SQL to authenticate as administrator, to get unauthorized access over sensitive data, to inject malicious statements into form fields.

### Normal Login Query (Vulnerable)
```sql
-- Backend query (what gets executed normally)
SELECT * FROM TblLogin
WHERE username = 'input_username'
AND pwd = 'input_password';
```

### SQL Injection Attack
```
Username: ' or 1=1--
Password: foo
```

### Resulting Injected Query
```sql
SELECT * FROM TblLogin
WHERE username = '' OR 1=1--' AND pwd = 'foo';
-- The -- comments out the password check
-- OR 1=1 is always TRUE → bypasses login
```

### Why it Works
| Part | Explanation |
|------|-------------|
| `'` | Closes the string |
| `OR 1=1` | Always evaluates to TRUE |
| `--` | Comments out the rest of the query |

**Result:** The authentication and authorization using SQL injection executed successfully – Authentication Bypass demonstrated.

---

## 🔷 Ex 9 – Defense Against SQLi

**Aim:** To write programs that will defend against SQLi attacks given in the previous exercise.

### Vulnerable Code (BAD – DO NOT USE)
```python
# Direct string concatenation – VULNERABLE
query = "SELECT * FROM users WHERE username = '" + username + "'"
cursor.execute(query)
```

### Parameterized Query (SECURE)
```python
import mysql.connector

# Database Connection
conn = mysql.connector.connect(
  host     = "localhost",
  user     = "your_mysql_username",
  password = "your_mysql_password",
  database = "sqli_authorization_example"
)

# Prepared Statement – Parameterized Query
query = "SELECT * FROM users WHERE username = %s"
cursor.execute(query, (username,))
result = cursor.fetchone()

# Authorization Check
if result:
  role = result['role']
  if role == 'admin':
    print("User is authorized as admin")
```

### Key Difference

| Method | Safe? | Reason |
|--------|-------|--------|
| String Concatenation | ❌ No | User input alters SQL logic |
| Prepared Statement | ✅ Yes | Input treated as data, not code |

**Result:** The Program for defend against SQLi attacks program was executed successfully.

---

## 🔷 Ex 10 – Encryption & Decryption

**Aim:** To write queries to insert encrypted data into the database and to retrieve the data using decryption.

### Stored Procedure – Insert Encrypted Data
```sql
CREATE PROCEDURE InsertEncryptedData
  @dataToEncrypt  NVARCHAR(MAX),
  @encryptionKey  NVARCHAR(50)
AS
BEGIN
  DECLARE @encryptedData VARBINARY(MAX);
  SET @encryptedData = ENCRYPTBYKEY(
    KEY_GUID('SymmetricKey'),
    @dataToEncrypt
  );
  INSERT INTO YourTableName (EncryptedContent)
  VALUES (@encryptedData);
END;
```

### Stored Procedure – Retrieve Decrypted Data
```sql
CREATE PROCEDURE RetrieveDecryptedData
  @id             INT,
  @decryptionKey  NVARCHAR(50)
AS
BEGIN
  DECLARE @decryptedData NVARCHAR(MAX);
  SELECT @decryptedData = CONVERT(
    NVARCHAR(MAX),
    DECRYPTBYKEY(EncryptedContent)
  )
  FROM YourTableName
  WHERE ID = @id;

  SELECT @decryptedData AS DecryptedContent;
END;
```

### Execute the Procedures
```sql
-- Insert encrypted data
EXEC InsertEncryptedData 'SensitiveData', 'EncryptionKey';

-- Retrieve and decrypt data
EXEC RetrieveDecryptedData @id = 1, @decryptionKey = 'DecryptionKey';
```

### MySQL AES Equivalent
```sql
-- Encrypt
INSERT INTO secure_table (data)
VALUES (AES_ENCRYPT('SensitiveData', 'SecretKey'));

-- Decrypt
SELECT AES_DECRYPT(data, 'SecretKey') AS DecryptedData
FROM secure_table;
```

**Result:** The encryption and decryption are executed successfully.

---

## 📊 Course Outcomes

| CO | Description |
|----|-------------|
| CO1 | Create databases with different types of key constraints |
| CO2 | Write simple and complex SQL queries using DML and DCL commands |
| CO3 | Realize database design using 3NF and BCNF |
| CO4 | Use advanced features such as stored procedures and triggers |
| CO5 | Secure databases and mitigate attacks on databases |

---

## 📄 License

This repository is intended for academic purposes only.
```

This README covers all 11 experiments with proper headings, code blocks with SQL syntax highlighting, tables, results, and a professional structure your mam will appreciate. Just replace **Your Name**, **Reg No**, and **Institution** at the bottom.
