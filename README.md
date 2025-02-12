# SQL_Project
CREATE DATABASE ORG123; SHOW DATABASES; USE ORG123;

CREATE TABLE Worker ( WORKER_ID INT NOT NULL PRIMARY KEY AUTO_INCREMENT, FIRST_NAME CHAR(25), LAST_NAME CHAR(25), SALARY INT(15), JOINING_DATE DATETIME, DEPARTMENT CHAR(25) );

INSERT INTO Worker (WORKER_ID, FIRST_NAME, LAST_NAME, SALARY, JOINING_DATE, DEPARTMENT) VALUES (001, 'Monika', 'Arora', 100000, '14-02-20 09.00.00', 'HR'), (002, 'Niharika', 'Verma', 80000, '14-06-11 09.00.00', 'Admin'), (003, 'Vishal', 'Singhal', 300000, '14-02-20 09.00.00', 'HR'), (004, 'Amitabh', 'Singh', 500000, '14-02-20 09.00.00', 'Admin'), (005, 'Vivek', 'Bhati', 500000, '14-06-11 09.00.00', 'Admin'), (006, 'Vipul', 'Diwan', 200000, '14-06-11 09.00.00', 'Account'), (007, 'Satish', 'Kumar', 75000, '14-01-20 09.00.00', 'Account'), (008, 'Geetika', 'Chauhan', 90000, '14-04-11 09.00.00', 'Admin'); SELECT * FROM Worker WHERE SALARY > 100000 AND DEPARTMENT = 'HR'; Select * from Worker where Salary > 200000; select * from worker where salary between 100000 and 200000; select * from worker where worker_id in (2,4,6,8); SELECT * FROM Worker WHERE salary BETWEEN 200000 AND 400000 AND WORKER_ID IN (1, 2, 3, 4, 5); SELECT *
FROM Worker
WHERE DEPARTMENT = 'HR'
ORDER BY SALARY ASC ; SELECT MIN(SALARY) FROM Worker WHERE DEPARTMENT = 'HR'; SELECT FIRST_NAME, LAST_NAME
FROM Worker
WHERE DEPARTMENT = 'HR'
AND SALARY = (SELECT MIN(SALARY) FROM Worker WHERE DEPARTMENT = 'HR'); SELECT DEPARTMENT, FIRST_NAME, LAST_NAME, SALARY FROM Worker w WHERE SALARY = ( SELECT MAX(SALARY) FROM Worker WHERE DEPARTMENT = w.DEPARTMENT ); SELECT FIRST_NAME, LAST_NAME, SALARY, DEPARTMENT
FROM Worker
WHERE (DEPARTMENT = 'Admin' OR DEPARTMENT = 'Account')
AND SALARY = ( SELECT MIN(SALARY) FROM Worker WHERE DEPARTMENT IN ('Admin', 'Account') AND SALARY = (SELECT MIN(SALARY) FROM Worker WHERE DEPARTMENT IN ('Admin', 'Account')) ); select * from worker; select distinct(department) from worker; #alias - help u to give some temp name for a coloumn select worker_id as emp_code from worker; SELECT worker_id FROM worker UNION #Union print once and union all print twice SELECT first_name FROM worker; SELECT DEPARTMENT, SALARY FROM Worker WHERE DEPARTMENT = 'HR' AND SALARY > 100000 UNION SELECT DEPARTMENT, SALARY FROM Worker WHERE DEPARTMENT = 'Admin' AND SALARY > 100000 ORDER BY SALARY; SELECT DEPARTMENT,WORKER_ID FROM Worker WHERE DEPARTMENT = 'HR' UNION SELECT DEPARTMENT, WORKER_ID FROM Worker WHERE DEPARTMENT = 'Account' ORDER BY WORKER_ID; SELECT worker_id, first_name,department, CASE WHEN salary > 300000 THEN 'Rich people' WHEN salary <=300000 && salary >=100000 THEN 'Middle stage' ELSE 'Poor people' END AS People_stage_wise FROM worker; SELECT DEPARTMENT, COUNT(WORKER_ID) AS Total_Employees FROM Worker GROUP BY DEPARTMENT ORDER BY DEPARTMENT; SELECT DISTINCT DEPARTMENT, (SELECT COUNT(*) FROM Worker AS W2 WHERE W2.DEPARTMENT = W1.DEPARTMENT) AS Total_Employees FROM Worker AS W1 ORDER BY DEPARTMENT; SELECT 'HR' AS DEPARTMENT, COUNT(WORKER_ID) AS Total_Employees FROM Worker WHERE DEPARTMENT = 'HR' UNION SELECT 'Admin' AS DEPARTMENT, COUNT(WORKER_ID) AS Total_Employees FROM Worker WHERE DEPARTMENT = 'Admin' UNION SELECT 'Account' AS DEPARTMENT, COUNT(WORKER_ID) AS Total_Employees FROM Worker WHERE DEPARTMENT = 'Account' ORDER BY DEPARTMENT;

