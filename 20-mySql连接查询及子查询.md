# 子查询

- 查询支持嵌套使用

### 什么是子查询

 当一个查询是另一个查询的条件时,这个查询称之为子查询(内层查询)

 什么时候用？

 当查询需求比较复杂，一次性查询无法得到结果，需要多次查询时，

 例如：给出一个部门名称，需要获得该部门所有的员工信息

 分析：

 1.需要先确定部门的id

 2.然后才能通过id确定员工

 解决问题的方式是把一个复杂的问题拆分为若干个简单的问题

###### 2. 如何使用？

首先明确子查询就是一个普通的查询,当一个查询需要作为子查询使用时,用括号包裹即可

###### 3. 需要注意

 in中的子查询只能包含一个列

 例如：查询财务部有哪些人

 正确的写法：select name from emp where dept_id in (select id from dept where name = "财务");

 错误的写法：select name from emp where dept_id in (select * from dept where name = "财务");

#### 关键字：exists

exists后跟子查询，子查询有结果是为True，没有结果时为False。为True时外层执行，为False外层不执行

##### 如何使用？

select *from emp where exists (select* from emp where salary > 1000);

前面 exists 后面 如果 *后面* 查询有结果时，*前面* 才会执行



# 连接查询

- 问：查询每个学生每个科目的分数
- 分析：学生姓名来源于students表，科目名称来源于subjects，分数来源于scores表，怎么将3个表放到一起查询，并将结果显示在同一个结果集中呢？
- 答：当查询结果来源于多张表时，需要使用连接查询
- 关键：找到表间的关系，当前的关系是
  - students表的id---scores表的stuid
  - subjects表的id---scores表的subid
- 则上面问题的答案是：

```
select students.sname,subjects.stitle,scores.score
from scores
inner join students on scores.stuid=students.id
inner join subjects on scores.subid=subjects.id;
```

- 结论：当需要对有关系的多张表进行查询时，需要使用连接join

# 连接查询

- 连接查询分类如下：
  - 表A inner join 表B：表A与表B匹配的行会出现在结果中
  - 表A left join 表B：表A与表B匹配的行会出现在结果中，外加表A中独有的数据，未对应的数据使用null填充
  - 表A right join 表B：表A与表B匹配的行会出现在结果中，外加表B中独有的数据，未对应的数据使用null填充
- 在查询或条件中推荐使用“表名.列名”的语法
- 如果多个表中列名不重复可以省略“表名.”部分
- 如果表的名称太长，可以在表名后面使用' as 简写名'或' 简写名'，为表起个临时的简写名称

# 练习

- 查询学生的姓名、平均分

```
select students.sname,avg(scores.score)
from scores
inner join students on scores.stuid=students.id
group by students.sname;
```

- 查询男生的姓名、总分

```
select students.sname,avg(scores.score)
from scores
inner join students on scores.stuid=students.id
where students.gender=1
group by students.sname;
```

- 查询科目的名称、平均分

```
select subjects.stitle,avg(scores.score)
from scores
inner join subjects on scores.subid=subjects.id
group by subjects.stitle;
```

- 查询未删除科目的名称、最高分、平均分

```
select subjects.stitle,avg(scores.score),max(scores.score)
from scores
inner join subjects on scores.subid=subjects.id
where subjects.isdelete=0
group by subjects.stitle;
```