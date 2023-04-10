========================= 数据库的基本命令 ============================
1.状态和启动命令
	- 查看mysql状态：sudo /etc/init.d/mysql status
	- 启动|停止|重启：sudo /etc/init.d/mysql start|stop|restart

2.客户端连接
	- 命令格式 
		- mysql -h主机地址 -u用户名 -p密码
		- mysql -hlocalhost -uroot -p123456
		- mysql -uroot -p123456(本地可不加-h)
	
3.关闭连接
	- ctrl+D 或  exit
	
4.修改密码
	- ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY '123456';

	
=============================== end ===================================




============================ 数据类型支持 ==============================
1.数字类型
	- 整数类型 (精确值)
		- INTEGER	
		- INT
		- SMALLINT
		- TINYINT    
		- MEDIUMINT
		- BIGINT
		
	- 定点类型 (精确值)
		- DECIMAL
		
	- 浮点类型 (近似值)
		- FLOAT
		- DOUBLE
	
	- 比特类型
		- BIT

2.字符类型
	- CHAR和VARCHAR类型
		- CHAR 	  效率高 定长
		- VARCHAR 效率低 不定长
		
	- BINARY和VARBINARY类型
		- 
	
	- BLOB和TEXT类型
		- BLOB  二进制长文本数据
		- TEXT	长文本数据
		
	- ENUM类型和SET类型
		- ENUM	存储给出的一个值
		- SET	存储给出的一个或多个值
================================ end ==================================




============================= 库的基本操作 =============================
1.库操作
	- 创建数据库：create database 库名[character set utf8];
	- 查看已有库：show databases;
	- 查看库：show create database 库名;
	- 查看当前所在库：select database();
	- 切换数据库：use 库名;
	- 删除数据库：drop database 库名;

================================ end ==================================




============================ 表的基本操作 ==============================
- 表操作
	- 创建表格：create table 表名;
	- 查看已有表格：show tables;
	- 查看表格：show create table 表名;
	- 查看表结构：desc 表名;
	- 删除表格：drop table 表名;
================================ end ==================================




=========================== 数据的基本操作 =============================
1.创建表(制定字符集)
	- create table 表名(
	    字段名   数据类型,
	    字段名   数据类型,
	  ....
	    字段名   数据类型
	  )
	- 字段描述
		- primary key
		- unsigned
		- not null
		- default 
	  
2.插入
	- insert into 表名  values(值1),(值2),...;
	- insert into 表名 (字段1,...) values (值1,...);

3.查询
	- select * from 表名 [where 条件];
	
4.修改(更新表记录)
	- update 表名  set 字段1=值1,字段2=值2,... where 条件;

5.删除记录
	- delete from 表名 where 条件;
	(delete语句后如果不加where条件，所有记录将全部晴空)
	
6.找关键字
	- select 字段名  from 表名 where 字段名 LIKE ...
		- (找出所有name为L开头的记录)
		 	elect * from class_1 where name like 'L%';
		 	
		- (找出interest表中comment包含良好的记录)
			select * from interest where comment like '%良好%';

7.排序
	- ORDER BY (从小到大)
		- select * from class_1 ORDER BY age;(年龄从小到大)
	- DESC (从大到小)
		- select * from class_1 ORDER BY age DESC;

8.限制
	- LIMIT 数量
		- e.g: delete from class_1 where age=17 LIMIT 1;

9.联合查询(可在不同表格联合查询)
	- UNION (除去重复内容)
		- e.g: select * from class_1 where gender = 'w' UNION 
			   select * from class_1 where age > 17;
			   
	- UNION ALL(不除去重复内容)
		- e.g: select * from class_1 where gender = 'w' UNION ALL
			   select * from class_1 where age > 17;
			   
================================ end ===================================




============================ 表字段的操作 ===============================
- 语法：alter table 表名 执行动作;
	- 添加字段(add)
		- alter table 表名 add 字段名 数据类型;
		- alter table 表名 add 字段名 数据类型   first;(第一行)
		- alter table 表名 add 字段名 数据类型   after 字段名;(在某一个字段的后面)
		
	- 删除字段(drop)
		- alter table 表名  drop 字段名;
	
	- 修改数据类型(modify)
		- alter table 表名 modify 字段名 新数据类型;
		
	- 修改字段名(change)
		- alter table 表名 change 旧字段名 新字段名 新数据类型;
		
	- 表重命名(rename)
		- alter table 表名 rename 新表名;
================================ end ===================================
	
	
	
	
================================ 时间 ===================================	
1.时间和日期类型
	- DATE DATETIME TIMESTRMP类型
	- TIME类型
	- YEAR年份类型

2.日期时间函数(可比较大小)
	- now()		 返回服务器当前时间	e.g: 2023-04-06 17:33:08
	- curdate()	 返回当前日期		e.g: 2023-04-06
	- curtime()  返回当前时间		e.g: 2023-04-06 17:37:56
	- date(date) 返回指定时间的日期	
	- time(date) 返回指定时间的时间
3.间隔(interval)
	- e.g: select * from marathon where 成绩 > (time('03:00:00')-interval 30 minute);
		(找出时间大于2小时30分钟的记录)
	- e.g: select * from marathon where 报名时间 > (now()-interval 7 day);
		(找出时间在一个星期之内的记录)
================================= end ===================================




=============================== 数据备份 =================================
1.备份命令格式
	- mysqldump -u用户名 -p源库名 > ~/***.sql
		- --all-databases 备份所有库
		- 库名 备份单个库
		- -B 库1 库2... 备份指定库
		- 库名 表1 表2... 备份指定库里指定的表
		
2.恢复命令格式
	- mysql -u用户名 -p源库名 < ***.sql

================================= end ===================================






































			
			
