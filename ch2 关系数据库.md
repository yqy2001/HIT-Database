# ch2 关系数据库

## 1 Relational Data Model

一种被广泛使用的实现数据模型，是众多关系数据库管理系统的模型基础。

三要素：关系数据结构、关系操作、关系完整性约束

### 1.1 关系数据结构：

唯一的数据结构：关系（二维表）

* 行—**元组**/记录，表示对象
* 列—**属性**/域，表示对象的性质

关系的定义：$D_1,D_2,\dots,D_n$是n个值域，$D_1\times D_2\times \dots \times D_n$的子集R称作$D_1,D_2,\dots,D_n$上的**关系**，记作$R(D_1,D_2,\dots,D_n)$。R是关系名，n是度，$(d_1,d_2,\dots,d_n)\in R$是关系R的元组，其中d~i~是元组的分量

![image-20210314180516435](https://i.loli.net/2021/03/14/emsQ6LK5rGF3fBv.png)

关系的正确性：
值域的笛卡尔积的任意子集都是关系，但只有符合客观实际的关系才是正确的关系。例如一个人不能有两个年龄

关系的属性：
由于值域可能相同，为了加以区分，为每个域$D_i$起一个不同的名字$A_i$，称作**属性**。

![image-20210314185654312](https://i.loli.net/2021/03/14/796K8XoaJqd5fCw.png)

**<font color='cornflowerblue'>关系的键：</font>**
关系的某些**属性集合**可以区分不同的元组，称作键。**键和超键有区别吗？**

若关系的某一组属性的值能**唯一**标识每个元组，则称该组属性为**超键**。

若一个超键的任意真子集都不是超键，则称其为**候选键**，即为极小的超键。可能有多组候选键，人为指定一个候选键作为**主键**。

**外键：**
不同关系中的元组通过外键建立联系。
F是关系R的属性子集，若F与关系S的主键K相对应，则F是R的外键，R是参照关系，S是被参照关系，外键参照主键。**R和S可以是同一关系**。
外键可以参照自己的主键，比如说班长这个外键

### 1.2 关系操作

查询操作：从关系数据库中查找数据；
更新操作：对关系数据库进行更新，插入、修改、删除；

查询语言是用于表示关系操作的语言。查询语言的类型：关系代数、关系演算、结构化查询语言SQL

### 1.3 关系完整性约束

关系数据库中所有数据必须满足的约束条件。

**实体完整性：**关系中任意元组的主键值必须唯一，关系中任意元组在主键中的属性值非空

**参照完整性约束：**

外键F必须满足以下两个条件之一：1、F的值为空；2、若F的值不为空，则F的值必须在S中存在。

**用户定义完整性约束：**

根据用户需求定义的完整性约束条件，例如考试成绩必须在0-100之间，性别必须为‘M’或‘F’。

### 关系的模式与实例：

模式是对关系的结构与语义的描述（前面的所有），实例是关系在某一时刻的取值

## 2 关系代数

使用关系代数操作表达式来查询的语言。其明确地给出了查询的执行过程（顺序）。

操作数是关系，操作结果是关系，即输入的是表，输出的也是表。

### 基本关系代数操作：

选择、投影、并、差、笛卡尔积、重命名

> “你们咏春就三板斧”，“三板斧就够你受的了”——形容基本关系代数操作的强大

选择：$\sigma_\theta(R)$，$\theta$是逻辑表达式

投影：$\Pi_L(R)$，从一个关系中选出指定的列，并去掉重复元组

并：$R\cup S$，要求R和S必须具有相同个数的属性，对应属性的值域必须相容

差：$R-S$，R中有但S中没有的元素，和并的要求相同

笛卡尔积：$R\times S$计算两个关系的笛卡尔积。其仅仅是将R和S中的元组无条件地连接起来，无意义，通常和选择操作一起使用（连接）。

![image-20210314200112990](https://i.loli.net/2021/03/14/dGLznFDXAHfsJNk.png)

重命名操作：$\rho_{B\leftarrow A}(R)$修改关系名、属性名。一个关系进行自连接时，需要使用重命名来区分同一关系的两个副本

### 派生关系代数操作：

为了方便

目的：为了简化查询编写，任何一项派生关系代数操作都可以用**基本关系代数操作来表示**。

交：计算R和S的交集，$R\cap S=R-(R-S)$，要求R和S必须具有相同个数的属性，对应属性的值域必须相容。

$\theta$连接$\Join_\theta$：$\theta$是连接条件，语法和选择操作相同。$R\Join_\theta S$的结果包含R和S中的**全部属性**，同名属性加关系前缀。连接条件仅涉及相等比较的连接称作**等值连接**。

自然连接$\Join$：默认条件：在同名属性上做等值连接，并从连接结果中去掉重复的同名属性。这个用的最多，一般将主外键连接，且习惯上主外键一般同名。

前两个连接都是内连接，内连接无法找出**不符合条件**的元组，例如未选课的人。

外连接：
左外连接$R\ ⟕_\theta\ S$：首先将R和S中满足条件$\theta$的元组进行连接，再对于R中不满足给定连接条件的元组，左外连接的结果中也包含该元组，只不过S中的属性值都为空。
右外连接同理，全外连接等于左并右

除：
针对这种查询：找出选修了所有课程的学生
$R / S$的结果是一个关系，它只包含R中的属性，不包含S中的属性，$R / S$的结果是使得$S \times T \in R$的最大的关系$T$

### 扩展关系代数操作：

无法用基本关系代数表示

分组操作$\gamma_{L:agg}(R)$：根据指定的属性进行分组，对每个组中的非分组属性的值进行aggregation操作：count、min、max、sum、avg

$\gamma_{Sdept,Ssex;count(*)\rightarrow Amt(Student)}$: 统计学生信息表中每个系的男生人数和女生人数

$\gamma_{Sno;avg(Grade)\rightarrow Score}(SC)$: 统计每门已选课学生的选课数和平均分

赋值操作

## 3 关系演算

