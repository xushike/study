# pl/sql
# 一 概述
## 1 简介
## 3 常识
# 三 基础
## 1 语法和子句
### 1.1 增
把查询结果插入:`insert into table value (xxx,xxx,xxx) select xxx,xxx,xxx from xxx`

### 1.2 删
delete from xxx 
### 1.3 改
update xxx set xxx = xxx,xxx= xxx
### 1.4 查
`select * from  xxx`

### 1.5 模糊查询like
`%`表示一个或多个字符,`_`表示一个字符,对于特殊符号可以使用ESCAPE标识符来查找,如`select * from emp where ename like '%*_%' escape '*'`,escape表示*后面的那个符号不当成特殊字符处理，就是查找普通的_符号(待补充)

### 1.5 group by分组
在`group by`子句的字段可以不在`select`后面,但是对于在`select`后面的非组函数字段,则必须在`group by`子句中
1. 按日期分组:`group by char(t.xxx,'yyyy-mm-dd')`

    上面是按日分组.如果是按周分组是`group by char(t.xxx,'yyyy-IW')`,按月分组则是`group by char(t.xxx,'yyyy-mm')`,按季度是`group by char(t.xxx,'yyyy-Q`,按年是`group by char(t.xxx,'yyyy')`

2. 按时间段分组:``
### 1.6 having过滤分组后的结果
放在group by后面

和where的异同:where子句中不能使用组函数,但是having可以;其他情况可以通用,从sql优化角度看,尽量使用where,因为having是先分组再过滤,而where是先过滤再分组
    
### 1.7 order by排序
有个快捷写法:用select后面字段的序号代替字段,比如`select deptno,avg(sal) from emp group by deptno order by 2`,那么里面的2就代表了avg(sal)

### 1.8 EXISTS和NOT EXISTS
Oracle EXISTS条件与子查询结合使用，并且如果子查询返回至少一行，则认为该条符合。它可以在SELECT，INSERT，UPDATE或DELETE语句中使用。

## 2 函数
### 2.1 分组函数(组函数)
常用的有六个:avg,sum,min,max,count,wm_concat(行转列);注意这几个函数都不会计算空值,比如`count(*)`是14,但`count(comm)`可能是10,最佳实践是使用`nvl`函数,如`count(nvl(comm,0))`
1. 组函数的嵌套:可以直接嵌套,比如
```sql
--求部门平均工资的最大值
select max(avg(sal))
from emp
group by deptno
```
其实按我个人不知道的情况下的理解应该是用max函数将整个求平均工资的语句包起来,事实上却不是我想的这样,需要多理解理解这个group by

#### avg
当字段的值为空时不会参与计算

#### wm_concat
行转列,中间用逗号拼接

### 2.2 nvl滤空函数

### 2.3 日期函数
#### ADD_MONTHS(date,number_months):增减月份

### 2.4 字符串相关函数
#### lengthb()和length()
- lengthb():计算string所占的字节长度
- length():计算string所占的字符长度

对于单字节字符,上面两个的结果是一样的;一个汉字在Oracle数据库里占多少字节跟数据库的字符集有关，UTF8时，长度为三;可以用`length(‘string’)=lengthb(‘string’)`判断字符串是否含有中文.
#### Upper(),Lower(),Initcap(),Concat(),Substr(),Replace(),Instr(),Lpad(),Rpad(),Trim()
Lpad():左侧填充

Rpad():右侧填充

Trim():去除首尾空格

### 2.1 decode
流程控制,效果类似于`if else`
1. 可用于`order by`的指定排序,如`order by decode(m.status,10,20,30,90,0,99)`

### 2.2 sum
一般用法:`sum(t.xxx)`

### 2.3 to_char(),to_number(),to_date()
1. number转date:`to_date(20180203,'yyyy-mm-dd')`,后面这个`yyyy-mm-dd`格式不管怎么写,最终转换出来都是类似这样的`2018/2/3`
2. date转char:`to_char(sysdate,'yyyy-mm-dd')`,会被转换成`2018-03-06`

### 2.4 like,instr和substr

`substr(<string>, <start_position> [,length])`:截取字符,注意plsql中所有字符串的第一个位置的index是从1开始,而不是从0开始

`like`用于模糊查询,`instr`用于判断是否包含某字符串,`substr`用于截取字符串;因为like的效率比较低,所以能用后面的情况下尽量用后面的

### 2.5 distinct去重
如果后面跟多个字段就是对多个字段去重,所以想对多个字段中的单个字段去重的话还是用`group by`

## 3 命令行命令
### 3.1 show user:查看当前用户
### 3.2 desc [表名]:查看表结构
### 3.3 host cls:清屏
### 3.4 /:执行上一条语句
### 3.5 a(--append) [xxx]:增加命令,一定要和[xxx]空两个空格以上

## 4 注释
1. 单行注释:`-- xxx`
2. 多行注释:`/* xxx */`

## 5 变量
### 5.1 
#### rownum
(未整理)只用于排序和分页?

# 四 高级

# 五 经验
## 1 总结
1. 在oracle中,很多的问题都是通过子查询解决的

# 六 问题
## 1 已解决
### 1.1 invalid SQL statement
### 1.2 date format picture ends before converting entire input string
`to_date()`格式化日期必须必须必须保证传入的字符串和要转换的格式精确匹配.前面若含有时分秒格式化的时候也必须含有。比如`to_date(‘2015-12-12 12:12:12’,'yyyy/mm/dd hh24:mi:ss')`

### 1.3 invalid user.table.column, table.column, or column specification
一般是列名不对

### 1.4 identifier is too long
标识符太长,超过了oracle限制的30个字符

### 1.5 column not allowed here
传入的值不符合要求,比如值的名字写错了,值的类型不对等.

### 1.6 SQL command not properly ended
一般都是写得不对,比如语法错误,格式错误

## 2 未解决
1. 易百教程:[http://www.yiibai.com/plsql/](http://www.yiibai.com/plsql/)
2. Oracle调优经验
3. 变量的声明
4. job是啥
5. 子查询是啥

6. lengthb(),substrb()

7. 项目中不支持卡号模糊查询,是因为索引的问题?
8. plsql中的冒号表示什么

9. 分析形函数,聚合函数,开窗函数