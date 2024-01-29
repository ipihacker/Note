**sql 19 level** 



### 基础语法

#### 1.查询

- 全表查询

```sql
select * from student
```

- 选择查询

```sql
select name, gender from student
```

- 别名

```sql
select name as stuff_name, position as position_name from employees
```

- 常量和运算

```sql
select 200, '篮球' as hobby
```



#### 2.条件查询

- where

**概念**

通过条件查询，你可以从数据库中筛选出 **满足特定条件** 的数据行，而不是返回表中的所有数据。
主要使用 where 子句在查询中设置过滤条件，只有满足这些条件的数据行才会被返回。

where 子句的语法如下：

```sql
SELECT 列1, 列2, ...
FROM 表名
WHERE 条件;
```

其中，`列1, 列2, ...`是你要选择的列，可以是具体的列名，也可以是`*`表示选择所有列。`表名`是你要从中查询数据的表名。`条件`是指定的查询条件，可以使用比较运算符（如`=`、`<`、`>`等）、逻辑运算符（如`AND`、`OR`等）、IN 操作符、LIKE 操作符等来设置条件。

**示例**

让我们来看一个具体的SQL代码和结果示例，假设有一张名为`products`的数据表，它存储了产品信息，包括产品名称（name）、单价（price）、库存（stock）等：

数据表`products`：

| name | price | stock |
| ---- | ----- | ----- |
| A    | 10.00 | 50    |
| B    | 20.00 | 30    |
| C    | 15.00 | 20    |
| D    | 25.00 | 10    |

现在，我们使用 "WHERE" 来筛选出库存小于等于 20 的产品：

```sql
-- SQL查询语句
select name, price, stock from products where stock <= 20;
```

查询结果：

| name | price | stock |
| ---- | ----- | ----- |
| C    | 15.00 | 20    |
| D    | 25.00 | 10    |

通过上述 SQL 查询语句，我们筛选出了库存小于等于 20 的产品，从而得到了符合条件的产品信息。

- 运算符

**概念**

运算符是 SQL 中用于在条件查询中进行条件判断的特殊符号，比如 `=`、 `!=`、`<`、`>` 等。通过使用不同的运算符，我们可以在查询语句中设定多样化的条件，从而根据数据的不同属性进行灵活的筛选和过滤。

**示例**

数据表 `employees`：

| name | age  | salary |
| ---- | ---- | ------ |
| 小明 | 25   | 5000   |
| 小红 | 30   | 6000   |
| 小李 | 28   | 5500   |
| 小张 | 22   | 4500   |

现在，我们使用不同的运算符来进行条件查询：

1）使用 "!=" 运算符筛选出 name 不是 '小张' 的员工：

```sql
-- SQL查询语句
select name, age, salary from employees where name != '小张';
```

查询结果：

| name | age  | salary |
| ---- | ---- | ------ |
| 小明 | 25   | 5000   |
| 小红 | 30   | 6000   |
| 小李 | 28   | 5500   |

2）使用 ">" 运算符筛选出工资高于 5500 的员工：

```sql
-- SQL查询语句
select name, age, salary from employees where salary > 5500;
```

查询结果：

| name | age  | salary |
| ---- | ---- | ------ |
| 小红 | 30   | 6000   |

3）使用 "BETWEEN" 运算符筛选出年龄在 25 到 30 之间的员工：

```sql
-- SQL查询语句
select name, age, salary from employees where age between 25 and 30;
```

查询结果：

| name | age  | salary |
| ---- | ---- | ------ |
| 小明 | 25   | 5000   |
| 小红 | 30   | 6000   |
| 小李 | 28   | 5500   |

- 空值

**概念**

在数据库中，有时候数据表的某些字段可能没有值，即为空值（NULL）。
空值表示该字段的值是未知的、不存在的或者没有被填写的。在SQL查询中，我们可以使用 "IS NULL" 和 "IS NOT NULL" 来判断字段是否为空值或非空值。

**示例**

假设有一张名为 `employees` 的数据表，它存储了员工信息，包括员工姓名（name）、年龄（age）、入职日期（hire_date）等：

数据表 `employees` ：

| name | age  | hire_date  |
| ---- | ---- | ---------- |
| 小明 | 25   | 2020-01-01 |
| 小红 | 30   | 2020-02-15 |
| 小李 | 28   | NULL       |
| 小张 | NULL | 2020-03-20 |

现在，我们使用 "IS NULL" 来查询出入职日期未填写的员工：

```sql
-- SQL查询语句
select name, age from employees where hire_date is null;
```

