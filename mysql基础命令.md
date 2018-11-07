#### 本文参考  http://www.runoob.com/mysql/mysql-create-tables.html
 ###  常用
  ```shell
  整数int、定点小数dec、浮点数float、字符串varchar、时间-时区、布尔bool、位
	desc table_name 		显示表结构
	show tables; --显示该数据库里的所有表
	show databases; 查看所有数据库，
	Show table status like ’testalter’\G 查看数据表类型
```
### 创建数据库
	 `create DATABASE` 数据库名;
### 删除数据库
	drop database 数据库名;
### 选择数据库	
	use  数据库名;
### 创建数据表
  ```shell
CREATE TABLE IF NOT EXISTS `runoob_tbl`(
`runoob_id` INT UNSIGNED AUTO_INCREMENT,
`runoob_title` VARCHAR(100) NOT NULL,
`runoob_author` VARCHAR(40) NOT NULL,
`submission_date` DATE,
PRIMARY KEY ( `runoob_id` ))
ENGINE=InnoDB DEFAULT CHARSET=utf8;

	INT UNSIGNED AUTO_INCREMENT 无符号自动递增
	varchar(10) not null 非空。
  ```

1添加表字段
```
alter table table1 add transactor varchar(10) not Null;
```
```
alter table   table1 add id int unsigned not Null auto_increment primary key
```


### 删除数据表
	DROP TABLE 数据库名;
### 插入数据
	insert into runoob_tbl 
	(runoob_title, runoob_author, submission_date)
	values
	("学习 PHP", "菜鸟教程", NOW());
insert into Websites
(name,url,alexa,country)
values
("","","","");
### 查询数据
	select * from runoob_tbl;
	select * from runoob_tbl where runoob_author='菜鸟教程';
	select * from runoob_tbl WHERE BINARY runoob_author='RUNOOB.COM';

BINARY 关键字来设定 WHERE 子句的字符串区分大小写
WHERE 后面加搜索条件
UPDATE 查询 
	UPDATE runoob_tbl SET runoob_title='学习 C++' WHERE runoob_id=3;
		Query OK, 1 rows affected (0.01 sec)

	SELECT * from runoob_tbl WHERE runoob_id=3;
		+-----------+--------------+---------------+-----------------+
		| runoob_id | runoob_title | runoob_author | submission_date |
		+-----------+--------------+---------------+-----------------+
		| 3         | 学习 C++   | RUNOOB.COM    | 2016-05-06      |
		+-----------+--------------+---------------+-----------------+
		1 rows in set (0.01 sec)
DELETE 删除数据
	DELETE FROM runoob_tbl WHERE runoob_id=3;
LIKE 子句
有时候我们需要获取 runoob_author 字段含有 "COM" 字符的所有记录
	SELECT * from runoob_tbl  WHERE runoob_author LIKE '%COM';
### UNION 操作符
UNION 操作符用于连接两个以上的 SELECT 语句的结果组合到一个结果集合中。多个 SELECT 语句会删除重复的数据。
	select country from Websites
	union    或者 union all
	select country from apps
	order by country;
语句使用 UNION ALL 从 "Websites" 和 "apps" 表中选取所有的country（也有重复的值）：
下面的 SQL 语句使用 UNION ALL 从 "Websites" 和 "apps" 表中选取所有的中国(CN)的数据（也有重复的值）：
SELECT country, name FROM Websites
WHERE country='CN'
UNION ALL
SELECT country, app_name FROM apps
WHERE country='CN'
ORDER BY country;
排序  ASC 	DESC
	SELECT * from runoob_tbl ORDER BY submission_date DESC; 倒序
	SELECT * from runoob_tbl ORDER BY submission_date ASC;    顺序
GROUP BY 语句   （SUM,AVG,COUNT…）
	接下来我们使用 GROUP BY 语句 将数据表按名字进行分组，并统计每个人有多少条记录：
	SELECT name, COUNT(*) FROM   employee_tbl GROUP BY name;
WITH ROLLUP 可以实现在分组统计数据基础上再进行相同的统计（SUM,AVG,COUNT…）。
	SELECT name, SUM(singin) as singin_count FROM  employee_tbl GROUP BY name WITH ROLLUP;
	我们可以使用 coalesce 来设置一个可以取代 NUll 的名称，coalesce 语法：
	SELECT coalesce(name, '总数'), SUM(singin) as singin_count FROM  employee_tbl GROUP BY name WITH ROLLUP;
	
