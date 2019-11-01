# mysql数据库
---

>登录数据库：

```cmd
mysql[.exe] [-hlocalhost] [-p3306] -uroot -p密码
```

> 退出数据库：

```cmd
exit | \q | quit
```

> 乱码问题：

```cmd
set names gbk;
```

<br>

## 增、删、改、查
---

### 增加

> 创建数据库：

```cmd
create database 数据库名 [charset utf8||gbk];
```

> 创建数据表：

```cmd
create table 数据表名(
  字段 类型 属性,
  字段 类型 属性,
  字段 类型 属性
);
```

> 插入数据：

```cmd
insert into 数据表 (字段1，字段2) values (值1，值2);
insert into 数据表 values (按照数据表字段顺序录入);
```

> 复制数据表：

```cmd
create table 新表名 like 旧表名;
```

> 添加字段：

```cmd
alter table 数据表名 add 字段名 类型 属性 [after 字段 | first],
add 字段名 类型 属性 [after 字段 | first];
```

> 给数据表添加主键：

```cmd
alter table 数据表名 modify 字段名 字段类型 [属性 primary key];
或者 alter table 数据表名 add primary key (字段名称);
```

<br>

### 查询

> 查看全部数据库：

```cmd
show databases;
```

> 查询指定的数据库：

```cmd
show databases like “字符串%”;
```

> 查看数据库的创建信息：

```cmd
show create database 数据库名;
```

> 选择数据库：

```cmd
use 数据库名;
```

> 查看数据表：

```cmd
show tables;
show tables from 数据库名;
```

> 查看以指定的数据表：

```cmd
show tables like “字符串%”;
```

> 查看表结构：

```cmd
desc|descril 数据表名;
```

> 查看数据表的创建信息：

```cmd
show create table 数据表名;
show create table 数据表名\G
```

> 查询数据内容：

```cmd
select (字段1,字段2|*) from 数据表名 where(条件);
```

<br>

### 修改

> 修改数据库：

```cmd
alter database 数据库名 charset 新字符集;
```

> 修改数据表：

```cmd
alter table 数据表名 charset 字符集;
```

> 修改数据表名（重名）：

```cmd
alter table 旧表名 rename 新表名;
```

> 修改数据：

```cmd
update 数据表 set 字段1=值1，字段2=值2 where(条件);
```

> 修改字段类型及属性：

```cmd
alter table 数据表名 modify 字段 新类型 新属性;
```

> 修改字段名称（类型及属性）：

```cmd
alter table 数据表名 change 旧字段名 新字段名 类型 属性;
```

<br>

### 删除

> 删除数据库：

```cmd
drop database 数据库名;
```

!> 系统数据库不要删
（information_schema, mysql, performance_schema）

> 删除数据表：

```cmd
drop table 数据表名;
```

> 删除数据：

```cmd
delete from 数据表 where (条件);
```

> 删除字段：

```cmd
alter table 表名 drop 字段;
```

<br>

## 字段类型和属性
---

### 类型

> 数字类型

```
tinyint(-128,127，占1字节)
smallint（正负三万，占2字节）
mediumint（正负八百万，占3字节）
int（正负21亿，占4字节）

float（6,2）（占4字节）
double,双精度浮点数 （占8字节）
decimal,定点型 （M大就占M+2字节，D大就占D+2字节）（M最大65，D最大30，默认10,0）
```

> 字符串类型

```
char(M) 0-255 指定存储长度后，系统分配固定长度，空间浪费，但执行效率高。
varchar(M) 系统先统计长度，然后分配空间。节省空间，但执行速度低。
```

> 枚举类型

```
enum:
字段 enum(“选项1”,”选项2”,”选项3”) not null default “选项n”，
1,2,3
set:
字段 set(“选项1”,”选项2”,”选项3”) not null default 默认值，
1,2,4
```

> 时间类型

```
time（时分秒）（占3字节）
date (年月日)(‘Y-m-d H:i:s’)(占3字节)
datetime (datetime占8字节)
timestamp (timestamp占4字节) 具有自动更新时间及默认值的功能

可以使用now()函数
```

<br>

### 属性

```
null 可以为空！| not null 不能为空值！
default 默认值
primary key 主键，不能为空，字段值不能重复，用来该行的唯一标识。
unique key 唯一键，可以为空，字段值不能重复
comment 字段注释
auto_increment 自动增长
zerofill 零填充 :zerofill就是将空格填充替换为零填充。不足显示宽度使用零在左侧填充。
unsigned 无符号属性 :整型添加unsigned属性后，只能存储无符号数（不能存储负数），最高位为数值位。
```

<br>

### 日期函数

```
now();
time(now()); 当前时分秒
date(now()); 当前年月日
year(now()); 当前年份
datediff(”,”); 两个日期的时间差
date_add(‘2017-3-5’,interval 10 day)
date_sub() 减去多少时间
dayofyear() 返回该日期为当年的第几天
```

<br>

## 修改密码

