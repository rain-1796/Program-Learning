---
title: MySQL——34道查询练习题
date: 2024-03-29 23:31
tags: "MySQL"
categories: "编程学习"
---

**村雨的34道MySQL查询练习题**

基于bilibili动力节点的教学视频

<!-- more -->

------



## **emp员工表**

![](http://villagerain.oss-cn-huhehaote.aliyuncs.com/imgSnipaste_2024-03-29_23-34-29.png)

## **dept部门表**

![](http://villagerain.oss-cn-huhehaote.aliyuncs.com/imgSnipaste_2024-03-29_23-35-16.png)

## **salgrade工资等级表**

![](http://villagerain.oss-cn-huhehaote.aliyuncs.com/imgSnipaste_2024-03-29_23-35-52.png)

## **1、取得每个部门最高薪水的人员名称**

```sql
1.
select deptno,max(sal) as max_sal from emp group by deptno; -- 按部门分组，找出每个部门的最高薪资
+--------+---------+
| deptno | max_sal |
+--------+---------+
|     20 | 3000.00 |
|     30 | 2850.00 |
|     10 | 5000.00 |
+--------+---------+
2.
select ename,t.*
from emp e
join (select deptno,max(sal) as max_sal from emp group by deptno) as t -- 将上面的查询结果作为新表t与emp表连接
on e.deptno = t.deptno and sal = max_sal; -- 查询条件：emp表中薪水等于所属部门的最高薪水
+-------+--------+---------+
| ename | deptno | max_sal |
+-------+--------+---------+
| BLAKE |     30 | 2850.00 |
| SCOTT |     20 | 3000.00 |
| KING  |     10 | 5000.00 |
| FORD  |     20 | 3000.00 |
+-------+--------+---------+
```



## **2.哪些人的薪水在部门的平均薪水之上**

```sql
1.
select deptno,avg(sal) as avg_sal
from emp group by deptno; -- 按部门分组，求出每个部门的平均薪水
+--------+-------------+
| deptno | avg_sal     |
+--------+-------------+
|     20 | 2175.000000 |
|     30 | 1566.666667 |
|     10 | 2916.666667 |
+--------+-------------+
2.
select t.*,ename,sal
from emp e
join (select avg(sal) as avg_sal,deptno -- 将上面的查询结果作为新表t和emp表连接
      from emp group by deptno) as t
on e.deptno = t.deptno and sal > avg_sal; -- 筛选出薪水大于所在部门平均薪水的员工
+-------------+--------+-------+---------+
| avg_sal     | deptno | ename | sal     |
+-------------+--------+-------+---------+
| 2175.000000 |     20 | FORD  | 3000.00 |
| 2175.000000 |     20 | SCOTT | 3000.00 |
| 2175.000000 |     20 | JONES | 2975.00 |
| 1566.666667 |     30 | BLAKE | 2850.00 |
| 1566.666667 |     30 | ALLEN | 1600.00 |
| 2916.666667 |     10 | KING  | 5000.00 |
+-------------+--------+-------+---------+
```

**将两张表连接后**：可以看到每一行都有sal和员工所属部门的avg_sal，筛选出sal > avg_sal的员工

![](http://villagerain.oss-cn-huhehaote.aliyuncs.com/imgSnipaste_2024-03-29_23-30-50.png)

## **3.取得部门中（所有人的）平均的薪水等级，如下**

```sql
select deptno,avg(grade) as avg_grade
from emp e
join salgrade s
on e.sal between s.losal and s.hisal -- 将emp表和salgrade表连接起来-非等值连接
group by deptno -- 按部门分组
order by deptno;-- 按部门编号升序查询结果-默认是升序
+--------+-----------+
| deptno | avg_grade |
+--------+-----------+
|     10 |    3.6667 |
|     20 |    2.8000 |
|     30 |    2.5000 |
+--------+-----------+
```

## **4.不准用分组函数（Max），取得所有员工中的最高薪水（给出两种解决方案）**

```sql
第一种：降序取第一行
select ename,sal 
from emp 
order by sal desc  -- 按照工资降序查找，那么第一行便是最高薪水
limit 1; -- 只取前1行
+-------+---------+
| ename | sal     |
+-------+---------+
| KING  | 5000.00 |
+-------+---------+

第二种：表的自连接
1.
select distinct a.sal -- distinct去重
from emp a
join emp b
on a.sal < b.sal; -- 除了最高薪水都会被筛选出来
+---------+
| sal     |
+---------+
| 1300.00 |
|  950.00 |
| 1100.00 |
| 1500.00 |
| 1250.00 |
|  800.00 |
| 2450.00 |
| 2850.00 |
| 1600.00 |
| 2975.00 |
| 3000.00 |
+---------+
2.
select ename,sal
from emp
where sal not in (select distinct a.sal -- 找出薪水不在这里面的员工，即只有最高薪水的员工不在
              from emp a
              join emp b
              on a.sal < b.sal);
+-------+---------+
| ename | sal     |
+-------+---------+
| KING  | 5000.00 |
+-------+---------+

第三种:使用组函数最简单
select max(sal) as max_sal -- 没有手动分组，整张表默认为一组。但是select后只能跟组函数
from emp;
+---------+
| max_sal |
+---------+
| 5000.00 |
+---------+
```

## **5.取得平均薪水最高的部门的部门编号（至少给出两种解决方案）**

```sql
第一种：降序取第一行
select deptno,avg(sal) as avg_sal
from emp
group by deptno
order by avg_sal desc -- 降序
limit 1; -- 取前1行
+--------+-------------+
| deptno | avg_sal     |
+--------+-------------+
|     10 | 2916.666667 |
+--------+-------------+

第二种：
1.取得每个部门的平均薪水
select deptno,avg(sal) as avg_sal
from emp 
group by deptno;
+--------+-------------+
| deptno | avg_sal     |
+--------+-------------+
|     20 | 2175.000000 |
|     30 | 1566.666667 |
|     10 | 2916.666667 |
+--------+-------------+
2.取得部门平均薪水中最高的薪水
select max(avg_sal) as max_avg_sal
from(select avg(sal) as avg_sal 
     from emp 
     group by deptno) as t; -- 把第一步的查询结果当作新表t
+-------------+
| max_avg_sal |
+-------------+
| 2916.666667 |
+-------------+
3.在emp表中筛选平均薪水等于第二步查询结果的部门
select deptno,avg(sal) as avg_sal
from emp
group by deptno
having avg_sal = (select max(avg_sal) as max_avg_sal -- 条件筛选
                   from(select avg(sal) as avg_sal 
                        from emp 
                        group by deptno) as t);
+--------+-------------+
| deptno | avg_sal     |
+--------+-------------+
|     10 | 2916.666667 |
+--------+-------------+
```

## **6.取得平均薪水最高的部门的部门名称**

```sql
1.取得平均薪水最高的部门
select deptno,avg(sal) as avg_sal
from emp
group by deptno
order by avg_sal desc -- 降序
limit 1; -- 取前1行
+--------+-------------+
| deptno | avg_sal     |
+--------+-------------+
|     10 | 2916.666667 |
+--------+-------------+
2.将第一步的查询结果作为新表t和dept表连接
select dname,avg_sal
from dept d
join (select deptno,avg(sal) as avg_sal
      from emp
      group by deptno
      order by avg_sal desc -- 降序
      limit 1) as t
on d.deptno = t.deptno;
+------------+-------------+
| dname      | avg_sal     |
+------------+-------------+
| ACCOUNTING | 2916.666667 |
+------------+-------------+
```

## **7.求平均薪水的等级最低的部门的部门名称**

```sql
1.取得部门的平均薪水
select deptno,avg(sal) as avg_sal
from emp 
group by deptno;
+--------+-------------+
| deptno | avg_sal     |
+--------+-------------+
|     20 | 2175.000000 |
|     30 | 1566.666667 |
|     10 | 2916.666667 |
+--------+-------------+
2.取得部门平均薪水所对应的等级
select t.*,grade
from salgrade s
join (select deptno,avg(sal) as avg_sal
      from emp 
      group by deptno) as t
on avg_sal between losal and hisal;
+--------+-------------+-------+
| deptno | avg_sal     | grade |
+--------+-------------+-------+
|     20 | 2175.000000 |     4 |
|     30 | 1566.666667 |     3 |
|     10 | 2916.666667 |     4 |
+--------+-------------+-------+
3.将第二步的查询结果与dept表连接
select dname,q.*
from dept d
join (select t.*,grade
from salgrade s
join (select deptno,avg(sal) as avg_sal
      from emp 
      group by deptno) as t
      on avg_sal between losal and hisal) as q
 on d.deptno = q.deptno;
+------------+--------+-------------+-------+
| dname      | deptno | avg_sal     | grade |
+------------+--------+-------------+-------+
| SALES      |     30 | 1566.666667 |     3 |
| RESEARCH   |     20 | 2175.000000 |     4 |
| ACCOUNTING |     10 | 2916.666667 |     4 |
+------------+--------+-------------+-------+
4.使第三步的查询结果按薪资等级升序，取第一行
select dname,grade
from (select dname,q.*
      from dept d
      join (select t.*,grade
            from salgrade s
            join (select deptno,avg(sal) as avg_sal
                  from emp 
                  group by deptno) as t
                  on avg_sal between losal and hisal) as q
       on d.deptno = q.deptno) as p
 order by grade
 limit 1;
 +-------+-------+
| dname | grade |
+-------+-------+
| SALES |     3 |
+-------+-------+
```

## 8.**取得比普通员工（员工代码没有在mgr 字段上出现的）的最高薪水还要高的领导人姓名**

```sql
1.先取得所有领导代码
select distinct mgr 
from emp 
where mgr is not null; -- 重点:使用 not in 的时候要确保所查范围中没有NULL
+------+
| mgr  |
+------+
| 7902 |
| 7698 |
| 7839 |
| 7566 |
| 7788 |
| 7782 |
+------+
2.不属于领导的就是普通员工，找出普通员工中的最高薪水
select max(sal) as max_sal
from emp
where empno not in (select distinct mgr 
                    from emp 
                    where mgr is not null); -- 重点:使用 not in 的时候要确保所查范围中没有NULL
                                            -- 在 SQL 中与 NULL 的比较通常会返回未知，而不是 True 或 False
+---------+
| max_sal |
+---------+
| 1600.00 |
+---------+
3.取得大于第二步查询结果的领导名
select ename,sal
from emp
where sal > (select max(sal) as max_sal
             from emp
             where empno not in (select distinct mgr 
                                 from emp 
                                 where mgr is not null));
 +-------+---------+
| ename | sal     |
+-------+---------+
| JONES | 2975.00 |
| BLAKE | 2850.00 |
| CLARK | 2450.00 |
| SCOTT | 3000.00 |
| KING  | 5000.00 |
| FORD  | 3000.00 |
+-------+---------+
```

## **9.取得薪水最高的前五名员工**

```sql
select ename,sal
from emp
order by sal desc -- 降序
limit 5; -- 取前5行
+-------+---------+
| ename | sal     |
+-------+---------+
| KING  | 5000.00 |
| SCOTT | 3000.00 |
| FORD  | 3000.00 |
| JONES | 2975.00 |
| BLAKE | 2850.00 |
+-------+---------+
```

## **10.取得薪水最高的第六到第十名员工**

```sql
0 1 2 3 4 5 6 7 8 9 -- 10名员工的下标

select ename,sal
from emp
order by sal desc
limit 5,5; -- 从第六名员工开始，也就是下标5；第六到第十长度为5
+--------+---------+
| ename  | sal     |
+--------+---------+
| CLARK  | 2450.00 |
| ALLEN  | 1600.00 |
| TURNER | 1500.00 |
| MILLER | 1300.00 |
| WARD   | 1250.00 |
+--------+---------+
```

## **11.取得最后入职的5名员工**

```sql
select ename,hiredate
from emp
order by hiredate desc -- 日期也可以排序
limit 5; -- 降序取前5行
+--------+------------+
| ename  | hiredate   |
+--------+------------+
| ADAMS  | 1987-05-23 |
| SCOTT  | 1987-04-19 |
| MILLER | 1982-01-23 |
| JAMES  | 1981-12-03 |
| FORD   | 1981-12-03 |
+--------+------------+
```

## **12.取得每个薪水等级有多少员工**

```sql
1.取得每个员工的薪水等级
select ename,grade
from emp e
join salgrade s
on e.sal between losal and hisal; -- 非等值连接
+--------+-------+
| ename  | grade |
+--------+-------+
| SMITH  |     1 |
| ALLEN  |     3 |
| WARD   |     2 |
| JONES  |     4 |
| MARTIN |     2 |
| BLAKE  |     4 |
| CLARK  |     4 |
| SCOTT  |     4 |
| KING   |     5 |
| TURNER |     3 |
| ADAMS  |     1 |
| JAMES  |     1 |
| FORD   |     4 |
| MILLER |     2 |
+--------+-------+
2.对薪水等级进行分组，并对每个组计数
select grade,count(*) as count_grade -- 对每个组的全部元组进行计数，用*即可
from emp e
join salgrade s
on e.sal between losal and hisal
group by grade
order by grade; -- 按等级升序
+-------+-------------+
| grade | count_grade |
+-------+-------------+
|     1 |           3 |
|     2 |           3 |
|     3 |           2 |
|     4 |           5 |
|     5 |           1 |
+-------+-------------+
```

## **13.面试题**

有 3 个表 **S(学生表)**，**C（课程表）**，**SC（学生选课表）**

**S**（SNO，SNAME）`代表`（学号，姓名） 

**C**（CNO，CNAME，CTEACHER）`代表`（课号，课名，教师）

**SC**（SNO，CNO，SCGRADE）`代表`（学号，课号，成绩）

**导入三张表**：

```sql
CREATE TABLE SC
(
 SNO VARCHAR(200),
 CNO VARCHAR(200),
 SCGRADE VARCHAR(200)
);
CREATE TABLE S
(
 SNO VARCHAR(200 ),
 SNAME VARCHAR(200)
);
CREATE TABLE C
(
 CNO VARCHAR(200),
 CNAME VARCHAR(200),
 CTEACHER VARCHAR(200)
);
INSERT INTO C ( CNO, CNAME, CTEACHER ) VALUES ( '1', '语文', '张'); 
INSERT INTO C ( CNO, CNAME, CTEACHER ) VALUES ( '2', '政治', '王'); 
INSERT INTO C ( CNO, CNAME, CTEACHER ) VALUES ( '3', '英语', '李'); 
INSERT INTO C ( CNO, CNAME, CTEACHER ) VALUES ( '4', '数学', '赵'); 
INSERT INTO C ( CNO, CNAME, CTEACHER ) VALUES ( '5', '物理', '黎明'); 
commit;
INSERT INTO S ( SNO, SNAME ) VALUES ( '1', '学生 1'); 
INSERT INTO S ( SNO, SNAME ) VALUES ( '2', '学生 2'); 
INSERT INTO S ( SNO, SNAME ) VALUES ( '3', '学生 3'); 
INSERT INTO S ( SNO, SNAME ) VALUES ( '4', '学生 4'); 
commit;
INSERT INTO SC ( SNO, CNO, SCGRADE ) VALUES ( '1', '1', '40'); 
INSERT INTO SC ( SNO, CNO, SCGRADE ) VALUES ( '1', '2', '30'); 
INSERT INTO SC ( SNO, CNO, SCGRADE ) VALUES ( '1', '3', '20'); 
INSERT INTO SC ( SNO, CNO, SCGRADE ) VALUES ( '1', '4', '80'); 
INSERT INTO SC ( SNO, CNO, SCGRADE ) VALUES ( '1', '5', '60'); 
INSERT INTO SC ( SNO, CNO, SCGRADE ) VALUES ( '2', '1', '60'); 
INSERT INTO SC ( SNO, CNO, SCGRADE ) VALUES ( '2', '2', '60'); 
INSERT INTO SC ( SNO, CNO, SCGRADE ) VALUES ( '2', '3', '60'); 
INSERT INTO SC ( SNO, CNO, SCGRADE ) VALUES ( '2', '4', '60'); 
INSERT INTO SC ( SNO, CNO, SCGRADE ) VALUES ( '2', '5', '40'); 
INSERT INTO SC ( SNO, CNO, SCGRADE ) VALUES ( '3', '1', '60'); 
INSERT INTO SC ( SNO, CNO, SCGRADE ) VALUES ( '3', '3', '80'); 
commit;
```

### **S表、C表、SC表**

```sql
S表：
+------+--------+
| SNO  | SNAME  |
+------+--------+
| 1    | 学生 1 |
| 2    | 学生 2 |
| 3    | 学生 3 |
| 4    | 学生 4 |
+------+--------+

C表：
+------+-------+----------+
| CNO  | CNAME | CTEACHER |
+------+-------+----------+
| 1    | 语文  | 张       |
| 2    | 政治  | 王       |
| 3    | 英语  | 李       |
| 4    | 数学  | 赵       |
| 5    | 物理  | 黎明     |
+------+-------+----------+

SC表：
+------+------+---------+
| SNO  | CNO  | SCGRADE |
+------+------+---------+
| 1    | 1    | 40      |
| 1    | 2    | 30      |
| 1    | 3    | 20      |
| 1    | 4    | 80      |
| 1    | 5    | 60      |
| 2    | 1    | 60      |
| 2    | 2    | 60      |
| 2    | 3    | 60      |
| 2    | 4    | 60      |
| 2    | 5    | 40      |
| 3    | 1    | 60      |
| 3    | 3    | 80      |
+------+------+---------+
```

### **问题 1.找出没选过黎明老师的所有学生姓名**

```sql
1.先取得黎明老师所教课程的课号
select cno
from c
where cteacher = '黎明';
+------+
| cno  |
+------+
| 5    |
+------+
2.取得所有选了黎明老师课程的同学
select distinct sno -- 去重
from sc
where cno = (select cno
              from c
              where cteacher = '黎明') ;
 +------+
| sno  |
+------+
| 1    |
| 2    |
+------+
3.哪位同学的学号不在第二步的查询结果当中，就说明该同学没有选黎明老师的课程
select distinct sname -- 去重
from s
left outer join sc -- 左外连接，将join左边的表看成主表，能够将s表中所有的数据都依次查询；能够查出学生4
on s.sno = sc.sno
where s.sno not in (select distinct sno
                  from sc
                  where cno = (select cno
                               from c
                               where cteacher = '黎明'));
+--------+
| sname  |
+--------+
| 学生 3 |
| 学生 4 |
+--------+
```

### **问题 2:列出 2 门以上（含 2 门）不及格学生姓名及平均成绩(巨难)**

```sql
1.取得不及格学生的学号
select sno
from sc
where scgrade < 60;
+------+
| sno  |
+------+
| 1    |
| 1    |
| 1    |
| 2    |
+------+
2.计算不及格学生的不及格科目数量
select sno,count(*) as nopass_number
from (select sno
      from sc
      where scgrade < 60) as t
group by t.sno;
+------+---------------+
| sno  | nopass_number |
+------+---------------+
| 1    |             3 |
| 2    |             1 |
+------+---------------+
3.将第二步的查询结果和s表相连，取得所要的学生姓名
select sname
from s
join (select sno,count(*) as nopass_number
      from (select sno
            from sc
            where scgrade < 60) as t
      group by t.sno) as q
on s.sno = q.sno
where nopass_number >= 2;
+--------+
| sname  |
+--------+
| 学生 1 |
+--------+
4.再连接一张sc表，计算所要学生的平均成绩
select sname,avg(scgrade) as avg_grade
from s
join (select sno,count(*) as nopass_number
      from (select sno
            from sc
            where scgrade < 60) as t
      group by t.sno) as q
on s.sno = q.sno
join sc
on s.sno = sc.sno
where nopass_number >= 2
group by s.sname; -- group by 要放在 where 后面
+--------+-----------+
| sname  | avg_grade |
+--------+-----------+
| 学生 1 |        46 |
+--------+-----------+
```

### **问题 3:既学过 1 号课程又学过 2 号课程所有学生的姓名**

```sql
SELECT DISTINCT sname -- 去重
FROM s
WHERE EXISTS (
    SELECT 1 -- 检查条件是否存在，而不关心具体返回的值是什么
    FROM sc
    WHERE sno = s.sno AND cno = 1)
  AND EXISTS (
    SELECT 1
    FROM sc
    WHERE sno = s.sno AND cno = 2);
+--------+
| sname  |
+--------+
| 学生 1 |
| 学生 2 |
+--------+
```

EXISTS命令解析：（chatgpt解答）

- `SELECT DISTINCT s.sname`: 这部分指定了要从数据库中返回的结果。`DISTINCT` 关键字用于确保返回的结果中不会包含重复的学生姓名。`s.sname` 表示从学生表 `s` 中选择学生姓名作为结果。
- `FROM s`: 这是查询的主要来源，它告诉数据库查询需要从哪个表中检索数据。在这里，我们从学生表 `s` 中检索数据。
- `WHERE EXISTS (...) AND EXISTS (...)`: 这是一个用 `EXISTS` 关键字组合的条件。它在每次查询中检查是否存在满足条件的记录，并根据其结果返回相应的行。
- `SELECT 1 FROM sc WHERE sno = s.sno AND cno = 1`: 这是第一个 `EXISTS` 子查询。它检查课程表 `sc` 中是否存在一行记录，其学生编号 (`sno`) 与学生表中当前学生的学生编号 (`s.sno`) 匹配，并且课程编号 (`cno`) 为 1。
- `SELECT 1 FROM sc WHERE sno = s.sno AND cno = 2`: 这是第二个 `EXISTS` 子查询，类似于第一个子查询，只不过检查的是课程编号为 2 的记录。
- `AND`: 这是一个逻辑运算符，表示两个条件都必须满足。换句话说，要返回学生的姓名，两个子查询都必须返回至少一行记录。
- 在 SQL 中，`SELECT 1` 是一个常见的用法，它的作用是在子查询中返回一个固定值 `1`。在这种情况下，它的实际作用是检查条件是否存在，而不关心具体返回的值是什么。因此，`SELECT 1` 可以用作条件是否满足的简单表示，而不会涉及到具体的数据。

## **14.列出所有员工及领导的姓名**

```sql
-- 自连接
select a.ename as '员工', b.ename as '领导'
from emp a
left join emp b -- 左外连接，将a表作为主表；将KING无上级的NULL也查出来。
on a.mgr = b.empno;
+--------+-------+
| 员工   | 领导  |
+--------+-------+
| SMITH  | FORD  |
| ALLEN  | BLAKE |
| WARD   | BLAKE |
| JONES  | KING  |
| MARTIN | BLAKE |
| BLAKE  | KING  |
| CLARK  | KING  |
| SCOTT  | JONES |
| KING   | NULL  |
| TURNER | BLAKE |
| ADAMS  | SCOTT |
| JAMES  | BLAKE |
| FORD   | JONES |
| MILLER | CLARK |
+--------+-------+
```

## **15.列出受雇日期早于其直接上级的所有员工的编号,姓名,部门名称**

```sql
-- 自连接
select a.empno,a.ename,dname
from emp a
join emp b
on a.mgr = b.empno
join dept d -- 再连接一张dept表
on a.deptno = d.deptno
where a.hiredate < b.hiredate; -- 查询条件
+-------+-------+------------+
| empno | ename | dname      |
+-------+-------+------------+
|  7369 | SMITH | RESEARCH   |
|  7499 | ALLEN | SALES      |
|  7521 | WARD  | SALES      |
|  7566 | JONES | RESEARCH   |
|  7698 | BLAKE | SALES      |
|  7782 | CLARK | ACCOUNTING |
+-------+-------+------------+
```

## **16.列出部门名称和这些部门的员工信息,同时列出那些没有员工的部门**

```sql
-- 自连接
select dname,e.*
from emp e
right join dept d -- 右外连接，将dept表作为主表；将没有员工的部门的NULL也查出来。
on e.deptno = d.deptno;
+------------+-------+--------+-----------+------+------------+---------+---------+--------+
| dname      | EMPNO | ENAME  | JOB       | MGR  | HIREDATE   | SAL     | COMM    | DEPTNO |
+------------+-------+--------+-----------+------+------------+---------+---------+--------+
| ACCOUNTING |  7934 | MILLER | CLERK     | 7782 | 1982-01-23 | 1300.00 |    NULL |     10 |
| ACCOUNTING |  7839 | KING   | PRESIDENT | NULL | 1981-11-17 | 5000.00 |    NULL |     10 |
| ACCOUNTING |  7782 | CLARK  | MANAGER   | 7839 | 1981-06-09 | 2450.00 |    NULL |     10 |
| RESEARCH   |  7902 | FORD   | ANALYST   | 7566 | 1981-12-03 | 3000.00 |    NULL |     20 |
| RESEARCH   |  7876 | ADAMS  | CLERK     | 7788 | 1987-05-23 | 1100.00 |    NULL |     20 |
| RESEARCH   |  7788 | SCOTT  | ANALYST   | 7566 | 1987-04-19 | 3000.00 |    NULL |     20 |
| RESEARCH   |  7566 | JONES  | MANAGER   | 7839 | 1981-04-02 | 2975.00 |    NULL |     20 |
| RESEARCH   |  7369 | SMITH  | CLERK     | 7902 | 1980-12-17 |  800.00 |    NULL |     20 |
| SALES      |  7900 | JAMES  | CLERK     | 7698 | 1981-12-03 |  950.00 |    NULL |     30 |
| SALES      |  7844 | TURNER | SALESMAN  | 7698 | 1981-09-08 | 1500.00 |    0.00 |     30 |
| SALES      |  7698 | BLAKE  | MANAGER   | 7839 | 1981-05-01 | 2850.00 |    NULL |     30 |
| SALES      |  7654 | MARTIN | SALESMAN  | 7698 | 1981-09-28 | 1250.00 | 1400.00 |     30 |
| SALES      |  7521 | WARD   | SALESMAN  | 7698 | 1981-02-22 | 1250.00 |  500.00 |     30 |
| SALES      |  7499 | ALLEN  | SALESMAN  | 7698 | 1981-02-20 | 1600.00 |  300.00 |     30 |
| OPERATIONS |  NULL | NULL   | NULL      | NULL | NULL       |    NULL |    NULL |   NULL |
+------------+-------+--------+-----------+------+------------+---------+---------+--------+
```

## **17.列出至少有5个员工的所有部门**

```sql
select dname,count(*) as count_emp
from emp e
join dept d -- 连接dept表，得到部门名
on e.deptno = d.deptno
group by dname -- 按部门名字分组，可以看成每一个部门都是一个组，都是一张表
having count(*) >= 5; -- 查询条件：每张表元组数大于等于5
+----------+-----------+
| dname    | count_emp |
+----------+-----------+
| RESEARCH |         5 |
| SALES    |         6 |
+----------+-----------+
```

## **18.列出薪资比"SMITH"多的所有员工信息**

```sql
1.先取得SIMTH的薪资
select sal
from emp
where ename = 'SMITH';
+--------+
| sal    |
+--------+
| 800.00 |
+--------+
2.查询比薪资第一步查询结果高的员工信息
select *
from emp
where sal > (select sal
             from emp
             where ename = 'SMITH');
+-------+--------+-----------+------+------------+---------+---------+--------+
| EMPNO | ENAME  | JOB       | MGR  | HIREDATE   | SAL     | COMM    | DEPTNO |
+-------+--------+-----------+------+------------+---------+---------+--------+
|  7499 | ALLEN  | SALESMAN  | 7698 | 1981-02-20 | 1600.00 |  300.00 |     30 |
|  7521 | WARD   | SALESMAN  | 7698 | 1981-02-22 | 1250.00 |  500.00 |     30 |
|  7566 | JONES  | MANAGER   | 7839 | 1981-04-02 | 2975.00 |    NULL |     20 |
|  7654 | MARTIN | SALESMAN  | 7698 | 1981-09-28 | 1250.00 | 1400.00 |     30 |
|  7698 | BLAKE  | MANAGER   | 7839 | 1981-05-01 | 2850.00 |    NULL |     30 |
|  7782 | CLARK  | MANAGER   | 7839 | 1981-06-09 | 2450.00 |    NULL |     10 |
|  7788 | SCOTT  | ANALYST   | 7566 | 1987-04-19 | 3000.00 |    NULL |     20 |
|  7839 | KING   | PRESIDENT | NULL | 1981-11-17 | 5000.00 |    NULL |     10 |
|  7844 | TURNER | SALESMAN  | 7698 | 1981-09-08 | 1500.00 |    0.00 |     30 |
|  7876 | ADAMS  | CLERK     | 7788 | 1987-05-23 | 1100.00 |    NULL |     20 |
|  7900 | JAMES  | CLERK     | 7698 | 1981-12-03 |  950.00 |    NULL |     30 |
|  7902 | FORD   | ANALYST   | 7566 | 1981-12-03 | 3000.00 |    NULL |     20 |
|  7934 | MILLER | CLERK     | 7782 | 1982-01-23 | 1300.00 |    NULL |     10 |
+-------+--------+-----------+------+------------+---------+---------+--------+
```

## **19.列出所有"CLERK"(办事员)的姓名及其部门名称,部门的人数**

```sql
1.取得职位为CLERK的员工姓名
select ename,deptno
from emp
where job = 'CLERK';
+--------+--------+
| ename  | deptno |
+--------+--------+
| SMITH  |     20 |
| ADAMS  |     20 |
| JAMES  |     30 |
| MILLER |     10 |
+--------+--------+
2.将第一步的查询结果当作新表t与dept表连接，取得部门名
select ename,dname
from dept d
join (select ename,deptno
      from emp
      where job = 'CLERK') as t
on d.deptno = t.deptno;
+--------+------------+
| ename  | dname      |
+--------+------------+
| SMITH  | RESEARCH   |
| ADAMS  | RESEARCH   |
| JAMES  | SALES      |
| MILLER | ACCOUNTING |
+--------+------------+
3.取得每个部门的员工人数
select deptno,count(*) as count_emp
from emp
group by deptno;
+--------+-----------+
| deptno | count_emp |
+--------+-----------+
|     20 |         5 |
|     30 |         6 |
|     10 |         3 |
+--------+-----------+
4.将第二步的查询结果与第三步的查询结果作为新表q连接
select ename,dname,count_emp
from dept d
join (select ename,deptno
      from emp
      where job = 'CLERK') as t
on d.deptno = t.deptno
join (select deptno,count(*) as count_emp
      from emp
      group by deptno) as q
on t.deptno = q.deptno;
+--------+------------+-----------+
| ename  | dname      | count_emp |
+--------+------------+-----------+
| SMITH  | RESEARCH   |         5 |
| ADAMS  | RESEARCH   |         5 |
| JAMES  | SALES      |         6 |
| MILLER | ACCOUNTING |         3 |
+--------+------------+-----------+
```

## **20.列出最低薪资大于1500的各种工作及从事此工作的全部雇员人数**

```sql
1.取得每个部门的最低薪资
select job,min(sal) as min_sal
from emp
group by job;
+-----------+---------+
| job       | min_sal |
+-----------+---------+
| CLERK     |  800.00 |
| SALESMAN  | 1250.00 |
| MANAGER   | 2450.00 |
| ANALYST   | 3000.00 |
| PRESIDENT | 5000.00 |
+-----------+---------+
2.取得最低薪资大于1500的工作
select job,min(sal) as min_sal
from emp
group by job
having min_sal > 1500;
+-----------+---------+
| job       | min_sal |
+-----------+---------+
| MANAGER   | 2450.00 |
| ANALYST   | 3000.00 |
| PRESIDENT | 5000.00 |
+-----------+---------+
3.取得每份工作的雇员人数
select job,count(*) as count_emp
from emp
group by job;
+-----------+-----------+
| job       | count_emp |
+-----------+-----------+
| CLERK     |         4 |
| SALESMAN  |         4 |
| MANAGER   |         3 |
| ANALYST   |         2 |
| PRESIDENT |         1 |
+-----------+-----------+
4.将第二步的查询结果与第三步的查询结果作为新表t连接
select e.job,min(sal) as min_sal,count_emp
from emp e
join (select job,count(*) as count_emp
      from emp
      group by job) as t
on e.job = t.job
group by e.job
having min_sal > 1500;
+-----------+---------+-----------+
| job       | min_sal | count_emp |
+-----------+---------+-----------+
| MANAGER   | 2450.00 |         3 |
| ANALYST   | 3000.00 |         2 |
| PRESIDENT | 5000.00 |         1 |
+-----------+---------+-----------+
```

## **21.列出在部门"SALES"<销售部>工作的员工的姓名,假定不知道销售部的部门编号**

```sql
1.一开始不知道销售部的部门编号，所以要查询销售部的部门编号
select deptno
from dept
where dname = "SALES";
+--------+
| deptno |
+--------+
|     30 |
+--------+
2.经过第一步的查询结果后，已经知道销售部的部门编号，接下来直接查就可以了
select ename
from emp
where deptno = (select deptno
                from dept
                where dname = "SALES");
+--------+
| ename  |
+--------+
| ALLEN  |
| WARD   |
| MARTIN |
| BLAKE  |
| TURNER |
| JAMES  |
+--------+                
```

## **22.列出薪金高于公司平均薪金的所有员工,所在部门名称,上级领导名称,雇员的工资等级**

```sql
1.取得公司的平均薪资
select avg(sal) as avg_sal
from emp;
+-------------+
| avg_sal     |
+-------------+
| 2073.214286 |
+-------------+
2.连接需要的表
select a.ename as '员工',dname as '所在部门',b.ename as '上级领导',grade as '工资等级'
from emp a
join dept d
on a.deptno = d.deptno
join emp b
on a.mgr = b.empno
join salgrade
on a.sal between losal and hisal;
+--------+------------+----------+----------+
| 员工   | 所在部门   | 上级领导 | 工资等级 |
+--------+------------+----------+----------+
| SMITH  | RESEARCH   | FORD     |        1 |
| ALLEN  | SALES      | BLAKE    |        3 |
| WARD   | SALES      | BLAKE    |        2 |
| JONES  | RESEARCH   | KING     |        4 |
| MARTIN | SALES      | BLAKE    |        2 |
| BLAKE  | SALES      | KING     |        4 |
| CLARK  | ACCOUNTING | KING     |        4 |
| SCOTT  | RESEARCH   | JONES    |        4 |
| TURNER | SALES      | BLAKE    |        3 |
| ADAMS  | RESEARCH   | SCOTT    |        1 |
| JAMES  | SALES      | BLAKE    |        1 |
| FORD   | RESEARCH   | JONES    |        4 |
| MILLER | ACCOUNTING | CLARK    |        2 |
+--------+------------+----------+----------+
注意到员工一栏没有KING，所以需要使用外连接：
select a.ename as '员工',dname as '所在部门',b.ename as '上级领导',grade as '工资等级'
from emp a
join dept d
on a.deptno = d.deptno
left join emp b
on a.mgr = b.empno
join salgrade
on a.sal between losal and hisal;
+--------+------------+----------+----------+
| 员工   | 所在部门   | 上级领导 | 工资等级 |
+--------+------------+----------+----------+
| SMITH  | RESEARCH   | FORD     |        1 |
| ALLEN  | SALES      | BLAKE    |        3 |
| WARD   | SALES      | BLAKE    |        2 |
| JONES  | RESEARCH   | KING     |        4 |
| MARTIN | SALES      | BLAKE    |        2 |
| BLAKE  | SALES      | KING     |        4 |
| CLARK  | ACCOUNTING | KING     |        4 |
| SCOTT  | RESEARCH   | JONES    |        4 |
| KING   | ACCOUNTING | NULL     |        5 | -- 取得KING的信息
| TURNER | SALES      | BLAKE    |        3 |
| ADAMS  | RESEARCH   | SCOTT    |        1 |
| JAMES  | SALES      | BLAKE    |        1 |
| FORD   | RESEARCH   | JONES    |        4 |
| MILLER | ACCOUNTING | CLARK    |        2 |
+--------+------------+----------+----------+
3.基于第二步的查询结果，筛选薪资大于公司平均薪资的元组
select a.ename as '员工',dname as '所在部门',b.ename as '上级领导',grade as '工资等级'
from emp a
join dept d
on a.deptno = d.deptno
left join emp b
on a.mgr = b.empno
join salgrade
on a.sal between losal and hisal
where a.sal > (select avg(sal) as avg_sal
             from emp);
+-------+------------+----------+----------+
| 员工  | 所在部门   | 上级领导 | 工资等级 |
+-------+------------+----------+----------+
| FORD  | RESEARCH   | JONES    |        4 |
| SCOTT | RESEARCH   | JONES    |        4 |
| CLARK | ACCOUNTING | KING     |        4 |
| BLAKE | SALES      | KING     |        4 |
| JONES | RESEARCH   | KING     |        4 |
| KING  | ACCOUNTING | NULL     |        5 |
+-------+------------+----------+----------+             
```

## **23.列出与"SCOTT"从事相同工作的其他所有员工及其所在部门的名称**

```sql
1.查询"SCOTT"的工作
select job
from emp
where ename = 'SCOTT';
+---------+
| job     |
+---------+
| ANALYST |
+---------+
2.将emp表和dept表连接
select ename,dname
from emp e
join dept d
on e.deptno = d.deptno;
+--------+------------+
| ename  | dname      |
+--------+------------+
| SMITH  | RESEARCH   |
| ALLEN  | SALES      |
| WARD   | SALES      |
| JONES  | RESEARCH   |
| MARTIN | SALES      |
| BLAKE  | SALES      |
| CLARK  | ACCOUNTING |
| SCOTT  | RESEARCH   |
| KING   | ACCOUNTING |
| TURNER | SALES      |
| ADAMS  | RESEARCH   |
| JAMES  | SALES      |
| FORD   | RESEARCH   |
| MILLER | ACCOUNTING |
+--------+------------+
3.筛选工作位第一步查询结果的员工
select ename,dname
from emp e
join dept d
on e.deptno = d.deptno
where job = (select job
             from emp
             where ename = 'SCOTT');
+-------+----------+
| ename | dname    |
+-------+----------+
| SCOTT | RESEARCH |
| FORD  | RESEARCH |
+-------+----------+
注意到查询结果有'SCOTT',把他剔除
select ename,dname
from emp e
join dept d
on e.deptno = d.deptno
where job = (select job
             from emp
             where ename = 'SCOTT')
  and ename <> 'SCOTT'; -- 剔除条件
+-------+----------+
| ename | dname    |
+-------+----------+
| FORD  | RESEARCH |
+-------+----------+
```

## **24.列出薪资等于部门30中员工的薪资的其他员工的姓名和薪资**

```sql
1.查询部门30中员工的薪资
select sal
from emp
where deptno = '30';
+---------+
| sal     |
+---------+
| 1600.00 |
| 1250.00 |
| 1250.00 |
| 2850.00 |
| 1500.00 |
|  950.00 |
+---------+
2.查询其他薪资等于第一步查询结果的员工
select ename,sal
from emp
where sal in (select sal
              from emp
              where deptno = '30')
  and deptno <> 30; -- 剔除部门30的员工

查询结果：Empty set 
```

## **25.列出薪资高于在部门30工作的所有员工的薪资的员工姓名和薪资和所在部门的名称**

```sql
1.查询部门30的员工薪资
select sal
from emp
where deptno = '30';
+---------+
| sal     |
+---------+
| 1600.00 |
| 1250.00 |
| 1250.00 |
| 2850.00 |
| 1500.00 |
|  950.00 |
+---------+
2.因为要高于所有员工，所以比max(sal)还要高,故先要查询到max(sal)
select max(sal) as max_sal
from emp
where deptno = '30';
+---------+
| max_sal |
+---------+
| 2850.00 |
+---------+
3.将emp表和dept表连接
select ename,dname
from emp e
join dept d
on e.deptno = d.deptno;
+--------+------------+
| ename  | dname      |
+--------+------------+
| SMITH  | RESEARCH   |
| ALLEN  | SALES      |
| WARD   | SALES      |
| JONES  | RESEARCH   |
| MARTIN | SALES      |
| BLAKE  | SALES      |
| CLARK  | ACCOUNTING |
| SCOTT  | RESEARCH   |
| KING   | ACCOUNTING |
| TURNER | SALES      |
| ADAMS  | RESEARCH   |
| JAMES  | SALES      |
| FORD   | RESEARCH   |
| MILLER | ACCOUNTING |
+--------+------------+
4.基于第三步的查询结果，筛选出薪资大于部门30最高薪资的员工
select ename,sal,dname
from emp e
join dept d
on e.deptno = d.deptno
where sal > (select max(sal) as max_sal
             from emp
             where deptno = '30');
+-------+---------+------------+
| ename | sal     | dname      |
+-------+---------+------------+
| JONES | 2975.00 | RESEARCH   |
| SCOTT | 3000.00 | RESEARCH   |
| KING  | 5000.00 | ACCOUNTING |
| FORD  | 3000.00 | RESEARCH   |
+-------+---------+------------+             
```

## **26.列出在每个部门工作的员工数量,平均工资和平均服务期限**

```sql
1.查询每个部门的员工数量（其实还存在着一个没有员工的40部门）
select d.deptno,count(ename) as count_emp -- count()条件改变为员工名
from emp e
right join dept d -- 使用右外连接，将dept表看作主表；能够查出40部门
on e.deptno = d.deptno
group by deptno;
+--------+-----------+
| deptno | count_emp |
+--------+-----------+
|     10 |         3 |
|     20 |         5 |
|     30 |         6 |
|     40 |         0 |
+--------+-----------+
2.基于第一步的查询结果，查询每个部门的平均工资
select d.deptno,count(ename) as count_emp,ifnull(avg(sal),0) as avg_sal
from emp e
right join dept d 
on e.deptno = d.deptno
group by deptno;
+--------+-----------+-------------+
| deptno | count_emp | avg_sal     |
+--------+-----------+-------------+
|     10 |         3 | 2916.666667 |
|     20 |         5 | 2175.000000 |
|     30 |         6 | 1566.666667 |
|     40 |         0 |    0.000000 |
+--------+-----------+-------------+
3.基于第二步的查询结果，查询每个部门的平均服务期限
select d.deptno,count(ename) as count_emp,ifnull(avg(sal),0) as avg_sal,
       ifnull(avg(timestampdiff(YEAR, hiredate, now())), 0) as avg_servicetime -- 服务时间
from emp e
right join dept d 
on e.deptno = d.deptno
group by deptno;
+--------+-----------+-------------+-----------------+
| deptno | count_emp | avg_sal     | avg_servicetime |
+--------+-----------+-------------+-----------------+
|     10 |         3 | 2916.666667 |         42.0000 |
|     20 |         5 | 2175.000000 |         40.0000 |
|     30 |         6 | 1566.666667 |         42.3333 |
|     40 |         0 |    0.000000 |          0.0000 |
+--------+-----------+-------------+-----------------+
```

计算两个日期的“年差”，差了多少年？
	

TimeStampDiff(间隔类型, 前一个日期, 后一个日期)
	

例如：timestampdiff(YEAR, hiredate, now())

**间隔类型**：
	

SECOND   秒
	

MINUTE   分钟
	

HOUR   小时
	

DAY   天

WEEK   星期
	

MONTH   月
	

QUARTER   季度
	

YEAR   年

------

## **27.列出所有员工的姓名、部门名称和工资**

```sql
select ename,dname,sal
from emp e
join dept d
on e.deptno = d.deptno;
+--------+------------+---------+
| ename  | dname      | sal     |
+--------+------------+---------+
| SMITH  | RESEARCH   |  800.00 |
| ALLEN  | SALES      | 1600.00 |
| WARD   | SALES      | 1250.00 |
| JONES  | RESEARCH   | 2975.00 |
| MARTIN | SALES      | 1250.00 |
| BLAKE  | SALES      | 2850.00 |
| CLARK  | ACCOUNTING | 2450.00 |
| SCOTT  | RESEARCH   | 3000.00 |
| KING   | ACCOUNTING | 5000.00 |
| TURNER | SALES      | 1500.00 |
| ADAMS  | RESEARCH   | 1100.00 |
| JAMES  | SALES      |  950.00 |
| FORD   | RESEARCH   | 3000.00 |
| MILLER | ACCOUNTING | 1300.00 |
+--------+------------+---------+
```

## **28.列出所有部门的详细信息和人数**

```sql
select d.deptno,d.dname,d.loc,count(ename) as count_emp
from emp e
right join dept d -- 右外连接，为了查出部门40
on e.deptno = d.deptno
group by d.deptno,d.dname,d.loc; -- 因为要取得部门的所有信息，所以将dept表的所有字段都分组
+--------+------------+----------+-----------+ -- select后只能跟进行分组的字段和分组函数
| deptno | dname      | loc      | count_emp |
+--------+------------+----------+-----------+
|     10 | ACCOUNTING | NEW YORK |         3 |
|     20 | RESEARCH   | DALLAS   |         5 |
|     30 | SALES      | CHICAGO  |         6 |
|     40 | OPERATIONS | BOSTON   |         0 |
+--------+------------+----------+-----------+
```

## **29.列出各种工作的最低工资以及对应的雇员姓名**

```sql
1.查询每种工作的最低薪资
select job,min(sal) as min_sal
from emp
group by job;
+-----------+---------+
| job       | min_sal |
+-----------+---------+
| CLERK     |  800.00 |
| SALESMAN  | 1250.00 |
| MANAGER   | 2450.00 |
| ANALYST   | 3000.00 |
| PRESIDENT | 5000.00 |
+-----------+---------+
2.将第一步的查询结果作为新表t与emp表连接
select t.job,t.min_sal as min_sal,e.ename
from emp e
join (select job,min(sal) as min_sal
      from emp
      group by job) as t
on e.job = t.job and e.sal =t.min_sal; -- 表连接兼筛选的条件
+-----------+---------+--------+
| job       | min_sal | ename  |
+-----------+---------+--------+
| CLERK     |  800.00 | SMITH  |
| SALESMAN  | 1250.00 | WARD   |
| SALESMAN  | 1250.00 | MARTIN |
| MANAGER   | 2450.00 | CLARK  |
| ANALYST   | 3000.00 | SCOTT  |
| PRESIDENT | 5000.00 | KING   |
| ANALYST   | 3000.00 | FORD   |
+-----------+---------+--------+
```

## **30.列出各个部门的MANAGER(领导)的最低薪资**

```sql
select deptno,min(sal) as min_sal
from emp
where job = 'MANAGER'
group by deptno;
+--------+---------+
| deptno | min_sal |
+--------+---------+
|     20 | 2975.00 |
|     30 | 2850.00 |
|     10 | 2450.00 |
+--------+---------+
```

## **31.列出所有员工的年薪,按年薪从低到高排序**

```sql
select ename,(sal+ifnull(comm,0))*12 as year_sal -- 年薪=（月工资+津贴）*12
from emp
order by year_sal;
+--------+----------+
| ename  | year_sal |
+--------+----------+
| SMITH  |  9600.00 |
| JAMES  | 11400.00 |
| ADAMS  | 13200.00 |
| MILLER | 15600.00 |
| TURNER | 18000.00 |
| WARD   | 21000.00 |
| ALLEN  | 22800.00 |
| CLARK  | 29400.00 |
| MARTIN | 31800.00 |
| BLAKE  | 34200.00 |
| JONES  | 35700.00 |
| SCOTT  | 36000.00 |
| FORD   | 36000.00 |
| KING   | 60000.00 |
+--------+----------+
```

## **32.求出员工领导的薪水超过3000的员工名称和他的领导名称**

```sql
emp表自连接
select a.ename,b.ename
from emp a -- 员工表
join emp b -- 领导表
on a.mgr = b.empno
where b.sal > 3000;
+-------+-------+
| ename | ename |
+-------+-------+
| JONES | KING  |
| BLAKE | KING  |
| CLARK | KING  |
+-------+-------+
```

**33.求出部门名称中带'S'字符的部门员工的工资合计、部门人数**

```sql
-- 模糊查询
select dname,ifnull(sum(sal),0) as sum_sal,count(ename) as count_emp
from emp e
right join dept d -- 右外连接，为了查出40部门
on  e.deptno = d.deptno
where dname like '%S%'
group by dname;
+------------+----------+-----------+
| dname      | sum_sal  | count_emp |
+------------+----------+-----------+
| RESEARCH   | 10875.00 |         5 |
| SALES      |  9400.00 |         6 |
| OPERATIONS |     0.00 |         0 |
+------------+----------+-----------+
```

## **34.给任职日期超过30年的员工加薪10%**

```sql
update emp  -- 修改emp表
set sal = sal * 1.1 
where timestampdiff(YEAR, hiredate, now()) > 30; -- 工作年龄

 修改前：
 +-------+--------+-----------+------+------------+---------+---------+--------+
| EMPNO | ENAME  | JOB       | MGR  | HIREDATE   | SAL     | COMM    | DEPTNO |
+-------+--------+-----------+------+------------+---------+---------+--------+
|  7369 | SMITH  | CLERK     | 7902 | 1980-12-17 |  800.00 |    NULL |     20 |
|  7499 | ALLEN  | SALESMAN  | 7698 | 1981-02-20 | 1600.00 |  300.00 |     30 |
|  7521 | WARD   | SALESMAN  | 7698 | 1981-02-22 | 1250.00 |  500.00 |     30 |
|  7566 | JONES  | MANAGER   | 7839 | 1981-04-02 | 2975.00 |    NULL |     20 |
|  7654 | MARTIN | SALESMAN  | 7698 | 1981-09-28 | 1250.00 | 1400.00 |     30 |
|  7698 | BLAKE  | MANAGER   | 7839 | 1981-05-01 | 2850.00 |    NULL |     30 |
|  7782 | CLARK  | MANAGER   | 7839 | 1981-06-09 | 2450.00 |    NULL |     10 |
|  7788 | SCOTT  | ANALYST   | 7566 | 1987-04-19 | 3000.00 |    NULL |     20 |
|  7839 | KING   | PRESIDENT | NULL | 1981-11-17 | 5000.00 |    NULL |     10 |
|  7844 | TURNER | SALESMAN  | 7698 | 1981-09-08 | 1500.00 |    0.00 |     30 |
|  7876 | ADAMS  | CLERK     | 7788 | 1987-05-23 | 1100.00 |    NULL |     20 |
|  7900 | JAMES  | CLERK     | 7698 | 1981-12-03 |  950.00 |    NULL |     30 |
|  7902 | FORD   | ANALYST   | 7566 | 1981-12-03 | 3000.00 |    NULL |     20 |
|  7934 | MILLER | CLERK     | 7782 | 1982-01-23 | 1300.00 |    NULL |     10 |
+-------+--------+-----------+------+------------+---------+---------+--------+
修改后：
+-------+--------+-----------+------+------------+---------+---------+--------+
| EMPNO | ENAME  | JOB       | MGR  | HIREDATE   | SAL     | COMM    | DEPTNO |
+-------+--------+-----------+------+------------+---------+---------+--------+
|  7369 | SMITH  | CLERK     | 7902 | 1980-12-17 |  880.00 |    NULL |     20 |
|  7499 | ALLEN  | SALESMAN  | 7698 | 1981-02-20 | 1760.00 |  300.00 |     30 |
|  7521 | WARD   | SALESMAN  | 7698 | 1981-02-22 | 1375.00 |  500.00 |     30 |
|  7566 | JONES  | MANAGER   | 7839 | 1981-04-02 | 3272.50 |    NULL |     20 |
|  7654 | MARTIN | SALESMAN  | 7698 | 1981-09-28 | 1375.00 | 1400.00 |     30 |
|  7698 | BLAKE  | MANAGER   | 7839 | 1981-05-01 | 3135.00 |    NULL |     30 |
|  7782 | CLARK  | MANAGER   | 7839 | 1981-06-09 | 2695.00 |    NULL |     10 |
|  7788 | SCOTT  | ANALYST   | 7566 | 1987-04-19 | 3300.00 |    NULL |     20 |
|  7839 | KING   | PRESIDENT | NULL | 1981-11-17 | 5500.00 |    NULL |     10 |
|  7844 | TURNER | SALESMAN  | 7698 | 1981-09-08 | 1650.00 |    0.00 |     30 |
|  7876 | ADAMS  | CLERK     | 7788 | 1987-05-23 | 1210.00 |    NULL |     20 |
|  7900 | JAMES  | CLERK     | 7698 | 1981-12-03 | 1045.00 |    NULL |     30 |
|  7902 | FORD   | ANALYST   | 7566 | 1981-12-03 | 3300.00 |    NULL |     20 |
|  7934 | MILLER | CLERK     | 7782 | 1982-01-23 | 1430.00 |    NULL |     10 |
+-------+--------+-----------+------+------------+---------+---------+--------+
```

------

34道MySQL查询练习题终于做完，从一开始的生疏到后来的得心应手，亲手实际果然是提高编程能力的最快途径！

——2024/4/3

