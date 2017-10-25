### query子句

| 子句名称 | 使用目的 |
| :---: | :---: |
| select | 确定结果集中应该包含哪些列 |
| from | 指明提供数据的表，以及这些表是如何连接的 |
| where | 过滤不要的数据 |
| group by | 对具有相同列值的行进行分组 |
| having | 过滤不要的组 |
| order by | 按一个或多个列，对最后结果集中的行进行排序 |

### select子句

**用于在所有可能的列中，选择查询结果集要包含哪些列。**

```
/* 显示department表中所有的行和列 */
SELECT * FROM department;
```

可以加上哪些元素：

* 字符，比如数字或字符串；
* 表达式，比如transaction.amount\*-1；
* 调用内建函数，比如ROUND\(transaction.amount,2\)；
* 用户自定义的函数调用。

简单的演示：

```
SELECT emp_id,
  'ACTIVE',
  emp_id * 3.14159,
  UPPER(lname)
FROM employee;  
```

```
SELECT VERSION(),
 USER(),
 DATABASE();
```

### 列的别名

通过在select子句中的每个元素后面增加列别名

```
SELECT emp_id,
  'ACTIVE' status,
  emp_id * 3.14159 empid_x_pi,
  UPPER(lname) AS last_name_upper
FROM employee;  
```

为了在子句中更清晰地表示别名，可以在这些别名前加上关键字as

### 去除重复的行

因为某些客户可能有多个账户，所以查询结果中多次包含该客户的ID。

如果只需要对每个客户显示一次ID，而不是为account表中每一行都显示相应的客户ID。

这时select后加上distinct，例如：

```
SELECT DISTINCT cust_id FROM account;
```

ALL关键字是默认的，这里被DISTINCT替代。

> 产生无重复的结果集需要首先对数据排序，这对大的结果集相当耗时。

### from子句

定义了查询中所使用的表，以及连接这些表的方式。

**“表“**去除”被存储的数据“的含义，仅考虑其关联行集合。因此宽泛的定义存在3种类型：

* 永久表（create table创建的）
* 临时表（子查询所返回的）
* 虚拟表（create view子句创建的视图）

这3中都可以在查询的from子句中使用。

**子查询**指的是包含在另一个查询中的查询。可以出现在select语句中的各个部分并且被包含在圆括号中国。

在from子句内，子查询的作用是根据其他查询子句（其中的from子句可以与其他表进行交互）产生临时表，例如：

```
SELECT e.emp_id, e.fname, e.lname
FROM (SELECT emp_id, fname, lname, start_date, title
      FROM employee) e;
```

### 视图

是存储在数据字典中的查询，它的行为表现得像一个表，但实际上并不拥有任何数据。

先定义一个查询employee表的视图：

```
CREATE VIEW employee_vw AS 
SELECT emp_id, fname, lname, YEAR(start_date) start_year
FROM employee;
```

当试图被创建后，并没有产生或存储任何数据，服务器只是简单地保留该查询以供将来使用。

```
SELECT emp_id, start_year
FROM employee_vw;
```