> 进入mysql数据库

```cmd
use mysql;
```

> 修改root用户和localhost的密码

```cmd
update user set password=password('root') where user='root';
```

> 刷新权限

```cmd
flush privileges;
```

<br>
<br>
<br>

## 练习sql语句
---

```shell
# 查询每位同学的工资和(去重)：
select name,salary+bonus as sum from student;
```

```shell
# 查询每位同学的工资和：基本工资+奖金。需要工资和大于9000: 
select distinct name,salary+bonus as sum from student where salary+bonus > 9000; 
```

```shell
# 学号在20到30之间的学生信息:
select * from student where id >= 20 and id <= 30; 
```

```shell
# 查询女神的信息，条件：山东21岁女青年:
select * from student where sex = '女' and city = '山东省' and age = 21; 
```

```shell
# 每一行都返回true--1--所有行都满足条件：
select * from student where 1; 
```

```shell
# 山东、山西、江西三省学生信息（用in）:
select * from student where city in ('山东省','山西省','江西省'); 
```

```shell
# 年龄为23或25或27的女生：
select * from student where age in (23,25,27) and sex = '女'; 
```

```shell
# 地域学生信息统计（华北地区，京津唐蒙晋）:
select * from student where city in ('北京市','天津市','河北省','内蒙古','山西省'); 
```

```shell
# 地域学生信息统计（非华北地区，除京津唐蒙晋外）:
select * from student where city not in ('北京市','天津市','河北省','内蒙古','山西省'); 
```

```shell
# 90后（18-27）学生姓名、年龄(用between):
select name,age from student where age between 18 and 27; 
```

```shell
# 薪资小于9400或者大于12000之间的同学信息:
select * from student where salary+bonus between 9400 and 12000; 
```

```shell
# 查询没有城市信息的学生:
select * from student where city is null or city = ''; 
```

```shell
# 查询张姓同学信息:
select * from student where name like "张%"; 
```

```shell
# 查询姓名含张字的同学信息
select * from student where name like '%张%'; 
```

```shell
# 查询名字为四个字的同学信息：
select * from student where name like '____'; 
```

```shell
# 聚合函数自动忽略空值--人数统计
select count(*),count(city) from student; 
```

```shell
# 查询数据表中的最高工资,最低工资，平均工资，总工资(所有人的基本工资总和 )；
select max(salary) as max,min(salary) as min,avg(salary) as avg,sum(salary) as sum from student; 
```

```shell
# 查询男生、女生各自的最高工资、最低工资、平均工资、总工资（salary）
select sex,max(salary) as max,min(salary) as min,avg(salary) as avg,sum(salary) as sum from student group by sex; 
```

```shell
# 查询各省份 男生、女生的平均工资 各省份 按照籍贯分组 男生女生 按照性别分组
select city,sex,avg(salary) as avg from student where city is not null and city !='' group by city,sex;
```

```shell
# 统计华北地区的各省份人数  
# '河北省','北京市','天津市','内蒙古','山西省'  
#华北地区 where子句  #各省份 按照籍贯分组
select city,count(*) from student where city in ('北京市','河北省','天津市','内蒙古','山西省') group by city; 
```

```shell
# 回溯合计 ： group by cith with rollup;  
# group_ concat():分组之后，对该组的特定字段值进行拼接返回 
```

```shell
# 统计男生、女生的姓名:
select sex,group_concat(distinct name) from student group by sex; 
```

```shell
# 查询省份平均工资大于10000的省份信息 #分组之后可以获取每组的平均工资进行筛选
select city,avg(salary) from student group by city having avg(salary) > 10000; 
```

```shell
# 平均工资大于10000的‘各城市’的工资的（max,min,avg）值
select city,avg(salary),max(salary),min(salary) from student group by city having avg(salary) > 10000; 
```

```shell
# 学号前5的同学信息
select * from student where id <= 5; 
```

```shell
# order by asc|desc # 学号前20的薪水排行榜
select * from student where id <= 20 order by salary asc;  select * from student where id <= 20 order by salary desc; 
```

```shell
# 各省份平均工资排名榜
select city,avg(salary) from student where city is not null and city != '' group by city order by avg(salary) desc; 
```

```shell
# 学号前20，按工资降序、奖金 降序排列
select id,name,salary,bonus from student where id <= 20 order by salary desc,bonus asc; 
```

```shell
# 工资最高的5位同学信息
select name,salary from student order by salary desc limit 0,5; 
```

```shell
# 每页5行，查询数据表中第三页数据 
select name,salary from student order by salary desc limit 10,5; 
```

```shell
# 每页3行，查询数据表中第6页数据
select name,salary from student order by salary desc limit 15,3; 
```

```shell
# 删除工资小于5000的，且工资最低的5条记录
select name,salary from student where salary<5000 order by salary asc limit 0,5; 
 delete from student where salary <5000 order by salary asc limit 5; 
```

```shell
# 将工资小于4400的最低的1条，工资多加5000
update student set salary = salary + 5000 where salary < 5000 order by salary asc limit 1; 
```