查询结果：

| name | age  |
| ---- | ---- |
| 小李 | 28   |

- 模糊查询

**概念**

模糊查询是一种特殊的条件查询，它允许我们根据模式匹配来查找符合特定条件的数据，可以使用 LIKE 关键字实现模糊查询。

在 LIKE 模糊查询中，我们使用通配符来代表零个或多个字符，从而能够快速地找到匹配的数据。
有如下 2 种通配符：
	百分号（%）：表示任意长度的任意字符序列。
	下划线（_）：表示任意单个字符。

**示例**

数据表`employees`：

| name | age  | position       |
| ---- | ---- | -------------- |
| 张三 | 25   | 软件工程师     |
| 李四 | 30   | 数据分析师     |
| 王五 | 28   | 产品经理       |
| 小明 | 22   | 软件测试工程师 |

现在，我们使用 LIKE 模糊查询来找出姓名（name）中包含关键字 "张" 的员工信息：

```sql
-- SQL查询语句
select name, age, position from employees where name like '%张%';
```

查询结果：

| name | age  | position   |
| ---- | ---- | ---------- |
| 张三 | 25   | 软件工程师 |

还可以使用模糊查询匹配开头和结尾：

```sql
-- 只查询以 "张" 开头的数据行
select name, age, position from employees where name like '张%';

-- 只查询以 "张" 结尾的数据行
select name, age, position from employees where name like '%张';
```

同理，可以使用 `not like` 来查询不包含某关键字的信息。

- 逻辑运算

**概念**

逻辑运算是一种在条件查询中使用的运算符，它允许我们结合多个条件来过滤出符合特定条件的数据。

在逻辑运算中，常用的运算符有：

- AND：表示逻辑与，要求同时满足多个条件，才返回 true。
- OR：表示逻辑或，要求满足其中任意一个条件，就返回 true。
- NOT：表示逻辑非，用于否定一个条件（本来是 true，用了 not 后转为 false）

**示例**

假设有一张名为`employees`的数据表，它存储了员工信息，包括员工姓名（name）、年龄（age）、工资（salary）等：

数据表`employees`：

| name | age  | salary |
| ---- | ---- | ------ |
| 张三 | 25   | 10000  |
| 李四 | 30   | 12000  |
| 李五 | 28   | 15000  |
| 小明 | 22   | 8000   |

现在，我们使用逻辑运算来找出姓名中包含关键字 "李" **且** 年龄小于 30 岁的员工信息：

```sql
-- SQL查询语句
select name, age, salary from employees where name like '%李%' and age < 30;
```

查询结果：

| name | age  | salary |
| ---- | ---- | ------ |
| 李五 | 28   | 15000  |

#### 3.去重

**概念**

使用 `DISTINCT` 关键字来实现去重操作。

**示例**

假设有一张名为`students`的数据表，它存储了学生信息，包括学生姓名（name）、班级ID（class_id）、考试编号（exam_num）、成绩（score）等：

数据表`students`：

| name | class_id | exam_num | score |
| ---- | -------- | -------- | ----- |
| 张三 | 1        | 1        | 90    |
| 李四 | 2        | 2        | 85    |
| 王五 | 1        | 1        | 92    |
| 李四 | 2        | 3        | 88    |

现在，我们使用`DISTINCT`关键字来找出不同的班级 ID：

```sql
-- SQL 查询语句
select distinct class_id from students;
```

查询结果：

| class_id |
| -------- |
| 1        |
| 2        |

除了按照单字段去重外，`DISTINCT` 关键字还支持根据多个字段的组合来进行去重操作，确保多个字段的组合是唯一的。

示例语法如下：

```sql
distinct 字段1, 字段2, 字段3, ...
```

#### 4.排序

在 SQL 中，我们可以使用 `ORDER BY` 关键字来实现排序操作。`ORDER BY` 后面跟上需要排序的字段，可以选择升序（ASC）或降序（DESC）排列。

数据表 `students` ：

| name | age  | score |
| ---- | ---- | ----- |
| 张三 | 18   | 90    |
| 李四 | 20   | 85    |
| 王五 | 19   | 92    |
| 赵六 | 20   | 88    |

现在，我们使用`ORDER BY`关键字来对学生表进行排序：

```sql
-- SQL 查询语句 1
select name, age from students order by age asc;

-- SQL 查询语句 2
select name, score from students order by score desc;
```

查询语句 1 结果，按照年龄升序（从小到大）：

