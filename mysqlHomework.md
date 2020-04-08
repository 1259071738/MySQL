## 作业目录：
##### 1.查询数据库，添加数据库，创建数据表并添加字段。
##### 2.查询数据库、删除数据库、建表、添加主键、逐条增加/一次增加多条字段。
##### 3.输出我、我的老板、我的老板的老板
##### 4.这两个query，用join能不能写
##### 5.运行上述储存过程和函数






### 1.查询数据库，添加数据库，创建数据表并添加字段。

~~~MYSQL
mysql> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| sys                |
+--------------------+
4 rows in set (0.17 sec)

mysql>  use std_num;
mysql> create database std_num;
Query OK, 1 row affected (0.17 sec)

mysql> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| std_num            |
| sys                |
+--------------------+
5 rows in set (0.16 sec)


Database changed
mysql> create table std_num
    -> (
    -> num INT,
    -> name CHAR
    -> );
Query OK, 0 rows affected (1.07 sec)

mysql> describe std_num;
+-------+---------+------+-----+---------+-------+
| Field | Type    | Null | Key | Default | Extra |
+-------+---------+------+-----+---------+-------+
| num   | int(11) | YES  |     | NULL    |       |
| name  | char(1) | YES  |     | NULL    |       |
+-------+---------+------+-----+---------+-------+
2 rows in set (0.11 sec)


~~~



### 2.查询数据库、删除数据库、建表、添加主键、逐条增加/一次增加多条字段。

~~~mysql
mysql> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| std_num            |
| sys                |
| text_db            |
+--------------------+
6 rows in set (0.00 sec)

mysql> drop database std_num;
Query OK, 1 row affected (0.85 sec)

mysql> use text_db;
Database changed
mysql> create table membertable
    -> (
    -> student_id VARCHAR(25),
    -> name VARCHAR(255)
    -> );
Query OK, 0 rows affected (0.65 sec)

mysql> alter table membertable
    -> ADD PRIMARY KEY(student_id);