Select * from worker; ( SELECT department, COUNT(department) AS total_employees FROM worker GROUP BY department ORDER BY total_employees ASC LIMIT 1 )

UNION ALL

( SELECT department, COUNT(department) AS total_employees FROM worker GROUP BY department ORDER BY total_employees DESC LIMIT 1 ); Create Table Persons( ID int not null, LastName varchar(255) NOT NULL, FirstName varchar(255) NOT NULL, Age int );

Alter table persons add unique(ID);

Create Table Persons1( ID int primary key, LastName varchar(255) NOT NULL unique, FirstName varchar(255) NOT NULL unique, Age int #primary key(ID) ); desc Persons1; create table category( c_id int primary key, c_name varchar(25) not null unique, c_decrp varchar(250) not null );

insert into category values (102, 'furnitures', 'it stores all set of wooden items'); select * from category; desc category;

use org123; CREATE TABLE Products ( P_ID int primary key, p_Name varchar(250) NOT NULL, c_id int , CONSTRAINT c_id FOREIGN KEY (c_id) REFERENCES category(c_id) ); show tables from org123; desc products; drop table products; insert into products values (904, 'Wooden table', null); select * from products; select * from category; delete from category where c_id=101; drop table category; CREATE TABLE Persona1 ( ID int NOT NULL, LastName varchar(255) NOT NULL, FirstName varchar (255), Age int, City varchar (255) DEFAULT 'Coimbatbre' ); desc persona1; SELECT * FROM worker; SELECT * FROM worker WHERE JOINING_DATE LIKE '2014-02%';

create view admin_ka_paisa as select * from worker where department="Admin" and salary>10000 order by salary desc; select * from admin_ka_paisa; CREATE TABLE Bonus ( WORKER_REF_ID INT, BONUS_AMOUNT INT, BONUS_DATE DATETIME, FOREIGN KEY (WORKER_REF_ID) REFERENCES Worker(WORKER_ID) ON DELETE CASCADE );

INSERT INTO Bonus (WORKER_REF_ID, BONUS_AMOUNT, BONUS_DATE) VALUES (1, 5000, '2016-02-20'), (2, 3000, '2016-06-11'), (3, 4000, '2016-02-20'), (1, 4500, '2016-02-20'), (2, 3500, '2016-06-11'); select * from worker; SELECT * FROM Worker WHERE first_name NOT IN ('Vipul', 'Satish'); select * from worker where first_name like "%a"; select * from worker where first_name like "_____h"; select department,count() as no_of_dept from worker group by department order by no_of_dept desc; SELECT * FROM Worker WHERE salary > 10000 UNION ALL SELECT * FROM Worker WHERE salary> 10000; SELECT COUNT(department) AS department_count, department FROM worker GROUP BY department HAVING COUNT(department) >= 3; SELECT department, COUNT() AS department_count FROM worker GROUP BY department ORDER BY department_count DESC LIMIT 1 OFFSET 1;

Create Table VitBhopal( id int primary key, name varchar(20) not null, department varchar(25) not null ); insert into VitBhopal values(104,'Karthik','cs'),(103,'Arun','cs'); create table vit (id int primary key, name varchar(20) not null, college varchar(25) not null); insert into vit values (104, 'Karthik', 'Chennai'), (103, 'Arun', 'bhopal'); select * from vit; select name as Winner from vitbhopal where id=(select id from vit where college="bhopal");

show databases; use temp; CREATE TABLE Worker ( WORKER_ID INT NOT NULL PRIMARY KEY AUTO_INCREMENT, FIRST_NAME CHAR(25), LAST_NAME CHAR(25), SALARY INT(15), JOINING_DATE DATETIME, DEPARTMENT CHAR(25) );

INSERT INTO Worker (WORKER_ID, FIRST_NAME, LAST_NAME, SALARY, JOINING_DATE, DEPARTMENT) VALUES (001, 'Monika', 'Arora', 100000, '14-02-20 09.00.00', 'HR'), (002, 'Niharika', 'Verma', 80000, '14-06-11 09.00.00', 'Admin'), (003, 'Vishal', 'Singhal', 300000, '14-02-20 09.00.00', 'HR'), (004, 'Amitabh', 'Singh', 500000, '14-02-20 09.00.00', 'Admin'), (005, 'Vivek', 'Bhati', 500000, '14-06-11 09.00.00', 'Admin'), (006, 'Vipul', 'Diwan', 200000, '14-06-11 09.00.00', 'Account'), (007, 'Satish', 'Kumar', 75000, '14-01-20 09.00.00', 'Account'), (008, 'Geetika', 'Chauhan', 90000, '14-04-11 09.00.00', 'Admin');

CREATE TABLE Bonus ( WORKER_REF_ID INT, BONUS_AMOUNT INT(10), BONUS_DATE DATETIME, FOREIGN KEY (WORKER_REF_ID) REFERENCES Worker(WORKER_ID) ON DELETE CASCADE );

INSERT INTO Bonus (WORKER_REF_ID, BONUS_AMOUNT, BONUS_DATE) VALUES (001, 5000, '16-02-20'), (002, 3000, '16-06-11'), (003, 4000, '16-02-20'), (001, 4500, '16-02-20'), (002, 3500, '16-06-11'); CREATE TABLE Title ( WORKER_REF_ID INT, WORKER_TITLE CHAR(25), AFFECTED_FROM DATETIME, FOREIGN KEY (WORKER_REF_ID) REFERENCES Worker(WORKER_ID) ON DELETE CASCADE );

INSERT INTO Title (WORKER_REF_ID, WORKER_TITLE, AFFECTED_FROM) VALUES (001, 'Manager', '2016-02-20 00:00:00'), (002, 'Executive', '2016-06-11 00:00:00'), (008, 'Executive', '2016-06-11 00:00:00'), (005, 'Manager', '2016-06-11 00:00:00'), (004, 'Asst. Manager', '2016-06-11 00:00:00'), (007, 'Executive', '2016-06-11 00:00:00'), (006, 'Lead', '2016-06-11 00:00:00'), (003, 'Lead', '2016-06-11 00:00:00');

#1st Question: Write an SQL query to fetch the departments that have less than five people in it. SELECT DEPARTMENT, COUNT(WORKER_ID) AS WorkerCount FROM Worker GROUP BY DEPARTMENT HAVING COUNT(WORKER_ID) < 5;

#2nd Question: Write an SQL query to fetch the last five records from a table. SELECT * FROM Worker ORDER BY WORKER_ID DESC LIMIT 5; SELECT * FROM Worker w inner JOIN Title t ON (w.WORKER_ID = t.WORKER_REF_ID) WHERE t.WORKER_TITLE = 'Manager';

use org123; create table student ( s_id int primary key, s_name varchar(25) not null, s_department varchar(25) not null );

insert into student values (1001,"Jayanth","ECE"),(1002,"Praveen","CSE"),(1003,"Logesh","Mech"),(1006,'karthick','Aero'),(1007,"Mahesh","Civil");

select * from student;

create table VIT( s_id int primary key, s_cgpa varchar(5) not null ); insert into vit values (1001,'7.2'),(1002,'8.6'),(1007,'9.25'); select * from vit;

select * from student cross join vit;

select * from student inner join vit where student.s_id=vit.s_id;

select * from student natural join vit;

select * from student left outer join vit on (student.s_id=vit.s_id); select * from student right outer join vit on (student.s_id=vit.s_id); select * from student full join vit on (student.s_id=vit.s_id);