| name | age  |
| ---- | ---- |
| 张三 | 18   |
| 王五 | 19   |
| 李四 | 20   |
| 赵六 | 20   |

查询语句 2 结果，按照分数降序（从大到小）：

| name | score |
| ---- | ----- |
| 王五 | 92    |
| 张三 | 90    |
| 赵六 | 88    |
| 李四 | 85    |

在排序的基础上，我们还可以根据多个字段的值进行排序。当第一个字段的值相同时，再按照第二个字段的值进行排序，以此类推。

示例语法如下：

```sql
order by 字段1 [升序/降序], 字段2 [升序/降序], ...
```



#### 5.截断和偏移

**概念**

假设你有一张待办事项清单，上面有很多任务。当你每次只想查看其中的几个任务时，会怎么办呢？

1）你可以使用手指挡住不需要看的部分（即截断）

2）根据任务的编号，直接翻到需要查看的位置（即偏移）

在 SQL 中，我们使用 `LIMIT` 关键字来实现数据的截断和偏移。

截断和偏移的一个典型的应用场景是分页，即网站内容很多时，用户可以根据页号每次只看部分数据。

**示例**

数据表`tasks`：

| task_name | due_date   |
| --------- | ---------- |
| 完成报告  | 2023-08-05 |
| 预约医生  | 2023-08-08 |
| 购买礼物  | 2023-08-10 |
| 安排旅行  | 2023-08-15 |

现在，我们使用`LIMIT`关键字来进行分页查询：

```sql
-- LIMIT 后只跟一个整数，表示要截断的数据条数（一次获取几条）
select task_name, due_date from tasks limit 2;

-- LIMIT 后跟 2 个整数，依次表示从第几条数据开始、一次获取几条
select task_name, due_date from tasks limit 2, 2;
```

查询语句 1 结果，只获取了 2 条数据：

| task_name | due_date   |
| --------- | ---------- |
| 完成报告  | 2023-08-05 |
| 预约医生  | 2023-08-08 |

查询语句 2 结果，从下标为 2（第 3 条）数据的位置开始获取 2 条数据：

| task_name | due_date   |
| --------- | ---------- |
| 购买礼物  | 2023-08-10 |
| 安排旅行  | 2023-08-15 |

通过上述 SQL 查询语句，我们分别选取了待办事项表中的前两个任务和从第三个任务开始的两个任务，实现了数据的截断和偏移。



#### 6.条件分支

**概念**

条件分支 `case when` 是 SQL 中用于根据条件进行分支处理的语法。它类似于其他编程语言中的 if else 条件判断语句，允许我们根据不同的条件选择不同的结果返回。

使用 `case when` 可以在查询结果中根据特定的条件动态生成新的列或对现有的列进行转换。

**示例**

假设有一个学生表 `student`，包含以下字段：`name`（姓名）、`age`（年龄）。数据如下：

| name | age  |
| ---- | ---- |
| 小明 | 18   |
| 鸡哥 | 25   |
| 李华 | 30   |
| 王五 | 40   |

使用条件分支 `case when` ，根据 name 来判断学生是否会说 RAP，并起别名为 can_rap。

示例 SQL 如下：

```sql
SELECT
  name,
  CASE WHEN (name = '鸡哥') THEN '会' ELSE '不会' END AS can_rap
FROM
  student;
```

查询结果：

| name | can_rap |
| ---- | ------- |
| 小明 | 不会    |
| 鸡哥 | 会      |
| 李华 | 不会    |
| 王五 | 不会    |

`case when` 支持同时指定多个分支，示例语法如下：

```sql
CASE WHEN (条件1) THEN 结果1
	   WHEN (条件2) THEN 结果2
	   ...
	   ELSE 其他结果 END
```



### 函数

#### 1.时间函数

**概念**

在 SQL 中，时间函数是用于处理日期和时间的特殊函数。它们允许我们在查询中操作和处理日期、时间、日期时间数据，从而使得在数据库中进行时间相关的操作变得更加方便和灵活。

常用的时间函数有：

- DATE：获取当前日期
- DATETIME：获取当前日期时间
- TIME：获取当前时间

**示例** 

假设有一个订单表 `orders`，包含以下字段：`order_id`（订单号）、`order_date`（下单日期）、`order_time`（下单时间）。数据如下：

| order_id | order_date | order_time |
| -------- | ---------- | ---------- |
| 1        | 2023-08-01 | 12:30:45   |
| 2        | 2023-08-01 | 14:20:10   |
| 3        | 2023-08-02 | 09:15:00   |
| 4        | 2023-08-02 | 18:05:30   |