Query OK, 0 rows affected (1.25 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> describe membertable;
+------------+--------------+------+-----+---------+-------+
| Field      | Type         | Null | Key | Default | Extra |
+------------+--------------+------+-----+---------+-------+
| student_id | varchar(25)  | NO   | PRI | NULL    |       |
| name       | varchar(255) | YES  |     | NULL    |       |
+------------+--------------+------+-----+---------+-------+
2 rows in set (0.00 sec)

mysql> insert into membertable
    -> (student_id,name)
    -> VALUES(17060001,'张三');
Query OK, 1 row affected (0.12 sec)
mysql> insert into membertable
    -> (student_id,name)
    -> VALUES(17060002,'李四');
Query OK, 1 row affected (0.16 sec)
mysql> insert into membertable
    -> (student_id,name)
    -> VALUES(17060003,'王五');
Query OK, 1 row affected (0.04 sec)
mysql> insert into membertable
    -> (student_id,name)
    ->  VALUES(17060004,'赵刚');
Query OK, 1 row affected (0.09 sec)

mysql> insert into membertable
    -> (student_id,name)
    -> VALUES(17060005,'李云龙');
Query OK, 1 row affected (0.02 sec)

mysql> select*from membertable;
+------------+-----------+
| student_id | name      |
+------------+-----------+
| 17060001   | 张三      |
| 17060002   | 李四      |
| 17060003   | 王五      |
| 17060004   | 赵刚      |
| 17060005   | 李云龙    |
+------------+-----------+
5 rows in set (0.03 sec)

mysql> create table course
    -> (
    -> num VARCHAR(4),
    -> course VARCHAR(25)
    -> );
Query OK, 0 rows affected (0.39 sec)

mysql> alter table course
    -> ADD PRIMARY KEY(course);
Query OK, 0 rows affected (0.58 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> describe course;
+--------+-------------+------+-----+---------+-------+
| Field  | Type        | Null | Key | Default | Extra |
+--------+-------------+------+-----+---------+-------+
| num    | varchar(4)  | YES  |     | NULL    |       |
| course | varchar(25) | NO   | PRI | NULL    |       |
+--------+-------------+------+-----+---------+-------+
2 rows in set (0.02 sec)

mysql> insert into course
    -> (num,course)
    -> VALUES(1,'吹'),(2,'拉'),(3,'弹'),(4,'唱'),(5,'跳'),(6,'rap'),(7,'篮球'),(8,'足球'),(9,'排球'),(10,'网球');
Query OK, 10 rows affected (0.06 sec)
Records: 10  Duplicates: 0  Warnings: 0

mysql> select*from course order by num;
+------+--------+
| num  | course |
+------+--------+
| 1    | 吹     |
| 10   | 网球   |
| 2    | 拉     |
| 3    | 弹     |
| 4    | 唱     |
| 5    | 跳     |
| 6    | rap    |
| 7    | 篮球   |
| 8    | 足球   |
| 9    | 排球   |
+------+--------+
10 rows in set (0.19 sec)
~~~



### 3.输出我、我的老板、我的老板的老板

~~~mysql
mysql> create database em;
Query OK, 1 row affected (0.13 sec)

mysql> use em;
Database changed
mysql> create table t_employee
    -> (
    -> deptno INT NOT NULL,
    -> empno INT  PRIMARY KEY,
    -> ename VARCHAR(20),
    -> job  VARCHAR(20),
    ->     MGR  INT,
    -> Hiredate Date,
    -> sal    float,
    -> comm   float
    -> );
Query OK, 0 rows affected (0.56 sec)

mysql> INSERT INTO t_employee(empno, ename, job, MGR, Hiredate, sal, comm, deptno)
    -> values(7369, "SMITH", "CLERK", 7902, "1981-03-12", 800.00, NULL, 20),
    -> (7499, "ALLEN", "SALESMAN", 7698, "1982-03-12", 1600, 300, 30),
    -> (7521, "WARD", "SALESMAN", 7698, "1838-03-12", 1250, 500, 30),
    -> (7566, "JONES", "MANAGER", 7839, "1981-03-12", 2975, NULL, 20),
    -> (7654, "MARTIN", "SALESMAN", 7698, "1981-01-12", 1250, 1400, 30),
    -> (7698, "BLAKE", "MANAGER", 7839, "1985-03-12", 2450, NULL, 10),
    -> (7788, "SCOTT", "ANALYST", 7566, "1981-03-12", 3000, NULL, 20),
    -> (7839, "KING", "PRESIDENT", NULL, "1981-03-12", 5000, NULL, 10),
    -> (7844, "TURNER", "SALESMAN", 7689, "1981-03-12", 1500, 0, 30),
    -> (7878, "ADAMS", "CLERK", 7788, "1981-03-12", 1100, NULL,20),
    -> (7900, "JAMES", "CLERK", 7698,"1981-03-12",  950, NULL, 30),
    -> (7902, "FORD", "ANALYST", 7566, "1981-03-12", 3000, NULL, 20),
    -> (7934, "MILLER", "CLERK", 7782, "1981-03-12", 1300, NULL, 10)
    -> ;
Query OK, 13 rows affected (0.06 sec)
Records: 13  Duplicates: 0  Warnings: 0

mysql> select*from t_employee;
+--------+-------+--------+-----------+------+------------+------+------+
| deptno | empno | ename  | job       | MGR  | Hiredate   | sal  | comm |
+--------+-------+--------+-----------+------+------------+------+------+
|     20 |  7369 | SMITH  | CLERK     | 7902 | 1981-03-12 |  800 | NULL |
|     30 |  7499 | ALLEN  | SALESMAN  | 7698 | 1982-03-12 | 1600 |  300 |
|     30 |  7521 | WARD   | SALESMAN  | 7698 | 1838-03-12 | 1250 |  500 |
|     20 |  7566 | JONES  | MANAGER   | 7839 | 1981-03-12 | 2975 | NULL |
|     30 |  7654 | MARTIN | SALESMAN  | 7698 | 1981-01-12 | 1250 | 1400 |
|     10 |  7698 | BLAKE  | MANAGER   | 7839 | 1985-03-12 | 2450 | NULL |
|     20 |  7788 | SCOTT  | ANALYST   | 7566 | 1981-03-12 | 3000 | NULL |
|     10 |  7839 | KING   | PRESIDENT | NULL | 1981-03-12 | 5000 | NULL |
|     30 |  7844 | TURNER | SALESMAN  | 7689 | 1981-03-12 | 1500 |    0 |
|     20 |  7878 | ADAMS  | CLERK     | 7788 | 1981-03-12 | 1100 | NULL |
|     30 |  7900 | JAMES  | CLERK     | 7698 | 1981-03-12 |  950 | NULL |
|     20 |  7902 | FORD   | ANALYST   | 7566 | 1981-03-12 | 3000 | NULL |
|     10 |  7934 | MILLER | CLERK     | 7782 | 1981-03-12 | 1300 | NULL |
+--------+-------+--------+-----------+------+------------+------+------+
13 rows in set (0.00 sec)

mysql> select*from(t_employee t1 inner join t_employee t2 on t1. mgr=t2.empno)
    -> inner join t_employee t3 on t2. mgr=t3.empno;
+--------+-------+--------+----------+------+------------+------+------+--------+-------+-------+---------+------+------------+------+------+--------+-------+-------+-----------+------+------------+------+------+
| deptno | empno | ename  | job      | MGR  | Hiredate   | sal  | comm | deptno | empno | ename | job     | MGR  | Hiredate   | sal  | comm | deptno | empno | ename | job       | MGR  | Hiredate   | sal  | comm |
+--------+-------+--------+----------+------+------------+------+------+--------+-------+-------+---------+------+------------+------+------+--------+-------+-------+-----------+------+------------+------+------+
|     20 |  7369 | SMITH  | CLERK    | 7902 | 1981-03-12 |  800 | NULL |     20 |  7902 | FORD  | ANALYST | 7566 | 1981-03-12 | 3000 | NULL |     20 |  7566 | JONES | MANAGER   | 7839 | 1981-03-12 | 2975 | NULL |
|     30 |  7499 | ALLEN  | SALESMAN | 7698 | 1982-03-12 | 1600 |  300 |     10 |  7698 | BLAKE | MANAGER | 7839 | 1985-03-12 | 2450 | NULL |     10 |  7839 | KING  | PRESIDENT | NULL | 1981-03-12 | 5000 | NULL |
|     30 |  7521 | WARD   | SALESMAN | 7698 | 1838-03-12 | 1250 |  500 |     10 |  7698 | BLAKE | MANAGER | 7839 | 1985-03-12 | 2450 | NULL |     10 |  7839 | KING  | PRESIDENT | NULL | 1981-03-12 | 5000 | NULL |
|     30 |  7654 | MARTIN | SALESMAN | 7698 | 1981-01-12 | 1250 | 1400 |     10 |  7698 | BLAKE | MANAGER | 7839 | 1985-03-12 | 2450 | NULL |     10 |  7839 | KING  | PRESIDENT | NULL | 1981-03-12 | 5000 | NULL |
|     20 |  7788 | SCOTT  | ANALYST  | 7566 | 1981-03-12 | 3000 | NULL |     20 |  7566 | JONES | MANAGER | 7839 | 1981-03-12 | 2975 | NULL |     10 |  7839 | KING  | PRESIDENT | NULL | 1981-03-12 | 5000 | NULL |
|     20 |  7878 | ADAMS  | CLERK    | 7788 | 1981-03-12 | 1100 | NULL |     20 |  7788 | SCOTT | ANALYST | 7566 | 1981-03-12 | 3000 | NULL |     20 |  7566 | JONES | MANAGER   | 7839 | 1981-03-12 | 2975 | NULL |
|     30 |  7900 | JAMES  | CLERK    | 7698 | 1981-03-12 |  950 | NULL |     10 |  7698 | BLAKE | MANAGER | 7839 | 1985-03-12 | 2450 | NULL |     10 |  7839 | KING  | PRESIDENT | NULL | 1981-03-12 | 5000 | NULL |
|     20 |  7902 | FORD   | ANALYST  | 7566 | 1981-03-12 | 3000 | NULL |     20 |  7566 | JONES | MANAGER | 7839 | 1981-03-12 | 2975 | NULL |     10 |  7839 | KING  | PRESIDENT | NULL | 1981-03-12 | 5000 | NULL |
+--------+-------+--------+----------+------+------------+------+------+--------+-------+-------+---------+------+------------+------+------+--------+-------+-------+-----------+------+------------+------+------+
8 rows in set (0.06 sec)

mysql> select t1.ename My_name,t2.ename My_b_name ,t3.ename My_b_b_name
    -> from (t_employee t1 inner join t_employee t2 on t1. mgr= t2.empno )inner join t_employee t3
    -> on t2. mgr= t3.empno;
+---------+-----------+-------------+
| My_name | My_b_name | My_b_b_name |
+---------+-----------+-------------+
| SMITH   | FORD      | JONES       |
| ALLEN   | BLAKE     | KING        |
| WARD    | BLAKE     | KING        |
| MARTIN  | BLAKE     | KING        |
| SCOTT   | JONES     | KING        |
| ADAMS   | SCOTT     | JONES       |
| JAMES   | BLAKE     | KING        |
| FORD    | JONES     | KING        |
+---------+-----------+-------------+
8 rows in set (0.01 sec)
~~~



### 4.这两个query，用join能不能写

~~~mysql
mysql> select t1.deptno,t1.empno,t1.ename,t1.job,t1.mgr,t1.hiredate,t1.sal,t1.comm
    -> from t_employee t1 inner join t_employee t2
    -> on t1.sal>t2.sal and (t2.ename='SMITH');
+--------+-------+--------+-----------+------+------------+------+------+
| deptno | empno | ename  | job       | mgr  | hiredate   | sal  | comm |
+--------+-------+--------+-----------+------+------------+------+------+
|     30 |  7499 | ALLEN  | SALESMAN  | 7698 | 1982-03-12 | 1600 |  300 |
|     30 |  7521 | WARD   | SALESMAN  | 7698 | 1838-03-12 | 1250 |  500 |
|     20 |  7566 | JONES  | MANAGER   | 7839 | 1981-03-12 | 2975 | NULL |
|     30 |  7654 | MARTIN | SALESMAN  | 7698 | 1981-01-12 | 1250 | 1400 |
|     10 |  7698 | BLAKE  | MANAGER   | 7839 | 1985-03-12 | 2450 | NULL |
|     20 |  7788 | SCOTT  | ANALYST   | 7566 | 1981-03-12 | 3000 | NULL |
|     10 |  7839 | KING   | PRESIDENT | NULL | 1981-03-12 | 5000 | NULL |
|     30 |  7844 | TURNER | SALESMAN  | 7689 | 1981-03-12 | 1500 |    0 |
|     20 |  7878 | ADAMS  | CLERK     | 7788 | 1981-03-12 | 1100 | NULL |
|     30 |  7900 | JAMES  | CLERK     | 7698 | 1981-03-12 |  950 | NULL |
|     20 |  7902 | FORD   | ANALYST   | 7566 | 1981-03-12 | 3000 | NULL |
|     10 |  7934 | MILLER | CLERK     | 7782 | 1981-03-12 | 1300 | NULL |
+--------+-------+--------+-----------+------+------------+------+------+
12 rows in set (0.02 sec)

mysql> select*from t_employee;
+--------+-------+--------+-----------+------+------------+------+------+
| deptno | empno | ename  | job       | MGR  | Hiredate   | sal  | comm |
+--------+-------+--------+-----------+------+------------+------+------+
|     20 |  7369 | SMITH  | CLERK     | 7902 | 1981-03-12 |  800 | NULL |
|     30 |  7499 | ALLEN  | SALESMAN  | 7698 | 1982-03-12 | 1600 |  300 |
|     30 |  7521 | WARD   | SALESMAN  | 7698 | 1838-03-12 | 1250 |  500 |
|     20 |  7566 | JONES  | MANAGER   | 7839 | 1981-03-12 | 2975 | NULL |
|     30 |  7654 | MARTIN | SALESMAN  | 7698 | 1981-01-12 | 1250 | 1400 |
|     10 |  7698 | BLAKE  | MANAGER   | 7839 | 1985-03-12 | 2450 | NULL |
|     20 |  7788 | SCOTT  | ANALYST   | 7566 | 1981-03-12 | 3000 | NULL |
|     10 |  7839 | KING   | PRESIDENT | NULL | 1981-03-12 | 5000 | NULL |
|     30 |  7844 | TURNER | SALESMAN  | 7689 | 1981-03-12 | 1500 |    0 |
|     20 |  7878 | ADAMS  | CLERK     | 7788 | 1981-03-12 | 1100 | NULL |
|     30 |  7900 | JAMES  | CLERK     | 7698 | 1981-03-12 |  950 | NULL |
|     20 |  7902 | FORD   | ANALYST   | 7566 | 1981-03-12 | 3000 | NULL |
|     10 |  7934 | MILLER | CLERK     | 7782 | 1981-03-12 | 1300 | NULL |
+--------+-------+--------+-----------+------+------------+------+------+
13 rows in set (0.00 sec)
~~~

~~~
mysql> select * from t_employee WHERE sal > (
    -> select sal from t_employee WHERE ename='SMITH');
+--------+-------+--------+-----------+------+------------+------+------+
| deptno | empno | ename  | job       | MGR  | Hiredate   | sal  | comm |
+--------+-------+--------+-----------+------+------------+------+------+
|     30 |  7499 | ALLEN  | SALESMAN  | 7698 | 1982-03-12 | 1600 |  300 |
|     30 |  7521 | WARD   | SALESMAN  | 7698 | 1838-03-12 | 1250 |  500 |
|     20 |  7566 | JONES  | MANAGER   | 7839 | 1981-03-12 | 2975 | NULL |
|     30 |  7654 | MARTIN | SALESMAN  | 7698 | 1981-01-12 | 1250 | 1400 |
|     10 |  7698 | BLAKE  | MANAGER   | 7839 | 1985-03-12 | 2450 | NULL |
|     20 |  7788 | SCOTT  | ANALYST   | 7566 | 1981-03-12 | 3000 | NULL |
|     10 |  7839 | KING   | PRESIDENT | NULL | 1981-03-12 | 5000 | NULL |
|     30 |  7844 | TURNER | SALESMAN  | 7689 | 1981-03-12 | 1500 |    0 |
|     20 |  7878 | ADAMS  | CLERK     | 7788 | 1981-03-12 | 1100 | NULL |
|     30 |  7900 | JAMES  | CLERK     | 7698 | 1981-03-12 |  950 | NULL |
|     20 |  7902 | FORD   | ANALYST   | 7566 | 1981-03-12 | 3000 | NULL |
|     10 |  7934 | MILLER | CLERK     | 7782 | 1981-03-12 | 1300 | NULL |
+--------+-------+--------+-----------+------+------------+------+------+
12 rows in set (0.03 sec)

mysql> select t1.deptno,t1.empno,t1.ename,t1.job,t1.MGR,t1.Hiredate,t1.sal,t1.comm
    -> from t_employee t1 inner join t_employee t2
    -> on (t1.sal = t2.sal and (t2.ename='SMITH')) AND (t1.job = t2.job and (t2.ename='SMITH'));
+--------+-------+-------+-------+------+------------+------+------+
| deptno | empno | ename | job   | MGR  | Hiredate   | sal  | comm |
+--------+-------+-------+-------+------+------------+------+------+
|     20 |  7369 | SMITH | CLERK | 7902 | 1981-03-12 |  800 | NULL |
+--------+-------+-------+-------+------+------------+------+------+
1 row in set (0.00 sec)
~~~



### 5.运行上述储存过程和函数

#### （1）创建储存过程

~~~mysql
mysql> SELECT * FROM t_employee;
+--------+-------+--------+-----------+------+------------+------+------+
| deptno | empno | ename  | job       | MGR  | Hiredate   | sal  | comm |
+--------+-------+--------+-----------+------+------------+------+------+
|     20 |  7369 | SMITH  | CLERK     | 7902 | 1981-03-12 |  800 | NULL |
|     30 |  7499 | ALLEN  | SALESMAN  | 7698 | 1982-03-12 | 1600 |  300 |
|     30 |  7521 | WARD   | SALESMAN  | 7698 | 1838-03-12 | 1250 |  500 |
|     20 |  7566 | JONES  | MANAGER   | 7839 | 1981-03-12 | 2975 | NULL |
|     30 |  7654 | MARTIN | SALESMAN  | 7698 | 1981-01-12 | 1250 | 1400 |
|     10 |  7698 | BLAKE  | MANAGER   | 7839 | 1985-03-12 | 2450 | NULL |
|     20 |  7788 | SCOTT  | ANALYST   | 7566 | 1981-03-12 | 3000 | NULL |
|     10 |  7839 | KING   | PRESIDENT | NULL | 1981-03-12 | 5000 | NULL |
|     30 |  7844 | TURNER | SALESMAN  | 7689 | 1981-03-12 | 1500 |    0 |
|     20 |  7878 | ADAMS  | CLERK     | 7788 | 1981-03-12 | 1100 | NULL |
|     30 |  7900 | JAMES  | CLERK     | 7698 | 1981-03-12 |  950 | NULL |
|     20 |  7902 | FORD   | ANALYST   | 7566 | 1981-03-12 | 3000 | NULL |
|     10 |  7934 | MILLER | CLERK     | 7782 | 1981-03-12 | 1300 | NULL |
+--------+-------+--------+-----------+------+------------+------+------+
13 rows in set (0.00 sec)

mysql> DELIMITER $$
mysql> CREATE PROCEDURE proce_employee_sal1 ()
    -> BEGIN
    -> SELECT sal
    -> FROM t_employee2;
    -> END$$
ERROR 1304 (42000): PROCEDURE proce_employee_sal1 already exists
mysql> DELIMITER ;
mysql> CALL proce_employee_sal1();
+------+
| sal  |
+------+
|  800 |
| 1600 |
| 1250 |
| 2975 |
| 1250 |
| 2450 |
| 3000 |
| 5000 |
| 1500 |
| 1100 |
|  950 |
| 3000 |
| 1300 |
+------+
13 rows in set (0.02 sec)

Query OK, 0 rows affected (0.02 sec)
~~~

#### （2）创建函数

~~~mysql
mysql> SELECT * FROM t_employee;
+--------+-------+--------+-----------+------+------------+------+------+
| deptno | empno | ename  | job       | MGR  | Hiredate   | sal  | comm |
+--------+-------+--------+-----------+------+------------+------+------+
|     20 |  7369 | SMITH  | CLERK     | 7902 | 1981-03-12 |  800 | NULL |
|     30 |  7499 | ALLEN  | SALESMAN  | 7698 | 1982-03-12 | 1600 |  300 |
|     30 |  7521 | WARD   | SALESMAN  | 7698 | 1838-03-12 | 1250 |  500 |
|     20 |  7566 | JONES  | MANAGER   | 7839 | 1981-03-12 | 2975 | NULL |
|     30 |  7654 | MARTIN | SALESMAN  | 7698 | 1981-01-12 | 1250 | 1400 |
|     10 |  7698 | BLAKE  | MANAGER   | 7839 | 1985-03-12 | 2450 | NULL |
|     20 |  7788 | SCOTT  | ANALYST   | 7566 | 1981-03-12 | 3000 | NULL |
|     10 |  7839 | KING   | PRESIDENT | NULL | 1981-03-12 | 5000 | NULL |
|     30 |  7844 | TURNER | SALESMAN  | 7689 | 1981-03-12 | 1500 |    0 |
|     20 |  7878 | ADAMS  | CLERK     | 7788 | 1981-03-12 | 1100 | NULL |
|     30 |  7900 | JAMES  | CLERK     | 7698 | 1981-03-12 |  950 | NULL |
|     20 |  7902 | FORD   | ANALYST   | 7566 | 1981-03-12 | 3000 | NULL |
|     10 |  7934 | MILLER | CLERK     | 7782 | 1981-03-12 | 1300 | NULL |
+--------+-------+--------+-----------+------+------------+------+------+
13 rows in set (0.00 sec)

mysql> DELIMITER $$
mysql> CREATE FUNCTION func_employee_sal (empno INT)
    -> RETURNS DOUBLE
    -> BEGIN
    -> RETURN (SELECT sal
    -> FROM t_employee
    -> WHERE t_employee.empno = empno);
    -> END$$
ERROR 1304 (42000): FUNCTION func_employee_sal already exists
mysql> DELIMITER ;
mysql>
mysql> SELECT func_employee_sal(7369);
+-------------------------+
| func_employee_sal(7369) |
+-------------------------+
|                     800 |
+-------------------------+
1 row in set (0.00 sec)

mysql> SELECT func_employee_sal(7934);
+-------------------------+
| func_employee_sal(7934) |
+-------------------------+
|                    1300 |
+-------------------------+
1 row in set (0.00 sec)
~~~







