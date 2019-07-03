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
       AND 操作符 ：SELECT prod_id,prod_price,prod_name FROM products WhHERE vend_id=1003 AND prod_price<=10;
       OR 操作符：SELECT prod_id,prod_price,prod_name FROM products WhHERE vend_id=1002 OR vend_id=1003;
       
    2、IN 操作符---用来指定条件范围，范围中的每个条件都可以进行匹配。
       SELECT prod_name,prod_price FROM products WHERE vend_id IN (1003,1004) ORDER BY prod_name;
    3、NOT 操作符 ---否定之后所跟的任何条件。
       SELECT prod_name,prod_price FROM products WHERE vend_in NOT IN (1002,1003) ORDER BY prod_name;
       MySQL支持使用 NOT 对 IN、BETWEEN 和 EXISTS 子句取反。                        
##8、用通配符进行过滤
    1、LIKE 操作符
       百分号（%）通配符：SELECT prod_id,prod_name FROM products WHERE prod_name LIKE 'jet%';// 以jet开头。匹配多个字符。
                          SELECT prod_id,prod_name FROM products WHERE prod_name LIKE '%anvil%';
       下划线（_）通配符：SELECT prod_id,prod_name FROM products WHERE prod_name LIKE '_ ton anvil';//下换线是匹配单个字符        
    
    2、使用通配符的技巧 
       1、不要过度使用通配符，该操作能替代的情况下少用。
       2、在确实需要使用通配符时，除非绝对有必要，否则不要把它们用到在搜索模式的开始处。
       3、仔细注意通配符的位置。
##9、用正则表达式进行搜索
     1、正则表达式的使用
         基本字符通配 REGEXP '1000'
           SELECT prod_name FROM products WHERE prod_name REGEXP '1000' ORDER BY prod_name;
           SELECT prod_name FROM products WHERE prod_name REGEXP '.000'; // .它表示匹配任意一个字符。
         进行OR 匹配 使用 |
           SELECT prod_name FROM products WHERE prod_name REGEXP '1000|2000';
         匹配几个字符之一
           SELECT prod_name FROM products WHERE prod_name REGEXP '[123] Tom';// 匹配1或2或3。
         匹配范围
           SELECT prod_name FROM products WHERE prod_name REGEXP '[1-5] Ton';// 匹配 1到5 的值
         匹配特殊字符
           SELECT prod_name FROM products WHERE prod_name REGEXP '.';// 匹配所有字符
           SELECT prod_name FROM products WHERE prod_name REGEXP '//.';// 匹配 . 字符
           为了匹配特殊字符，必须用\\ 为前导  \\-，\\.  。
           \\f：换页，\\n：换行，\\r：回车，\\t：制表，\\v：纵向制表
         匹配字符类：
            [:alnum:]：任意字母和数字（同[a-zA-Z0-9]）
            [:alpha:]：任意字符（同[a-zA-Z]）
            [:blank:]：空格和制表（同[\\t]）
            [:cntrl:]：ASCII控制字符（ASCII 0到31和127）
            [:digit:]：任意数字（同[0-9]）
            [:graph:]：与[:print:]相同，但不包含空格
            [:lower:]：任意小写字母（同[a-z]）
            [:print:]：打印任意字符
            [:punct:]：既不在[:alnum:]又不在[:cntrl:]中的任意字符
            [:space:]：包括空格在内的任意空白字符（同[\\f\\n\\r\\t\\v]）
            [:upper:]：任意大写字母（同[A-Z]）
            [:xdigit:]：任意十六进制数字（同[a-fA-F0-9]）
         匹配多个实例
             *：0个或多个匹配
             +：一个或多个匹配（等于{1,}）
             ?：0个或1个匹配（等于{0,1}）
             {n}：指定数目的匹配
             {n,}：不少于指定数目的匹配
             {n,m}：匹配数目的范围（m不超过255）
             SELECT prod_name FROM products WHERE prod_name REGEXP '\\([0-9] sticks?\\)';
             SELECT prod_name FROM products WHERE prod_name REGEXP '[[:DIGIT:]]{4}';匹配4位数字
         定位符
             ^：文本的开始
             $：文本的结尾
             [[:<:]]：词的开始
             [[:>:]]：词的结尾
             SELECT prod_name FROM products WHERE prod_name REFEXP '^[0-9\\.]';
##10、创建计算字段
    1、计算字段
       字段（field）基本上与列（column）意思相同。
       计算字段并不存在于数据库表中。计算字段是运行时在SELECT语句内创建的。
    2、拼接字段
       拼接（concatenate）将值联结到一起构成单个值。
       在MySQL的SELECT 语句中，可使用 Concat() 函数来拼接两个列。
       SELECT Concat(vend_name,'(',vend_country,')') AS vend_title FROM vendors ORDER BY vend_name;
       AS vend_title 为使用别名的方法。
    3、执行算术计算
       SELECT prod_id,quantity,item_price,quantity*item_price AS expended_price FROM orderitems WHERE order_num=20005;
        + ：加，- ：减，* ：乘，/ ：除 。
       
##11、使用数据处理函数
    1、文本处理函数
       SELECT vend_name,Upper(vend_name) AS vend_name_upcase FROM vendors ORDER BY vend_name;
       Left()：返回串左边的字符
       Length()：返回串的长度
       Locate()：找出串的一个子串
       Lower()：将串转化为小写
       LTrime()：去掉串左边的空格
       Right()：返回串右边的字符
       RTrime()：去掉串右边的空格
       Soundex()：返回串的Soundex值
       Substring()：返回子串的字符
       Upper()：将串转化为大写          
       SELECT cust_name,cust_contact FROM customers WHERE Soundx(cust_contact) = Soundex('Y Lie');
    2、日期和时间处理函数
       AddDate() 增加一个日期（天，周等）
       AddTime() 增加一个时间（时，分等）
       CurDate() 返回当前日期
       CurTime() 返回当前时间
       Date() 返回日期时间的的日期部分
       DateDiff() 计算两个日期之差
       Date_Add() 高度灵活的日期运算函数
       Date_Format() 返回一个格式化日期或时间串
       Now() 返回当前日期和时间
       SELECT cust_id,order_num FROM orders WHERE Date(order_date) BETWEEN '2019-07-03' AND '2019-07-04';
       
    3、数值处理函数
        Abs()： 返回一个数的绝对值
        Cos()： 返回一个角度的余弦
        Exp()： 返回一个数的指数值
        Mod()： 返回除操作的余数
        Pi()：  返回圆周率
        Rand()：返回一个随机数字
        Sin()： 返回一个角度的正弦
        Sqrt()：返回一个数的平方根
        Tan()： 返回一个角度的正切                                         
 ##12、汇总数据   
     1、聚集函数
     