使用时间函数获取当前日期、当前日期时间和当前时间：

```sql
-- 获取当前日期
SELECT DATE() AS current_date;

-- 获取当前日期时间
SELECT DATETIME() AS current_datetime;

-- 获取当前时间
SELECT TIME() AS current_time;

-- 返回日期/时间的单独部分
EXTRACT()	

-- 向日期添加指定的时间间隔
DATE_ADD()

-- 从日期减去指定的时间间隔
DATE_SUB()

-- 返回两个日期之间的天数
DATEDIFF()	

-- 用不同的格式显示日期/时间
DATE_FORMAT()	
```

查询结果：

> 为了方便对比，放到同一个表格

| current_date | current_datetime    | current_time |
| ------------ | ------------------- | ------------ |
| 2023-08-01   | 2023-08-01 14:30:00 | 14:30:00     |

> 注意，这里的日期、日期时间和时间将根据当前的系统时间来生成，实际运行结果可能会因为当前时间而不同。

#### 2.字符串处理

**概念**

在 SQL 中，字符串处理是一类用于处理文本数据的函数。它们允许我们对字符串进行各种操作，如转换大小写、计算字符串长度以及搜索和替换子字符串等。字符串处理函数可以帮助我们在数据库中对字符串进行加工和转换，从而满足不同的需求。

**示例**

假设有一个员工表 `employees`，包含以下字段：`id`（员工编号）、`name`（员工姓名）。数据如下：

| id   | name     |
| ---- | -------- |
| 1    | 小明     |
| 2    | 热dog    |
| 3    | Fish摸摸 |
| 4    | 鸡哥     |

1）使用字符串处理函数 `UPPER` 将姓名转换为大写：

```sql
-- 将姓名转换为大写
SELECT name, UPPER(name) AS upper_name
FROM employees;
```

查询结果：

| name     | upper_name |
| -------- | ---------- |
| 小明     | 小明       |
| 热dog    | 热DOG      |
| Fish摸摸 | FISH摸摸   |
| 鸡哥     | 鸡哥       |

2）使用字符串处理函数 `LENGTH` 计算姓名长度：

```sql
-- 计算姓名长度
SELECT name, LENGTH(name) AS name_length
FROM employees;
```

查询结果：

| name     | name_length |
| -------- | ----------- |
| 小明     | 2           |
| 热dog    | 4           |
| Fish摸摸 | 6           |
| 鸡哥     | 2           |

3）使用字符串处理函数 `LOWER` 将姓名转换为小写：

```sql
-- 将姓名转换为小写并进行条件筛选
SELECT name, LOWER(name) AS lower_name
FROM employees;
```

查询结果：

| id   | name     |
| ---- | -------- |
| 1    | 小明     |
| 2    | 热dog    |
| 3    | fish摸摸 |
| 4    | 鸡哥     |

#### 3.聚合函数

**概念**

在 SQL 中，聚合函数是一类用于对数据集进行 **汇总计算** 的特殊函数。它们可以对一组数据执行诸如计数、求和、平均值、最大值和最小值等操作。聚合函数通常在 SELECT 语句中配合 GROUP BY 子句使用，用于对分组后的数据进行汇总分析。

常见的聚合函数包括：

- COUNT：计算指定列的行数或非空值的数量。
- SUM：计算指定列的数值之和。
- AVG：计算指定列的数值平均值。
- MAX：找出指定列的最大值。
- MIN：找出指定列的最小值。

**示例**

假设有一个订单表 `orders`，包含以下字段：`order_id`（订单号）、`customer_id`（客户编号）、`amount`（订单金额）。数据如下：

| order_id | customer_id | amount |
| -------- | ----------- | ------ |
| 1        | A001        | 100    |
| 2        | A002        | 200    |
| 3        | A001        | 150    |
| 4        | A003        | 50     |

1）使用聚合函数 `COUNT` 计算订单表中的总订单数：

```sql
SELECT COUNT(*) AS order_num
FROM orders;
```

查询结果：

| order_num |
| --------- |
| 4         |

2）使用聚合函数 `COUNT(DISTINCT 列名)` 计算订单表中不同客户的数量：

```sql
SELECT COUNT(DISTINCT customer_id) AS customer_num
FROM orders;
```

查询结果：

| customer_num |
| ------------ |
| 3            |

3）使用聚合函数 `SUM` 计算总订单金额：

```sql
SELECT SUM(amount) AS total_amount
FROM orders;
```

查询结果：

