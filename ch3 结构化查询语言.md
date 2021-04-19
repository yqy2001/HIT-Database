## 3.1 SQL数据定义

数据类型

创建关系模式

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

增加主键：

```sql
alter table student add primary key (Snun);
```



定义关系模式，包括关系名、属性名、属性类型、主键、外键、完整性约束等

## 3.3 SQL数据查询

### 单关系查询

SELECT 属性名列表 FROM 关系名 WHERE 选择条件

空值判断：属性名 IS NULL

查询语句1 EXCEPT 查询语句2

### 连接查询

内连接 SELECT FROM A JOIN B

### 嵌套查询