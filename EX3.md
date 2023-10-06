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
 create table customer1(cusid int(8),cusname char(20),city char(92),grade int(5),salesid int(27));
```
## Inserting Values to the Table
```
insert into customer1 (cusid,cusname,city,grade,salesid) values (100,'varsha','chennai',5,123);

insert into customer1 (cusid,cusname,city,grade,sales) values (101,'swetha','kanchipuram',4,124);

insert into customer1 (cusid,cusname,city,grade,salesid) values (102,'dhivya','chennai',3,124);

insert into customer1 (cusid,cusname,city,grade,salesid) values (103,'vidhya','mumbai',2,125);

insert into customer1 (cusid,cusname,city,grade,salesid) values (104,'yuva','hyd',1,126);
```
## Create a Salesperson table
```
create table salesperson (salesid int(2),city char(39),salesname char(20),commission int(5));
```
## Inserting Values to the Table
```
insert into salesperson(salesid,city,salesname,commission) values(1,'chennai','dhru',500);

insert into salesperson(salesid,city,salesname,commission) values(2,'hyd','nive',200);

insert into salesperson(salesid,city,salesname,commission) values(3,'mumbai','deepesh',400);

insert into salesperson(salesid,city,salesname,commission) values(4,'kanchipuram','jeeva',100);
```
### Q7) Write a SQL query to find the salesperson and customer who reside in the same city. Return Salesman, cust_name and city.

### QUERY:
```
select salesperson.salesname AS "Salesman", customer1.cusname as "Customer Name", salesperson.city AS "City" from salesperson inner join customer1 on salesperson.city=customer1.city;
```

### OUTPUT:
![dbms 3 7](https://github.com/svarsha220/EX-3-SubQueries-Views-and-Joins/assets/127709117/02e6eae3-0ce4-4d00-a495-aff841f64255)



### Q8) Write a SQL query to find salespeople who received commissions of more than 100. Return Customer Name, customer city, Salesman, commission.


### QUERY:
```
select customer1.cusname as "Customer Name",customer1.city as "Customer City",salesperson.salesname AS "Salesman",salesperson.commission as "Commission" from salesperson inner join customer1 on salesperson.salesid=customer1.salesid where salesperson.commission>100;
```

### OUTPUT:

![dbms 3 8](https://github.com/svarsha220/EX-3-SubQueries-Views-and-Joins/assets/127709117/68e4224a-ebcf-44aa-986b-3da6fb22eca8)


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