| total_amount |
| ------------ |
| 500          |

### 分组聚合 

#### 1.单字段组合

**概念**

在 SQL 中，分组聚合是一种对数据进行分类并对每个分类进行聚合计算的操作。它允许我们按照指定的列或字段对数据进行分组，然后对每个分组应用聚合函数，如 COUNT、SUM、AVG 等，以获得分组后的汇总结果。

举个例子：某个学校可以按照班级将学生分组，并对每个班级进行统计。查看每个班级有多少学生、每个班级的平均成绩。这样我们就能够对学校各班的学生情况有一个整体的了解，而不是单纯看个别学生的信息。

在 SQL 中，通常使用 `GROUP BY` 关键字对数据进行分组。

**示例**

假设有一个订单表 `orders`，包含以下字段：`order_id`（订单号）、`customer_id`（客户编号）、`amount`（订单金额）。数据如下：

| order_id | customer_id | amount |
| -------- | ----------- | ------ |
| 1        | A001        | 100    |
| 2        | A002        | 200    |
| 3        | A001        | 150    |
| 4        | A003        | 50     |

1）使用分组聚合查询中每个客户的编号：

```sql
SELECT customer_id
FROM orders
GROUP BY customer_id;
```

查询结果：

| customer_id |
| ----------- |
| A001        |
| A002        |
| A003        |

2）使用分组聚合查询每个客户的下单数：

```sql
SELECT customer_id, COUNT(order_id) AS order_num
FROM orders
GROUP BY customer_id;
```

查询结果：

| customer_id | order_num |
| ----------- | --------- |
| A001        | 2         |
| A002        | 1         |
| A003        | 1         |

#### 2.多字段组合

**概念**

有时，单字段分组并不能满足我们的需求，比如想统计学校里每个班级每次考试的学生情况，这时就可以使用多字段分组。

多字段分组和单字段分组的实现方式几乎一致，使用 `GROUP BY` 语法即可。

**示例**

假设有一个订单表 `orders`，包含以下字段：`order_id`（订单号）、`product_id`（商品编号）、`customer_id`（客户编号）、`amount`（订单金额）。

数据如下：

| order_id | product_id | customer_id | amount |
| -------- | ---------- | ----------- | ------ |
| 1        | 1          | A001        | 100    |
| 2        | 1          | A002        | 200    |
| 3        | 1          | A001        | 150    |
| 4        | 1          | A003        | 50     |
| 5        | 2          | A001        | 50     |

要查询使用多字段分组查询表中 **每个客户** 购买的 **每种商品** 的总金额，相当于按照客户编号和商品编号分组：

```sql
-- 查询每个班级每次考试的学生人数
SELECT customer_id, product_id, SUM(amount) AS total_amount
FROM orders
GROUP BY customer_id, product_id;
```

查询结果：

| customer_id | product_id | total_amount |
| ----------- | ---------- | ------------ |
| A001        | 1          | 250          |
| A001        | 2          | 50           |
| A002        | 1          | 200          |
| A003        | 1          | 50           |

#### 3.having 子句

**概念**

在 SQL 中，HAVING 子句用于在分组聚合后对分组进行过滤。它允许我们对分组后的结果进行条件筛选，只保留满足特定条件的分组。

HAVING 子句与条件查询 WHERE 子句的区别在于，WHERE 子句用于在 **分组之前** 进行过滤，而 HAVING 子句用于在 **分组之后** 进行过滤。

**示例**

假设有一个订单表 `orders`，包含以下字段：`order_id`（订单号）、`customer_id`（客户编号）、`amount`（订单金额）。数据如下：

| order_id | customer_id | amount |
| -------- | ----------- | ------ |
| 1        | A001        | 100    |
| 2        | A002        | 200    |
| 3        | A001        | 150    |
| 4        | A003        | 50     |

1）使用 HAVING 子句查询订单数超过 1 的客户：

```sql
SELECT customer_id, COUNT(order_id) AS order_num
FROM orders
GROUP BY customer_id
HAVING COUNT(order_id) > 1;
```

查询结果：

| customer_id | order_num |
| ----------- | --------- |
| A001        | 2         |

2）使用 HAVING 子句查询订单总金额超过 100 的客户：

```sql
-- 查询总成绩超过200的班级
SELECT customer_id, SUM(amount) AS total_amount
FROM orders
GROUP BY customer_id
HAVING SUM(amount) > 100;
```

查询结果：

| customer_id | total_amount |
| ----------- | ------------ |
| A001        | 250          |
| A002        | 200          |