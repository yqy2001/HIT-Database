## 3.1 SQL数据定义

数据类型

### 创建关系模式

CREATE TABLE

```sql
create table student(
    Snum char(5) primary key,
    Sname varchar(10),
    Ssex enum('M', 'F'),
    Sage int,
    Dnum char(5),
    Sd date
);
```

增加主键：`primary key (Sno)`

```sql
alter table student add primary key (Snun);
```

声明外键：

```sql
FOREIGN key (Sno) REFERENCES Student(Sno);
```

声明用户定义完整性约束：

not null, unique, auto_increment, default, check

删除关系：DROP TABLE 关系1，关系2，……，关系n；

定义关系模式，包括关系名、属性名、属性类型、主键、外键、完整性约束等

## 3.2 SQL数据更新

插入元组：INSERT INTO 关系名 (属性1, 属性2, …, 属性n) VALUES (表达式1, …, 表达式n)；

数据修改：UPDATE，数据删除：DELETE

数据修改时要对数据完整性进行检查：实体完整性、参照完整性、用户定义完整性

## 3.3 SQL数据查询

### 单关系查询

SELECT 属性名列表 FROM 关系名 WHERE 选择条件

空值判断：属性名 IS [NOT] NULL

查询语句1 EXCEPT 查询语句2

集合操作：UNION、INTERSECT、MINUS/EXCEPT

查询结果排序：在查询语句后面加上ORDER BY 属性名[ASC|DESC]；限制查询结果数量用LIMIT

聚集查询：聚集函数不能出现在WHERE子句中，因为聚集函数实质上是作用于一个集合；
分组查询GROUP BY
HAVING条件对分组进行筛选

### 连接查询

NATURAL JOIN是同名属性的等值连接

内连接 SELECT FROM A JOIN B

### 嵌套查询

EXISTS可以实现全称量词功能，转换为没有没有，两个NOT EXISTS

若子查询的结果作为派生关系放在FROM语句中，必须重命名