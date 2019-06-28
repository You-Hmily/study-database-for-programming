#MySQL必知必会
##1、了解数据库
    1.数据库基础
          数据库（database）：保存有组织的数据的容器（通常是一个文件或文件组）。
          表（table）：某种特定类型的数据的结构化清单。
          模式（schema）：关于数据库和表的布局及特性的信息。
          列（column）：表中的一个字段。所有表都是由一个或者多个列组成的。
          数据类型（datatype）：所容许的数据的类型，每个表列都有相应的数据类型，它限制该列中存储的数据
          行（row）：表中的一个记录。
          主键（primary key）：一列（或一组列），其值能够唯一区分表中每个行。
          
    2.SQL
          SQL：结构化查询语言的缩写，SQL是专门用来与数据库通信的语言。
          SQL的优点：
              1、SQL不是某个特定数据库供应商转有的语言。几乎所有重要的DBMS都支持SQL，所以，学习此语言使你几乎能与所有数据库打交道
              2、SQL简单易学。它的语句全都是由描述性很强的英语单词组成，而且这些单词的数目不多。
              3、SQL尽管看上去很简单，但实际上是一种强有力的语言，灵活使其语言元素，可以进行复杂和高级的数据库操作。
              
##2、MySQL数据库简介
    1、什么是MySQL：MySQL是一种DBMS(数据库管理系统)，即它是一种数据库软件
       使用MySQL的原因：
           1、成本--开源软件，免费使用。
           2、性能--MySQL执行很快
           3、可信赖--很多公司使用
           4、简单--MySQL容易安装和使用
    2、MySQL工具：MySQL是一个客户机-服务器DBMS。
           1、mysql命令行实用程序
              完整命令获取 mysql --help
              命令输入在mysql>之后
              命令用;或者\g结束，仅使用enter不执行命令
              输入help或\h获取帮助 如 help select（获取使用select的帮助）
              输入quit 或 exit退出命令行实用程序
           2、MySQL Administrator
              
           3、MySQL Query Browser 
           
##3、使用MySQL
    1、连接
    2、选择数据库
       关键字（key word）：作为MySQL语言组成部分的一个保留字。决不要用关键字命名一个表或列。
       使用test数据库，应输入： USE test 
    3、了解数据库和表
       查看数据库列表：SHOW DATABASES
       查看数据库内表的列表：SHOW TABLES
       查询表的表列：SHOW COLUMNS FROM TABLE
       用于显示广泛的服务器状态信息：SHOW STATUS
       显示创建特定数据库或表的MySQL语句：SHOW CREATE DATABASE 和 SHOW CREATE TABLE
       显示授予用户的安全权限：SHOW GRANTS
       显示服务器错误或者警告：SHOW ERRORS 和 SHOW WARNING
       
##4、检索数据
    1、SELECT语句
       SELECT * FROM TEST
    2、检索单个列
       SELECT prod_name FROM products
    3、检索多列
       SELECT prod_id,prod_name FROM products
    4、检索所有列
       SELECT * FROM products
    5、检索不同的行
       SELECT DISTINCT vend_id FROM products
    6、限制结果
       SELECT prod_name FROM products LIMIT 5; //显示不多余5条记录
       
       SELECT prod_name FROM products LIMIT 5,5;//显示 第五行开始的5行记录
       
    7、使用完全限定的表名
       SELECT products.prod_name FROM products;
       SELECT products.prod_name FROM crashcourse.products;
    
       
##5、排序检索数据
    1、排序数据
    SELECT prod_name FROM products ORDER BY prod_name;
    2、按多个列排序
    SELECT prod_id,prod_price,prod_name FROM products ORDER BY prod_price , prod_name;
    3、指定排序方向
    SELECT prod_id,prod_price,prod_name FROM prosucts ORDER BY prod_price DESC;
    SELECT prod_id,prod_price,prod_name FROM prosucts ORDER BY prod_price DESC,prod_name;
    
##6、过滤数据
    1、使用WHERE子句
    SELECT prod_name,prod_price FROM products WHERE prod_price=2.50;
    
    2、WHERE 子句操作符
       =  ：等于
       <> ：不等于
       != ：不等于
       <  ：小于
       <= ：小于等于
       >  ：大于
       >= ：大于等于
       BETWEEN : 在指定的两个值之间
       检查单个值：SELECT prod_name,prod_price WHERE prod_name=‘fuses’
       不匹配检查：SELECT vend_id,prod_name FROM products WHERE vend_id<>1003;
                  SELECT vend_id,prod_name FROM products WHERE vend_id != 1003;
       范围值检查：SELECT prod_name,prod_price FROM products WHERE prod_price BETWEEN 5 and 10;// 取值范围包括开始值和结束值
       空值检查： NULL 无值，它与字段包含0、空字符串或仅仅包含空格不同
                 SELECT prod_name FROM products WHERE prod_price IS NULL;

##7、数据过滤
    1、组合 WHERE 子句
    2、IN 操作符                 
