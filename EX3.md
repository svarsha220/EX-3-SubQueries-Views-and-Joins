# EX 3 SubQueries, Views and Joins 


## Create employee Table
```
 create table emp (empno int(5) primary key,name char(29),job char(24),sal int(5),deptno int(3));

```
## Insert the values
```
insert into emp(empno,name,job,sal,deptno) values (1234,'varsha','manager',12345,12);

insert into emp(empno,name,job,sal,deptno) values (1235,'jeeva','clerk',1234,14);

insert into emp(empno,name,job,sal,deptno) values (1236,'thilaga','clerk',1235,14);

insert into emp(empno,name,job,sal,deptno) values (1237,'swetha','manager',12315,12);

insert into emp(empno,name,job,sal,deptno) values (1238,'yuva','salesman',1345,11);

insert into emp(empno,name,job,sal,deptno) values (1239,'vidhya','accountant',2345,2);
```

## Create department table
```
create table dept(deptno int(5) primary key,deptname char(30),loc char(40));
```
## Insert the values in the department table
```
insert into dept (deptno,deptname,loc) values (2,'accounting','delhi');

insert into dept (deptno,deptname,loc) values (1,'research','pune');

insert into dept (deptno,deptname,loc) values (4,'marketing','goa');

insert into dept (deptno,deptname,loc) values (8,'manufacture','france');
```

### Q1) List the name of the employees whose salary is greater than that of employee with empno 1239 .


### QUERY:
```
 select name from emp where sal >(select sal from emp where empno=1239);
```