两张表链接的使用   

使用MySQL的INNER JOIN(也可以省略 INNER 使用 JOIN，效果一样)来连接以上两张表来读取runoob_tbl表中所有runoob_author字段在tcount_tbl表对应的runoob_count字段值：
	SELECT a.runoob_id, a.runoob_author, b.runoob_count FROM runoob_tbl a INNER JOIN tcount_tbl b ON a.runoob_author = b.runoob_author;
	以上 SQL 语句等价于：
	SELECT a.runoob_id, a.runoob_author, b.runoob_count FROM runoob_tbl a, tcount_tbl b WHERE a.runoob_author = b.runoob_author;
LEFT JOIN
MySQL left join 与 join 有所不同。 MySQL LEFT JOIN 会读取左边数据表的全部数据，即便右边表无对应数据。
RIGHT JOIN
MySQL RIGHT JOIN 会读取右边数据表的全部数据，即便左边边表无对应数据。

NULL 值处理
	查找数据表中 runoob_test_tbl 列是否为 NULL，必须使用 IS NULL 和 IS NOT NULL，如下实例：
	SELECT * FROM runoob_test_tbl WHERE runoob_count IS NULL;
	SELECT * from runoob_test_tbl WHERE runoob_count IS NOT NULL;

### 正则表达式
	
^ , $
. 匹配除 "\n" 之外的任何单个字符
[...] 字符集合。匹配所包含的任意一个字符。 例如， '[abc]' 可以匹配 "plain" 中的 'a'。
[^…]负值字符集合。匹配未包含的任意字符 例如， '[^abc]' 可以匹配 "plain" 中的'p'。
p1|p2|p3 	  匹配 p1 或 p2 或 p3。例如，'z|food' 能匹配 "z" 或 "food"。'(z|f)ood' 则匹配 "zood" 或 "food"。
*  匹配前面的子表达式零次或多次
+	匹配前面的子表达式一次或多次。例如，'zo+' 能匹配 "zo" 以及 "zoo"，但不能匹配 "z"。+ 等价于 {1,}。
{n}	n 是一个非负整数。匹配确定的 n 次。例如，'o{2}' 不能匹配 "Bob" 中的 'o'，但是能匹配 "food" 中的两个 o。
{n,m}	m 和 n 均为非负整数，其中n <= m。最少匹配 n 次且最多匹配 m 次。

### ALTER命令

#### 创建一张表，表名为：testalter_tbl。
mysql> create table testalter_tbl
	(
	 i INT,
	 c CHAR(1)
	);

#### 如下命令使用了 ALTER 命令及 DROP 子句来删除以上创建表的 i 字段：
	ALTER TABLE testalter_tbl  DROP i;
#### MySQL 中使用 ADD 子句来向数据表中添加列，如下实例在表 testalter_tbl 中添加 i 字段，并定义数据类型:
	ALTER TABLE testalter_tbl ADD i INT;
#### 新增字段的位置， FIRST (设定位第一列)， AFTER 字段名（设定位于某个字段之后）。FIRST 和 AFTER 关键字只占用于 ADD 子句
	ALTER TABLE testalter_tbl ADD i INT FIRST;
	ALTER TABLE testalter_tbl ADD i INT AFTER c;
	
#### 把字段 c 的类型从 CHAR(1) 改为 CHAR(10)
	ALTER TABLE testalter_tbl MODIFY c CHAR(10);    
#### 使用 CHANGE 子句,  在 CHANGE 后，指定新字段名及类型。
	ALTER TABLE testalter_tbl CHANGE i j BIGINT;
	ALTER TABLE testalter_tbl CHANGE j j INT;
#### ALTER TABLE 对 Null 值和默认值的影响
	指定字段 j 为 NOT NULL 且默认值为100 。
	ALTER TABLE testalter_tbl 
	MODIFY j BIGINT NOT NULL DEFAULT 100;