```shell
# 籍贯中含‘西’字的学生学号、姓名、年龄及薪水,籍贯，
select id,name,age,salary+bonus,city from student where city like '%西%'; 
```

```shell
# 需求2：年龄大于35岁的学生学号、姓名、年龄及薪水，籍贯，
select id,name,age,salary+bonus,city from student where age >35; 
```

```shell
# 联合查询：
select id,name,age,salary+bonus,city from student where city like '%西%'
union 
select id,name,age,salary+bonus,city from student where age >35; 
```

```shell
# 结果集排序  
# 需求1：籍贯中含‘西’字的学生学号、姓名、年龄及薪水,籍贯，  
# 需求2：年龄大于35岁的学生学号、姓名、年龄及薪水，籍贯，  
# 对整个结果集进行 工资升序排序
select id,name,age,salary+bonus,city from student where city like '%西%' 
union 
select id,name,age,salary+bonus,city from student where age >35 order by salary+bonus asc; 

select * from student where age between 18 and 27; 
select * from student where salary+bonus not between 10000 and 20000;  
```

```shell
# 回溯统计 with rollup # group_concat() 
select sex,group_concat(name) from student group by sex; 
select city,avg(salary) from student group by city having avg(salary)>10000; 
```

```shell
# 内连接 
# a cross join b a表 任意匹配 b表  
# a inner join b on 连接条件 内连接查询  
# 把apple_c和apple_p连接匹配在一起显示; 
select c.name,p.name,p.price,p.pub_date from apple_c as c inner join apple_p as p on c.id = p.cid; 
```

```shell
# 筛选并匹配students和schools在江西的学生的信息： 
select st.name,st.gender,st.city,sc.school_name from students as st inner join schools as sc on st.school_id = sc.id  where st.city = '江西'; 
```

```shell
# 匹配tb_cat和tb_goods并筛选售价大于4000元的手机； 
select * from tb_cat as cat inner join tb_goods as goods on cat.id = goods.cid 
where market_price > 4000; 
```

```shell
# 匹配stu_info和stu_pays并筛选籍贯为山东并且ID排在前五的工资在5000到10000的女生 
select * from stu_info as i inner join stu_pays as p on i.id = p.id 
where i.city = '山东省' and i.sex = '女' and p.id < 5 and salary+bonus between 5000 and 10000; 
```

```shell
# pid 代表他的上级编号 # 自连接 # 让city自连接，显示城市和上级城市；
select a.name as '城市',b.name as '上级城市' from city as a left join city as b on a.pid = b.id; 
```

```shell
# 查询tb_goods中比苹果7贵的手机 :subquery 子查询 
select * from tb_goods where market_price > (select market_price from tb_goods where name = 'iphone7');
```

```shell
# 查询跟胡歌同一籍贯的女老乡的信息 
select * from student where sex = '女' and city = (select city from student where name ="胡歌"); 
```

```shell
# 显示籍贯为山东省的基本工资高于全国平均工资的全部信息 
select * from student where city = '山东省' and salary > (select avg(salary) from student); 
```

```shell
# 查询计算机系的所有学生信息 
select stu.id,stu.name,stu.gender,stu.city,sch.school_name from students as stu left join schools as sch on stu.school_id = sch.id where stu.school_id = (select sch.id from schools as sch where sch.school_name = '计算机系'); 
```

```shell
#查出“王凯”所在的院系信息。 
select * from schools where id = (select stu.school_id from students as stu where stu.name = '王凯'); 
```

```shell
/**  
* 列子查询  
*/  
#students schools 查出有“河北”人就读的院系信息。
select * from schools where id in (select school_id from students where city = '河北'); 
# students schools查出跟“河北男生”同院系的所有学生的信息。 
select * from students where school_id in (select school_id from students where gender = '男' and city = '河北'); 
```

```shell
-- 以下是student表 #张姓同学老乡信息 
select * from student where city in (select city from student where name like '张%' and city is not null and city != ''); 
```

```shell
#比胡歌，邓超其中一位的工资高的学生信息 
select * from student where salary > (select min(salary) from student where name in ('胡歌','李聪')); 
select * from student where salary > any (select salary from student where name in ('胡歌','李聪')); 
```

```shell
#比胡歌，舒淇，张震工资都高的学生信息 
select * from student where salary > all (select salary from student where name in ('胡歌','李聪')); 
```

```shell
/**  
* 行子查询  
*/  #跟贾原同岁的老乡信息 
select age,city from student where name = '贾原'; 
select * from student where city = (select city from student where name = '贾原') and 
```

```shell
/** 
* 表子查询 
*/  
#查询各省份工资最低的学生信息（不考虑并列的情况） 
select * from (select * from student where city !=''and city is not null order by salary desc) as a group by city;
#查询tb_goods中各分类的价格最高的商品
select * from (select * from tb_goods order by market_price desc) as a group by cid;  
```