### OUTPUT:
![image](https://github.com/svarsha220/EX-3-SubQueries-Views-and-Joins/assets/127709117/82834903-eaca-4221-b51f-9c56a6f09c3b)

### Q2) List the ename,job,sal of the employee who get minimum salary in the company.

### QUERY:
```
 create view minimum as select name,job,sal from emp where sal =(select min(sal) from emp);
```

### OUTPUT:
![image](https://github.com/svarsha220/EX-3-SubQueries-Views-and-Joins/assets/127709117/5bbeec1b-5a39-4260-8675-fd1553f42bc6)


### Q3) List ename, job of the employees who work in deptno 10 and his/her job is any one of the job in the department ‘SALES’.

### QUERY:
```
 select name,job from emp where  deptno=10 and job='salesman';
```

### OUTPUT:
![dbms 3 3](https://github.com/svarsha220/EX-3-SubQueries-Views-and-Joins/assets/127709117/a35e4417-9819-4f13-aa33-c4b360e5691d)




### Q4) Create a view empv5 (for the table emp) that contains empno, ename, job of the employees who work in dept 12.

### QUERY:
```
 create view empv5 as select empno,name,job from emp where deptno=12;
```

### OUTPUT:
![dbms 3 4](https://github.com/svarsha220/EX-3-SubQueries-Views-and-Joins/assets/127709117/6c49bea5-40ec-430e-b860-3b03686e1796)



### Q5) Create a view with column aliases empv30 that contains empno, ename, sal of the employees who work in dept 11. Also display the contents of the view.

### QUERY:
```
 create view empv30 as select empno,name,sal from emp where deptno=11;
```

### OUTPUT:
![dbms 3 5](https://github.com/svarsha220/EX-3-SubQueries-Views-and-Joins/assets/127709117/b49a209f-1db2-4373-b6ee-5c3804e21622)

### Q6) Update the table emp by increasing 10% salary of the employees who work as ‘CLERK’. Also confirm the modifications in emp table

### QUERY:
```
 update emp set sal=sal*1.1 where job='clerk';
```

### OUTPUT:
![dbms 3 6](https://github.com/svarsha220/EX-3-SubQueries-Views-and-Joins/assets/127709117/b9b10066-2ed8-43d0-8a84-9c398a04e3c5)

## Create a Customer1 Table
```
CREATE TABLE Customer1 (customer_id INT,cust_name VARCHAR(20),city VARCHAR(20),grade INT,salesman_id INT);
```
## Inserting Values to the Table
```
sql
INSERT INTO Customer1 (customer_id, cust_name, city, grade, salesman_id) VALUES(3002, 'Nick Rimando', 'New York', 100, 5001);
INSERT INTO Customer1 (customer_id, cust_name, city, grade, salesman_id) VALUES(3007, 'Brad Davis', 'New York', 200, 5001);
INSERT INTO Customer1 (customer_id, cust_name, city, grade, salesman_id) VALUES(3005, 'Graham Zusi', 'California', 200, 5002);
INSERT INTO Customer1 (customer_id, cust_name, city, grade, salesman_id) VALUES(3008, 'Julian Green', 'London', 300, 5002);
INSERT INTO Customer1 (customer_id, cust_name, city, grade, salesman_id) VALUES(3004, 'Fabian Johnson', 'Paris', 300, 5006);
INSERT INTO Customer1 (customer_id, cust_name, city, grade, salesman_id) VALUES(3009, 'Geoff Cameron', 'Berlin', 100, 5003);
INSERT INTO Customer1 (customer_id, cust_name, city, grade, salesman_id) VALUES(3003, 'Jozy Altidor', 'Moscow', 200, 5007);
INSERT INTO Customer1 (customer_id, cust_name, city, grade, salesman_id) VALUES(3001, 'Brad Guzan', 'London', NULL, 5005);
```
## Create a Salesperson1 table
```
sql
CREATE TABLE Salesman1 (salesman_id INT,name VARCHAR(20),city VARCHAR(20),commission DECIMAL(4,2));
```
## Inserting Values to the Table
```
sql
INSERT INTO Salesman1 (salesman_id, name, city, commission) VALUES(5001, 'James Hoog', 'New York', 0.15);
INSERT INTO Salesman1 (salesman_id, name, city, commission) VALUES(5002, 'Nail Knite', 'Paris', 0.13);
INSERT INTO Salesman1 (salesman_id, name, city, commission) VALUES(5005, 'Pit Alex', 'London', 0.11);
INSERT INTO Salesman1 (salesman_id, name, city, commission) VALUES(5006, 'Mc Lyon', 'Paris', 0.14);
INSERT INTO Salesman1 (salesman_id, name, city, commission) VALUES(5007, 'Paul Adam', 'Rome', 0.13);
INSERT INTO Salesman1 (salesman_id, name, city, commission) VALUES(5003, 'Lauson Hen', 'San Jose', 0.12);
```
### Q7) Write a SQL query to find the salesperson and customer who reside in the same city. Return Salesman, cust_name and city.

### QUERY:
```
SELECT salesman1.name AS "Salesman", customer1.cust_name AS "Customer Name", salesman1.city AS "City" from salesman1 INNER JOIN customer1 ON salesman1.city=customer1.city;
```

### OUTPUT:
![image](https://github.com/svarsha220/EX-3-SubQueries-Views-and-Joins/assets/127709117/03740d61-0447-4ca7-81bc-c0aa3bb12821)


### Q8) Write a SQL query to find salespeople who received commissions of more than 13 percent from the company. Return Customer Name, customer city, Salesman, commission.


### QUERY:
```
SELECT customer1.cust_name AS "Customer Name",customer1.city AS "Customer City",salesman1.name AS "Salesman",salesman1.commission AS "Commission" FROM salesman1 INNER JOIN customer1 ON salesman1.salesman_id=customer1.salesman_id WHERE salesman1.commission>0.13;
```

### OUTPUT:
![image](https://github.com/svarsha220/EX-3-SubQueries-Views-and-Joins/assets/127709117/4cee81a9-3ba0-48b5-8711-b886db08594b)


### Q9) Perform Natural join on both tables

### QUERY:
```
SELECT customer1.cust_name AS "Customer Name",customer1.city AS "Customer City",salesman1.name AS "Salesman",salesman1.commission AS "Commission" FROM salesman1 INNER JOIN customer1 ON salesman1.salesman_id=customer1.salesman_id WHERE salesman1.commission>0.13;
```


### OUTPUT:
![image](https://github.com/svarsha220/EX-3-SubQueries-Views-and-Joins/assets/127709117/60e52b70-c6e6-457b-a473-11314fc3790a)

### Q10) Perform Left and right join on both tables

### QUERY FOR LEFT JOIN:
```
SELECT customer1.cust_name AS "Customer Name",customer1.city AS "Customer City",salesman1.name AS "Salesman",salesman1.commissioSELECT customer1.cust_name AS "Customer Name",customer1.city AS "Customer City",salesman1.name AS "Salesman",salesman1.commission AS "Commission" FROM salesman1 INNER JOIN customer1 ON salesman1.salesman_id=customer1.salesman_id WHERE salesman1.commission>0.13;
```
```
select * from customer1 natural join salesman1;
```

### OUTPUT:
![image](https://github.com/svarsha220/EX-3-SubQueries-Views-and-Joins/assets/127709117/9b763855-6a09-48b4-baad-c0c52e98e88a)

### QUERY FOR RIGHT JOIN:
```
SELECT * FROM salesman1 RIGHT JOIN customer1 ON salesman1.salesman_id=customer1.salesman_id;
```
### OUTPUT:
![image](https://github.com/svarsha220/EX-3-SubQueries-Views-and-Joins/assets/127709117/57f50dad-874b-436f-80c9-062a0e420eb1)


