# 聚合

- 为了快速得到统计数据，提供了5个聚合函数
- count(*)表示计算总行数，括号中写星与列名，结果是相同的
- 查询学生总数

```
select count(*) from students;
```

- max(列)表示求此列的最大值
- 查询女生的编号最大值

```
select max(id) from students where gender=0;
```

- min(列)表示求此列的最小值
- 查询未删除的学生最小编号

```
select min(id) from students where isdelete=0;
```

- sum(列)表示求此列的和
- 查询男生的编号之和

```
select sum(id) from students where gender=1;
```

- avg(列)表示求此列的平均值
- 查询未删除女生的编号平均值

```
select avg(id) from students where isdelete=0 and gender=0;
```