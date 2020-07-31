### mysql if函数

```mysql
# 类似 java中的三元运算符号
select IF(10>5,'da','xiao')

# 查询员工表中 有奖金的并备注
select last_name , commissin ,IF(commissin is null , '有奖金'，'没有奖金') as 备注 
from table

# switch case 表达式
# case 要判断的字段或者表达式
# when 常量1 then 要显示的值1
# when 常量2 then 。。。。
# else 要显示的值或者语句n;
# end
# 查询员工的工资 ， 要求
# 部门号 为 30 显示新工资为1.1倍
# 部门号 为 40 显示为1.2倍
select salary as 原始工资 ,department_id , 
case department_id
when 30 then salary*1.1
when 40 then salary * 1.2
else salary
end as 新工资
from table

# ps 备注 when 后可以跟着 范围 例如
select salary as 原始工资 ,department_id ,
case department_id
when department_id > 30 then salary = salary *10
when department_id < 30 then salary = salary *-1
else salary
end as 新工资
from table

# 多重if
# case
# when 条件1 then 要显示的值 或者语句1
# when 条件2 then 要显示的值 或者语句2
# 和 switch 的 最主要区别是 switch 主要是等值判断 多重if 判断范围值
SELECT student,class,price,success,
CASE
WHEN price > 60 THEN '好学生'
WHEN price < 60 THEN '学渣'
ELSE '及格'
END AS 分类
FROM courses
# 常见单行 函数
# 字符函数
# length 查找 某行的长度
SELECT LENGTH(student) AS len FROM courses
# concat 讲两个字符串连接到一起
SELECT CONCAT(student,price) AS newstar FROM courses;
# substr 截取字符串

# instr INSTR(str,字符串) 第一个参数从哪个字符串中搜索 ，返回值是字符串在str中的哪个位置
# trim 删除指定的字符 leading 删除前面指点的字符
select trim (leading 'x' from 'xxxxxxxaaaa');
-> barxx
# trim 删除指定的字符 both 删除指定的尾部字符
select trim (both 'x' from 'xxxxbbbbxxx');
-> xxxxbbbb
# upper 变大写
# lower 变小写
# lpad lpad：函数语法：lpad(str1,length,str2)。其中str1是第一个字符串，length是结果字符串的长 # 度，str2是一个填充字符串。如果str1的长度没有length那么长，则使用str2填充；如果str1的长度大于
# length，则截断。
select lpad('abcdefghi',8,'abc')
# abcdefghi 十位 多出来两位 截断
-> abcdefg
select lpad('cde',5,'abc')
#长度小于5 添加上
-> abcde
# rpad 类似于 lpad 在右边添加元素
# replace 取代字符
# 数学函数
# round 随机数
# ceil 返回参数的整数
select cell(3.46)
-> 4
# floor
select floor(1.23)
-> 1
select floor(-1.2)
-> -2
# truncate
# mod 取余数
# 日期函数
# now SELECT NOW(),CURDATE(),CURTIME()
# 返回当前时间 ， 返回 当前日期 不包含时分秒， 返回时分秒 不包含 日期
select now() , curdate() , curtime()

# curdate
# curtime
# year
# month
# monthname
# day
# hour
# minute
# second
# str_to_date
# date_format
# 其他函数

# 分组函数，聚合函数，组函数 group by sum avg max min count
group by
# 分组后的筛选用having，分组前的筛选用where
# 分组函数做条件必须要放在having子句中
# 性能分析需要筛选尽量要使用分组前筛选






```