#### 修改字段默认值
	alter table testalter_tbl alter i set default 1000;
	show columns from testalter_tbl;
	你也可以使用 ALTER 命令及 DROP子句来删除字段的默认值，如下实例：
	ALTER TABLE testalter_tbl ALTER i DROP DEFAULT;
#### 修改表名
	alter table testalter_tbl rename to alter_tbl;
#### 查看数据表类型可以使用 SHOW TABLE STATUS 语句。
	SHOW TABLE STATUS LIKE 'testalter_tbl'\G

#### 修改存储引擎：修改为myisam
	alter table tableName engine=myisam;
#### 删除外键约束：keyName是外键别名
	alter table tableName drop foreign key keyName;
#### 修改字段的相对位置：这里name1为想要修改的字段，type1为该字段原来类型，first和after二选一，这应该显而易见，first放在第一位，after放在name2字段后面
	alter table tableName modify name1 type1 first|after name2;


#### 复制表   （测试失败）
	1.获取数据表的完整结构。
	SHOW CREATE TABLE runoob_tbl \G;
	2.修改SQL语句的数据表名，并执行SQL语句。
	CREATE TABLE `clone_tbl` (
	   `runoob_id` int(11) NOT NULL auto_increment,
	   `runoob_title` varchar(100) NOT NULL default '',
	   `runoob_author` varchar(40) NOT NULL default '',
	   `submission_date` date default NULL,
	   PRIMARY KEY  (`runoob_id`),
	   UNIQUE KEY `AUTHOR_INDEX` (`runoob_author`)
	) ENGINE=InnoDB;
	3. 执行完第二步骤后，你将在数据库中创建新的克隆表 clone_tbl。 如果你想拷贝数据表的数据你可以使用 INSERT INTO... SELECT 语句来实现。
	INSERT INTO clone_tbl (runoob_id,runoob_title,runoob_author,submission_date)
    	SELECT runoob_id,runoob_title,runoob_author,submission_date
  	FROM runoob_tbl;
序列使用
	AUTO_INCREMENT 来定义列。 id 无需指定值可实现自动增长。\
		  CREATE TABLE insect
    	 (
  	   id INT UNSIGNED NOT NULL auto_increment,
   	   primary key (id),
  	   name VARCHAR(30) NOT NULL, # type of insect
    	   date DATE NOT NULL, # date collected
 	   origin VARCHAR(30) NOT NULL # where collected
	);


	INSERT INTO insect (id,name,date,origin) VALUES
	(NULL,'grasshopper','2001-09-10','front yard');
	SELECT * FROM insect ORDER BY id;
### 处理重复数据
	PRIMARY KEY  (primary key)  // 重要的 key 不重复
	CREATE TABLE person_tbl
	(
	  first_name CHAR(20) NOT NULL,
 	  last_name CHAR(20) NOT NULL,
 	  sex CHAR(10),
   	  PRIMARY KEY (last_name, first_name)
	);
INSERT IGNORE INTO（insert ignore into）会忽略数据库中已经存在的数据，如果数据库没有数据，就插入新的数据，如果有数据的话就跳过这条数据。这样就可以保留数据库中已经存在数据，达到在间隙中插入数据的目的。
	INSERT IGNORE INTO person_tbl (last_name, first_name)
    	VALUES( 'Jay', 'Thomas');

### 统计重复数据
	SELECT COUNT(*) as repetitions, last_name, first_name
	FROM person_tbl
    	GROUP BY last_name, first_name
    	HAVING repetitions > 1;
### 过滤重复数据
	SELECT DISTINCT last_name, first_name
	FROM person_tbl;
你也可以使用 GROUP BY 来读取数据表中不重复的数据：
	SELECT last_name, first_name
	FROM person_tbl
	GROUP BY (last_name, first_name);

### 删除重复数据
	CREATE TABLE tmp SELECT last_name, first_name, sex FROM person_tbl  GROUP BY (last_name, first_name, sex);
	DROP TABLE person_tbl;
	ALTER TABLE tmp RENAME TO person_tbl;
当然你也可以在数据表中添加 INDEX（索引） 和 PRIMAY KEY（主键）这种简单的方法来删除表中的重复记录。方法如下：
	ALTER IGNORE TABLE person_tbl
	ADD PRIMARY KEY (last_name, first_name);













