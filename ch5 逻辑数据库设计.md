之前：需求——>ER模型；本章：ER模型——>DB模式

## 1、ER模型转换为关系数据库模式

复合属性直接拿来作为关系的属性，多值属性开一个新关系并建立多值属性关系到实体型关系的外键约束；

弱实体型的转换：拿属主实体型的主键和弱实体型的部分键作为关系的主键，建立外键约束

M:N二元联系型：将联系型转换为关系名，两个实体型的主键作为此关系的主键，建立两个外键约束
N:1二元联系型：将1的主键放到N的属性集中，建立一个外键约束
1:1二元联系型：将1的主键和联系的属性放到另一个1中，往联系的双线实体加比较好

## 2、函数依赖

定义：R(U)是属性集U上的关系模式，$X\subseteq U,Y\subseteq U$。对于此关系模式的**所有关系实例**中的任意两个元组$t_1$和$t_2$，若由$t_1[X]=t_2[X]$可以推出$t_1[Y]=t_2[Y]$，则称X函数决定Y，Y函数依赖X，记作$X\rightarrow Y$

函数依赖针对关系模式，候选键针对关系。

例子：

<img src="ch5 逻辑数据库设计.assets/image-20210525203837187.png" alt="image-20210525203837187" style="zoom:50%;" />

### Armstrong公理系统

自反律

增广律

传递律

合并规则

伪传递规则

分解规则

### 属性集闭包

$X_F^+$

### 等价函数依赖集

函数依赖集的闭包：由F逻辑蕴含的全部函数依赖的集合叫做F的闭包，记作$F^+$

等价函数依赖集：若$F^+=G^+$，则F与G等价

函数依赖集的覆盖：若$G^+\subseteq F^+$，即G中的每个函数依赖都被F逻辑蕴含，则称F覆盖G

定理：F和G等价，当且仅当F覆盖G且G覆盖F，即G中的函数依赖都被F逻辑蕴含，F中的函数依赖都被G逻辑蕴含。

<img src="ch5 逻辑数据库设计.assets/image-20210526091334295.png" alt="image-20210526091334295" style="zoom:50%;" />

### 最小覆盖的计算

* 分解函数依赖
* 删除左部冗余属性：F删除后得到F'，F'肯定覆盖F，就看F能不能推出F'
* 删除冗余函数依赖，一个个看

## 3、关系模式的范式

1NF的问题：非主属性部分函数依赖于候选键，把候选键拆开

2NF：是1NF，且每个非主属性都完全函数依赖于R的候选键

3NF：是2NF，且每个非主属性都不传递函数依赖于候选键

BCNF：

* 若是1NF，F的最小覆盖中每个函数依赖的左部都是R的候选键
* 若是3NF，任意主属性都完全函数依赖于R的候选键

## 4、关系模式分解

无损连接性的判定

函数依赖保持性：

函数依赖集的投影：设R(U,F)是关系模式，U是属性集，F是函数依赖集，对于属性集的一个子集V，F在V上的投影是$F^+$中满足$X\cup Y\subseteq V$的函数依赖$X\rightarrow Y$的集合。投影都是针对**闭包**的。

分解后子关系的函数依赖集是F在这个关系上的投影，若所有子关系投影的并覆盖F，则此分解保持函数依赖。

函数依赖保持性的判定

关系模式的分解方法