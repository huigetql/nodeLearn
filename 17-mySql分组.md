# 分组

- 按照字段分组，表示此字段相同的数据会被放到一个组中
- 分组后，只能查询出相同的数据列，对于有差异的数据列无法出现在结果集中
- 可以对分组后的数据进行统计，做聚合运算
- 语法：

```
select 列1,列2,聚合... from 表名 group by 列1,列2,列3...
```

- 查询男女生总数

```
select gender as 性别,count(*)
from students
group by gender;
```

- 查询各城市人数

```
select hometown as 家乡,count(*)
from students
group by hometown;
```

#### 分组后的数据筛选

- 语法：

```
select 列1,列2,聚合... from 表名
group by 列1,列2,列3...
having 列1,...聚合...
```

- having后面的条件运算符与where的相同
- 查询男生总人数

```
方案一
select count(*)
from students
where gender=1;
-----------------------------------
方案二：
select gender as 性别,count(*)
from students
group by gender
having gender=1;
```

#### 对比where与having

- where是对from后面指定的表进行数据筛选，属于对原始数据的筛选
- having是对group by的结果进行筛选

 