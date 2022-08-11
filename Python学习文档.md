# Python学习文档

## python语言基础

### 运算符

记忆点：

逻辑运算符：and 、or

a and b 如果a为flase，则返回false，否则返回b的值

a or b 如果a为true，则返回a的值，否则返回b的值

成员运算符： in 、not in

判断列表或者字符串中是否有某个元素

==符的特殊点：

a==b==c 等效于 （a==b）and （b==c）

is和 == 的区别：

is：判断a对象是否是b对象

==：判断a对象和b对象的值是否相等

拓展：

二进制乘除法

假设不能使用乘除运算求a×b的结果，当a=b=123时，最直接的方法是通过88个88相加。但是，我们不难发现这样的规律：
123 × 123 = （100+20+3）×123 = （100×123） + （20 × 123） + （3 × 123）
因此，我们需要进行计算的次数为min(len(a), len(b))。
根据这个原理，不难想出二进制的乘法运算：
0011 * 1001 = ( 0011 * 1000)+( 0011 * 0001)
注意，这时应该使用位移运算来取代乘法运算：
0011*1000 => 3<<3
0011 * 0001 => 3<<0

二进制乘法：

```
//不用乘除做整数乘法运算
def Mult(a, b):
	ans = 0;
	for i in range(32):
		if b&(1<<i):
			ans+=a<<i
		else:
			ans+=0
	return ans;


```

二进制除法



![image-20220404104451830](https://s2.loli.net/2022/04/04/hQxD59ez2JwmE1q.png)

ps:表格第四行应该为1001

```
//二进制除法运算
def Dvi(a, b):
	ans = 0;
	for j in range(31,-1,-1):
		tmp=a>>j
		if tmp>=b:
			ans=ans|(1<<j)
			a-=(b<<j)
	return ans
```



### 数据类型

#### 可变数据类型（可以修改当前对象的值）

##### 列表

列表与其他类型的转化

```python
set(list)
#列表转集合

list1=[1,2]
list2=['a','b']
dict1=dict(zip(list1,list2))
#dict1:{1: 'a', 2: 'a'} 列表转字典
#列表转字符串
str.join(list1)
#字典value和key互换
dict1={'1':'a','2':'b'}
{value:key for key,value in a_dict.items()}
```

列表中删除重复元素

```python
#1.使用set
list1=[1,1,2,2,3,3]
list2=list(set(list1))
#2. 字典法
list3=list({}.formkeys(list1).keys()) 或者 list({}.formkeys(list1))
#3.for 循环法，就是遍历，不多加赘述
```

列表求交集并集差集

```python
#for 循环法
#交集
a=[1,2,3]
b=[2,3,4]
result=[r for r in a if r in b]
print('a和b的交集',result)
result=[r for r in a if r not in b]
print('a和b的差集'，result)
result=a
for r in b:
	if r not in result:
		result.append(r);
print('a和b的并集'，result)
#集合法（集合有自带求交并差集的函数）
result=list(set(a).intersection(set(b))
print('交集： '，result)
result=list(set(a).difference(set(b))
print('差集： '，result)
result=list(set(a).union(set(b)))
print('并集： '，result)
```

列表合并（合在一起，不是并集，集合不可以重复）

```python
#+号合并
a=[1,2,3]
b=['a','b']
c=a+b
print(c)
# extend合并
c=a.extend(b)
c.sort()
print(c)
```

列表倒序遍历

```python
#reversed()方法
seq='Hello World!'
for s in reversed(seq):
	print(s,end='')
print()
#range函数方法 注：range需要倒序的话需要追加参数-1
for i in range(len(seq)-1,-1,-1):
	print(seq[i],end='')
print()
#[::-1]扩展切片法
for s in seq[::-1]:
`	print(s,end='')
print()
#list自带reverse方法 注：reverse函数无返回值
list1=[1,2,3,4,5,6]
list1.reverse()
print(list2)
```

列表排序

```python
#list.sort()对列表排序
seq=[1,3,4,2,5,6]
print('原来的序列'，seq)
seq.sort()
print('排序的序列'，seq)
#list,sorted()对列表排序 原来的序列不变
seq=[1,3,2,5,4,6]
print('原来的序列',seq)
s=sorted(seq)
print('排序的序列',s)
#使用lambda对嵌套列表进行排序
list1=[[1,2],[2,3],[3,4]]
list1.sort(key=lambda x:x[0],reverse=True)
print(list1)
list1.sort(key=lambda x:x[1],reverse=True)
print(list1)
#lambda 可以对列表排序进行选择或者设置优先级，例如正数从大到小，负数从小到大
foo=[["zs",19],["I",54],["wa",23],["df",23],["xf" ,23]]
foo.sort(key=lambda x:(x[1],x[0]),reverse=True)
print(foo)
```

![image-20220207132958909](https://s2.loli.net/2022/02/07/518WIwiHuor4vqA.png)

list的常用方法

列表生成式 ：[表达式 for循环]

```python
#使用列表生成一个1-11的平方式
l2=[x*x for x in range(1,11)]
print(l2)
# 对偶数取平方
l3=[x*x for x in range(1,11) if x%2==0]
print(l3)

#拓展 生成器
l4=(x*x for x in range(1,11))
print(l4)
for i in l4:
    print(i)
#使用生成器直接输出会输出生成器的信息
#<generator object <genexpr> at 0x000001C032459740>
#需要使用for循环输出
```

注：a[::2]为间隔2取列表元素

##### 集合

![image-20220207141447113](https://s2.loli.net/2022/02/07/EigP2SazFjUrI9W.png)

集合查看不同的元素和相同的元素

```python
a=[1,2,3]
b=[2,3,4]
list1=list(set(a)&set(b))
list2=list(set(a)^set(b))
print('相同元素：{}'.format(list1))
print('不同元素：{}'.format(list2))
```



##### 字典

字典排序

```
a=[{'name':'a','age':20},{'name':'b','age':50},{'name':'d','age':40}]
print(sorted(a,key=lambda x:x['age'],reverse=True))
```

 按照value排序

```
d={'a':24,'g':52,'T':12,'k':33}
print(sorted(d.items(),key = lambda x:x[1]))
```

字典内置函数

![image-20220207140128205](https://s2.loli.net/2022/02/07/oCb2r3he1g7uWAM.png)

字典的删除方法

```
#pop
dic={'name':'Stevin','age':100}
dic1=dic
dic.pop('name')
#del
print(dic)
del dic1['name']
print(dic1)
```

json与字典的区别：json必须都是字符串，字典不需要

json.dumps() 可以让字典转json，json.load()可以让json转字典

给定字典或者列表，找到其中最大的N个值（使用headq的nlargest）找到最小值（使用headq的nsmallest）

```python
import heapq
portfolio=[
{'name':'IBM', 'shares': 100, 'price':91.13},{'name': 'AAPL', 'shares': 50, 'price': 543.223},{'name':'FB', 'shares': 200,'price': 21.09},{'name':'HPQ','shares': 35, 'price': 31.75},{'name':'YHO0','shares': 45, 'price': 16.35},{'name': 'ACME', 'shares': 75, 'price':115.65}]
#参数3为最大的3个值(最小的3个值)
cheap = heapq.nsmallest(3, portfolio,key=lambda s: s['price'])
expensive=heapq.nlargest(3, portfolio, key=lambda s: s['price'])
#上面代码在对每个元素进行对比的时候，会以 price的值进行比较。
print(cheap)
print(expensive)
#时间复杂度O（
```



#### 不可变数据类型（更改值相当于重新创建对象）

##### 字符串

删除字符串末尾空白函数：rstrip()（暂时性的删除）

删除字符串开始空白函数：lstrip()

删除字符串两端空白函数：strip()

（三者用法一致）

```python
name="python "
name.rstrip()
>>>'python'
name
>>>'python '
```

字符串逆序输出

```
#切片法
name='abcdefg'
print(name[::-1])
#转化为列表
name1=list(name)
name1.reverse()
print(''.join(name1))

```

字符串排序

```python
seq='125678'
s==sorted(seq)
print('原来的序列',seq)
print('排序的字符串',"".join(s))
```

字符串格式化

```
#%的格式化
c=(250,250)
s1='坐标：%s'%(c,)
print(s1)
#format的格式化
s1='坐标:{}'.format(c)
print(s1)
#format可以挑选参数位置
x='{0}，{1}虎年快乐！'.format('伟杰','啊达')
print(x)
x='{1}，{0}虎年快乐！'.format('伟杰','啊达')
print(x)
```

![image-20220207135727894](https://s2.loli.net/2022/02/07/rALV3sJbFnpjNTl.png)

![image-20220207135918074](https://s2.loli.net/2022/02/07/8GvznYcrTLyHU6u.png)

回文字符串判断

```
def converted(s):
	ss=s[:]
	if len(ss)>=2 and s==ss[::-1]:
		return True
	else:
		return False
```

字符串去除指定字符

```
#空格
str='hello world!'
res=str.replace(' ','')
print(str,res)
list=str.spilt(' ','')
res=''.join(list)
print(str,res)
```

使用ord函数可以获得字符串的ASCII码值

使用chr函数可以获得ASCII对应的字符

##### 元组

##### 数值

整型：支持加减乘除运输，位运算

浮点数：浮点数的小数位数不确定

浮点数的精确：round函数

使用：

```Shell
>>> x=3.1495926
>>> y=round(x,3)
>>> y
3.15
#四舍五入使用
print("%.xf"%x)
```

最大公约数算法

```
#数学约法
def max_yue_num(a,b):
	x,y=int(a),int(b)
	c=x%y
	while c:
		x,y=y,c
		c=x%y
	print(y)
#遍历法
def max_yue_num2(a,b):
	x,y=int(a),int(b)
	min=y if x>y else x
	max=1
	for i in range(min+1):
		if x%i==0 and y%i==0:
			max=i
	print(max)
```

最小公倍数算法

```python
def min_bei_num(a,b):
	x,y=int(a),int(b)
	max=x if x>y else y
	ans=0
	while(True):
		if max%x==0 or max%y==0:
			ans=max
			break
		max+=1
	print(ans)
#最大公约数法
def min_bei_num(a,b):
	x,y=int(a),int(b)
	ans=x_yue_num(x,y)
	return (max(x,y)//ans)*min(x,y)
```

进制转换函数

![img](https://s2.loli.net/2022/04/04/H8qY6uefTGDMZc4.png)

#### 时间

![image-20220207194001780](https://s2.loli.net/2022/02/07/2f74VLacp8ZU9gD.png)

![image-20220207194025150](https://s2.loli.net/2022/02/07/UJ2lxPu6LVNvaWt.png)

```python
import time

localtime=time.asctime(time.localtime(time.time()))
print('本地时间为：',localtime)
#格式化成Sat Mar 28 22:24:24 2016 形式
print(time.strftime("%a%b%d%H%M%S",time.localtime()))
print(time.ctime())

#格式化成2016-03-20 11:45:39 形式
print(time.strftime("%Y-%m-%d %H:%M:%S",time.localtime()))
print(time.strftime("%Y-%m-%d %H:%M:%S"))#当前时间转为字符串
print(time.strftime("%Y-%m-%d %X"))#将当前时间转为字符串

import datetime
print(datetime.datetime.now())
from datetime import datetime,timedelta
dt_now=datetime.now()
print(dt_now)

print(dt_now.date()) #得到日期
print(dt_now.time()) #得到时间
print(dt_now.timestamp()) #得到时间戳

#格式化为指定格式的字符串
print(dt_now.strftime('%Y-%m-%d %X'))
#时间格式字符串转为时间
d1=datetime.strptime("2018-03-05 23:59:59",'%Y-%m-%d %H:%M:%S')
print(d1)

```

返回昨天

```
import datetime
def getYesterday():
	today=datetime.date.today()
	oneday=datetime.timedelta(days=1)
	return today-oneday
print(getYesterday)
```

计算月的天数

```
import calendar
monthRange=calendar.monthrange(2013,,1)
print(monthRange)
```

### shell脚本

打开终端，创建一个sh文件就可以编写

shell变量

命名规则：

- 命名只能使用英文字母，数字和下划线，首个字符不能以数字开头。
- 中间不能有空格，可以使用下划线 _。
- 不能使用标点符号。
- 不能使用bash里的关键字（可用help命令查看保留关键字）。

使用变量：

```shell
your_name="qinjx"
echo $your_name
echo ${your_name}
```

变量名外面的花括号是可选的，加不加都行，加花括号是为了帮助解释器识别变量的边界，比如下面这种情况：

```shell
for skill in Ada Coffe Action Java; do
    echo "I am good at ${skill}Script"
done
```

变量可以重新定义

readonly可以设置变量为只读变量

```shell
#!/bin/bash
myUrl="https://www.google.com"
readonly myUrl
myUrl="https://www.runoob.com"
```

这样执行会出错

使用unset命令可以删除变量

```
unset variable_name
```

```shell
#!/bin/sh
myUrl="https://www.runoob.com"
unset myUrl
echo $myUrl
```

执行得到结果，不会有输出

### 变量类型

运行shell时，会同时存在三种变量：

- 1) 局部变量 局部变量在脚本或命令中定义，仅在当前shell实例中有效，其他shell启动的程序不能访问局部变量。
- 2) 环境变量 所有的程序，包括shell启动的程序，都能访问环境变量，有些程序需要环境变量来保证其正常运行。必要的时候shell脚本也可以定义环境变量。
- 3) shell变量 shell变量是由shell程序设置的特殊变量。shell变量中有一部分是环境变量，有一部分是局部变量，这些变量保证了shell的正常运行

### Shell 字符串

字符串是shell编程中最常用最有用的数据类型（除了数字和字符串，也没啥其它类型好用了），字符串可以用单引号，也可以用双引号，也可以不用引号。

#### 单引号

```
str='this is a string'
```

单引号字符串的限制：

- 单引号里的任何字符都会原样输出，单引号字符串中的变量是无效的；
- 单引号字串中不能出现单独一个的单引号（对单引号使用转义符后也不行），但可成对出现，作为字符串拼接使用。

#### 双引号

```
your_name="runoob"
str="Hello, I know you are \"$your_name\"! \n"
echo -e $str
```

输出结果为：

```
Hello, I know you are "runoob"! 
```

双引号的优点：

- 双引号里可以有变量
- 双引号里可以出现转义字符

#### 拼接字符串

```
your_name="runoob"
# 使用双引号拼接
greeting="hello, "$your_name" !"
greeting_1="hello, ${your_name} !"
echo $greeting  $greeting_1
# 使用单引号拼接
greeting_2='hello, '$your_name' !'
greeting_3='hello, ${your_name} !'
echo $greeting_2  $greeting_3
```

输出结果为：

```
hello, runoob ! hello, runoob !
hello, runoob ! hello, ${your_name} !
```

#### 获取字符串长度

```
string="abcd"
echo ${#string} #输出 4
```

#### 提取子字符串

以下实例从字符串第 2 个字符开始截取 4 个字符：

```
string="runoob is a great site"
echo ${string:1:4} # 输出 unoo
```

注意：第一个字符的索引值为 0。

#### 查找子字符串

查找字符 i 或 o 的位置(哪个字母先出现就计算哪个)：

```
string="runoob is a great site"
echo `expr index "$string" io`  # 输出 4
```

注意： 以上脚本中 ` 是反引号，而不是单引号 '，不要看错了哦。

### Shell 数组

bash支持一维数组（不支持多维数组），并且没有限定数组的大小。

类似于 C 语言，数组元素的下标由 0 开始编号。获取数组中的元素要利用下标，下标可以是整数或算术表达式，其值应大于或等于 0。

#### 定义数组

在 Shell 中，用括号来表示数组，数组元素用"空格"符号分割开。定义数组的一般形式为：

```
数组名=(值1 值2 ... 值n)
```

例如：

```
array_name=(value0 value1 value2 value3)
```

或者

```
array_name=(
value0
value1
value2
value3
)
```

还可以单独定义数组的各个分量：

```
array_name[0]=value0
array_name[1]=value1
array_name[n]=valuen
```

可以不使用连续的下标，而且下标的范围没有限制。

#### 读取数组

读取数组元素值的一般格式是：

```
${数组名[下标]}
```

例如：

```
valuen=${array_name[n]}
```

使用 @ 符号可以获取数组中的所有元素，例如：

```
echo ${array_name[@]}
```

#### 获取数组的长度

获取数组长度的方法与获取字符串长度的方法相同，例如：

```shell

# 取得数组元素的个数
length=${#array_name[@]}
# 或者
length=${#array_name[*]}
# 取得数组单个元素的长度
lengthn=${#array_name[n]}
```

### Shell 注释

以 # 开头的行就是注释，会被解释器忽略。

通过每一行加一个 # 号设置多行注释，像这样：

```
#--------------------------------------------
# 这是一个注释
# author：菜鸟教程
# site：www.runoob.com
# slogan：学的不仅是技术，更是梦想！
#--------------------------------------------
##### 用户配置区 开始 #####
#
#
# 这里可以添加脚本描述信息
# 
#
##### 用户配置区 结束  #####
```

如果在开发过程中，遇到大段的代码需要临时注释起来，过一会儿又取消注释，怎么办呢？

每一行加个#符号太费力了，可以把这一段要注释的代码用一对花括号括起来，定义成一个函数，没有地方调用这个函数，这块代码就不会执行，达到了和注释一样的效果。

#### 多行注释

多行注释还可以使用以下格式：

```
:<<EOF
注释内容...
注释内容...
注释内容...
EOF
```

EOF 也可以使用其他符号:

```
:<<'
注释内容...
注释内容...
注释内容...
'

:<<!
注释内容...
注释内容...
注释内容...
!
```

### Shell 传递参数

我们可以在执行 Shell 脚本时，向脚本传递参数，脚本内获取参数的格式为：$n。n 代表一个数字，1 为执行脚本的第一个参数，2 为执行脚本的第二个参数，以此类推……

#### 实例

以下实例我们向脚本传递三个参数，并分别输出，其中 $0 为执行的文件名（包含文件路径）：

```
#!/bin/bash*
*# author:菜鸟教程*
*# url:www.runoob.com*

echo "Shell 传递参数实例！";
echo "执行的文件名：$0";
echo "第一个参数为：$1";
echo "第二个参数为：$2";
echo "第三个参数为：$3";
```

为脚本设置可执行权限，并执行脚本，输出结果如下所示：

```
$ chmod +x test.sh 
$ ./test.sh 1 2 3
Shell 传递参数实例！
执行的文件名：./test.sh
第一个参数为：1
第二个参数为：2
第三个参数为：3
```

另外，还有几个特殊字符用来处理参数：

| 参数处理 | 说明                                                         |
| :------- | :----------------------------------------------------------- |
| $#       | 传递到脚本的参数个数                                         |
| $*       | 以一个单字符串显示所有向脚本传递的参数。 如"$*"用「"」括起来的情况、以"$1 $2 … $n"的形式输出所有参数。 |
| $$       | 脚本运行的当前进程ID号                                       |
| $!       | 后台运行的最后一个进程的ID号                                 |
| $@       | 与$*相同，但是使用时加引号，并在引号中返回每个参数。 如"$@"用「"」括起来的情况、以"$1" "$2" … "$n" 的形式输出所有参数。 |
| $-       | 显示Shell使用的当前选项，与[set命令](https://www.runoob.com/linux/linux-comm-set.html)功能相同。 |
| $?       | 显示最后命令的退出状态。0表示没有错误，其他任何值表明有错误。 |

#### 实例

```
#!/bin/bash*
*# author:菜鸟教程*
*# url:www.runoob.com*

echo "Shell 传递参数实例！";
echo "第一个参数为：$1";

echo "参数个数为：$#";
echo "传递的参数作为一个字符串显示：$*";
```

执行脚本，输出结果如下所示：

```
$ chmod +x test.sh 
$ ./test.sh 1 2 3
Shell 传递参数实例！
第一个参数为：1
参数个数为：3
传递的参数作为一个字符串显示：1 2 3
```

$* 与 $@ 区别：

- 相同点：都是引用所有参数。
- 不同点：只有在双引号中体现出来。假设在脚本运行时写了三个参数 1、2、3，，则 " * " 等价于 "1 2 3"（传递了一个参数），而 "@" 等价于 "1" "2" "3"（传递了三个参数）。

#### 实例

```shell
#!/bin/bash*
*# author*

*hor:菜鸟教程*
*# url:www.runoob.com*

echo "-- \$* 演示 ---"
for i in "$*"; do
  echo $i
done

echo "-- \$@ 演示 ---"
for i in "$@"; do
echo $i
done
```

### Shell 基本运算符

Shell 和其他编程语言一样，支持多种运算符，包括：

- 算数运算符
- 关系运算符
- 布尔运算符
- 字符串运算符
- 文件测试运算符

原生bash不支持简单的数学运算，但是可以通过其他命令来实现，例如 awk 和 expr，expr 最常用。

expr 是一款表达式计算工具，使用它能完成表达式的求值操作。

例如，两个数相加(注意使用的是反引号 \`\ 而不是单引号 \'\)：

#### 实例

```
#!/bin/bash*

val=`expr 2 + 2`
echo "两数之和为 : $val"
```

执行脚本，输出结果如下所示：

```
两数之和为 : 4
```

两点注意：

- 表达式和运算符之间要有空格，例如 2+2 是不对的，必须写成 2 + 2，这与我们熟悉的大多数编程语言不一样。
- 完整的表达式要被 ` ` 包含，注意这个字符不是常用的单引号，在 Esc 键下边。

------

#### 算术运算符

下表列出了常用的算术运算符，假定变量 a 为 10，变量 b 为 20：

| 运算符 | 说明                                          | 举例                          |
| :----- | :-------------------------------------------- | :---------------------------- |
| +      | 加法                                          | `expr $a + $b` 结果为 30。    |
| -      | 减法                                          | `expr $a - $b` 结果为 -10。   |
| *      | 乘法                                          | `expr $a \* $b` 结果为  200。 |
| /      | 除法                                          | `expr $b / $a` 结果为 2。     |
| %      | 取余                                          | `expr $b % $a` 结果为 0。     |
| =      | 赋值                                          | a=$b 把变量 b 的值赋给 a。    |
| ==     | 相等。用于比较两个数字，相同则返回 true。     | [ $a == $b ] 返回 false。     |
| !=     | 不相等。用于比较两个数字，不相同则返回 true。 | [ $a != $b ] 返回 true。      |

注意：条件表达式要放在方括号之间，并且要有空格，例如: [$a==$b] 是错误的，必须写成 [ $a == $b ]。

算术运算符实例如下：

```
#!/bin/bash*
*# author:菜鸟教程*
*# url:www.runoob.com*

a=10
b=20

val=`expr $a + $b`
echo "a + b : $val"

val=`expr $a - $b`
echo "a - b : $val"

val=`expr $a \* $b`
echo "a * b : $val"

val=`expr $b / $a`
echo "b / a : $val"

val=`expr $b % $a`
echo "b % a : $val"

if [ $a == $b ]
then
  echo "a 等于 b"
fi
if [ $a != $b ]
then
  echo "a 不等于 b"
fi
```

执行脚本，输出结果如下所示：

```
a + b : 30
a - b : -10
a * b : 200
b / a : 2
b % a : 0
a 不等于 b
```

> 注意：
>
> - 乘号(*)前边必须加反斜杠(\)才能实现乘法运算；
> - if...then...fi 是条件语句，后续将会讲解。
> - 在 MAC 中 shell 的 expr 语法是：$((表达式))，此处表达式中的 "*" 不需要转义符号 "\" 。

------

#### 关系运算符

关系运算符只支持数字，不支持字符串，除非字符串的值是数字。

下表列出了常用的关系运算符，假定变量 a 为 10，变量 b 为 20：

| 运算符 | 说明                                                  | 举例                       |
| :----- | :---------------------------------------------------- | :------------------------- |
| -eq    | 检测两个数是否相等，相等返回 true。                   | [ $a -eq $b ] 返回 false。 |
| -ne    | 检测两个数是否不相等，不相等返回 true。               | [ $a -ne $b ] 返回 true。  |
| -gt    | 检测左边的数是否大于右边的，如果是，则返回 true。     | [ $a -gt $b ] 返回 false。 |
| -lt    | 检测左边的数是否小于右边的，如果是，则返回 true。     | [ $a -lt $b ] 返回 true。  |
| -ge    | 检测左边的数是否大于等于右边的，如果是，则返回 true。 | [ $a -ge $b ] 返回 false。 |
| -le    | 检测左边的数是否小于等于右边的，如果是，则返回 true。 | [ $a -le $b ] 返回 true。  |

关系运算符实例如下：

```
#!/bin/bash*
*# author:菜鸟教程*
*# url:www.runoob.com*

a=10
b=20

if [ $a -eq $b ]
then
  echo "$a -eq $b : a 等于 b"
else
  echo "$a -eq $b: a 不等于 b"
fi
if [ $a -ne $b ]
then
  echo "$a -ne $b: a 不等于 b"
else
  echo "$a -ne $b : a 等于 b"
fi
if [ $a -gt $b ]
then
  echo "$a -gt $b: a 大于 b"
else
  echo "$a -gt $b: a 不大于 b"
fi
if [ $a -lt $b ]
then
  echo "$a -lt $b: a 小于 b"
else
  echo "$a -lt $b: a 不小于 b"
fi
if [ $a -ge $b ]
then
  echo "$a -ge $b: a 大于或等于 b"
else
  echo "$a -ge $b: a 小于 b"
fi
if [ $a -le $b ]
then
  echo "$a -le $b: a 小于或等于 b"
else
  echo "$a -le $b: a 大于 b"
fi
```

执行脚本，输出结果如下所示：

```
10 -eq 20: a 不等于 b
10 -ne 20: a 不等于 b
10 -gt 20: a 不大于 b
10 -lt 20: a 小于 b
10 -ge 20: a 小于 b
10 -le 20: a 小于或等于 b
```

------

#### 布尔运算符

下表列出了常用的布尔运算符，假定变量 a 为 10，变量 b 为 20：

| 运算符 | 说明                                                | 举例                                     |
| :----- | :-------------------------------------------------- | :--------------------------------------- |
| !      | 非运算，表达式为 true 则返回 false，否则返回 true。 | [ ! false ] 返回 true。                  |
| -o     | 或运算，有一个表达式为 true 则返回 true。           | [ $a -lt 20 -o $b -gt 100 ] 返回 true。  |
| -a     | 与运算，两个表达式都为 true 才返回 true。           | [ $a -lt 20 -a $b -gt 100 ] 返回 false。 |

布尔运算符实例如下：

```
#!/bin/bash*
*# author:菜鸟教程*
*# url:www.runoob.com*

a=10
b=20

if [ $a != $b ]
then
  echo "$a != $b : a 不等于 b"
else
  echo "$a == $b: a 等于 b"
fi
if [ $a -lt 100 -a $b -gt 15 ]
then
  echo "$a 小于 100 且 $b 大于 15 : 返回 true"
else
  echo "$a 小于 100 且 $b 大于 15 : 返回 false"
fi
if [ $a -lt 100 -o $b -gt 100 ]
then
  echo "$a 小于 100 或 $b 大于 100 : 返回 true"
else
  echo "$a 小于 100 或 $b 大于 100 : 返回 false"
fi
if [ $a -lt 5 -o $b -gt 100 ]
then
  echo "$a 小于 5 或 $b 大于 100 : 返回 true"
else
  echo "$a 小于 5 或 $b 大于 100 : 返回 false"
fi

```

执行脚本，输出结果如下所示：

```
10 != 20 : a 不等于 b
10 小于 100 且 20 大于 15 : 返回 true
10 小于 100 或 20 大于 100 : 返回 true
10 小于 5 或 20 大于 100 : 返回 false
```

------

#### 逻辑运算符

以下介绍 Shell 的逻辑运算符，假定变量 a 为 10，变量 b 为 20:

| 运算符 | 说明       | 举例                                       |
| :----- | :--------- | :----------------------------------------- |
| &&     | 逻辑的 AND | [[ $a -lt 100 && $b -gt 100 ]] 返回 false  |
| \|\|   | 逻辑的 OR  | [[ $a -lt 100 \|\| $b -gt 100 ]] 返回 true |

逻辑运算符实例如下：

```
#!/bin/bash*
*# author:菜鸟教程*
*# url:www.runoob.com*

a=10
b=20

if [[ $a -lt 100 && $b -gt 100 ]]
then
  echo "返回 true"
else
  echo "返回 false"
fi

if [[ $a -lt 100 || $b -gt 100 ]]
then
  echo "返回 true"
else
  echo "返回 false"
fi


```

执行脚本，输出结果如下所示：

```
返回 false
返回 true
```

------

#### 字符串运算符

下表列出了常用的字符串运算符，假定变量 a 为 "abc"，变量 b 为 "efg"：

| 运算符 | 说明                                         | 举例                     |
| :----- | :------------------------------------------- | :----------------------- |
| =      | 检测两个字符串是否相等，相等返回 true。      | [ $a = $b ] 返回 false。 |
| !=     | 检测两个字符串是否不相等，不相等返回 true。  | [ $a != $b ] 返回 true。 |
| -z     | 检测字符串长度是否为0，为0返回 true。        | [ -z $a ] 返回 false。   |
| -n     | 检测字符串长度是否不为 0，不为 0 返回 true。 | [ -n "$a" ] 返回 true。  |
| $      | 检测字符串是否为空，不为空返回 true。        | [ $a ] 返回 true。       |

字符串运算符实例如下：

```
#!/bin/bash*
*# author:菜鸟教程*
*# url:www.runoob.com*

a="abc"
b="efg"

if [ $a = $b ]
then
  echo "$a = $b : a 等于 b"
else
  echo "$a = $b: a 不等于 b"
fi
if [ $a != $b ]
then
  echo "$a != $b : a 不等于 b"
else
  echo "$a != $b: a 等于 b"
fi
if [ -z $a ]
then
  echo "-z $a : 字符串长度为 0"
else
  echo "-z $a : 字符串长度不为 0"
fi
if [ -n "$a" ]
then
  echo "-n $a : 字符串长度不为 0"
else
  echo "-n $a : 字符串长度为 0"
fi
if [ $a ]
then
  echo "$a : 字符串不为空"
else
  echo "$a : 字符串为空"
fi


```

执行脚本，输出结果如下所示：

```
abc = efg: a 不等于 b
abc != efg : a 不等于 b
-z abc : 字符串长度不为 0
-n abc : 字符串长度不为 0
abc : 字符串不为空
```

------

#### 文件测试运算符

文件测试运算符用于检测 Unix 文件的各种属性。

属性检测描述如下：

| 操作符  | 说明                                                         | 举例                      |
| :------ | :----------------------------------------------------------- | :------------------------ |
| -b file | 检测文件是否是块设备文件，如果是，则返回 true。              | [ -b $file ] 返回 false。 |
| -c file | 检测文件是否是字符设备文件，如果是，则返回 true。            | [ -c $file ] 返回 false。 |
| -d file | 检测文件是否是目录，如果是，则返回 true。                    | [ -d $file ] 返回 false。 |
| -f file | 检测文件是否是普通文件（既不是目录，也不是设备文件），如果是，则返回 true。 | [ -f $file ] 返回 true。  |
| -g file | 检测文件是否设置了 SGID 位，如果是，则返回 true。            | [ -g $file ] 返回 false。 |
| -k file | 检测文件是否设置了粘着位(Sticky Bit)，如果是，则返回 true。  | [ -k $file ] 返回 false。 |
| -p file | 检测文件是否是有名管道，如果是，则返回 true。                | [ -p $file ] 返回 false。 |
| -u file | 检测文件是否设置了 SUID 位，如果是，则返回 true。            | [ -u $file ] 返回 false。 |
| -r file | 检测文件是否可读，如果是，则返回 true。                      | [ -r $file ] 返回 true。  |
| -w file | 检测文件是否可写，如果是，则返回 true。                      | [ -w $file ] 返回 true。  |
| -x file | 检测文件是否可执行，如果是，则返回 true。                    | [ -x $file ] 返回 true。  |
| -s file | 检测文件是否为空（文件大小是否大于0），不为空返回 true。     | [ -s $file ] 返回 true。  |
| -e file | 检测文件（包括目录）是否存在，如果是，则返回 true。          | [ -e $file ] 返回 true。  |

其他检查符：

- -S: 判断某文件是否 socket。
- -L: 检测文件是否存在并且是一个符号链接。

变量 file 表示文件 /var/www/runoob/test.sh，它的大小为 100 字节，具有 rwx 权限。下面的代码，将检测该文件的各种属性：

```
#!/bin/bash*
*# author:菜鸟教程*
*# url:www.runoob.com*

file="/var/www/runoob/test.sh"
if [ -r $file ]
then
  echo "文件可读"
else
  echo "文件不可读"
fi
if [ -w $file ]
then
  echo "文件可写"
else
  echo "文件不可写"
fi
if [ -x $file ]
then
  echo "文件可执行"
else
  echo "文件不可执行"
fi
if [ -f $file ]
then
  echo "文件为普通文件"
else
  echo "文件为特殊文件"
fi
if [ -d $file ]
then
  echo "文件是个目录"
else
  echo "文件不是个目录"
fi
if [ -s $file ]
then
  echo "文件不为空"
else
  echo "文件为空"
fi
if [ -e $file ]
then
  echo "文件存在"
else
  echo "文件不存在"
fi
```

执行脚本，输出结果如下所示：

```
文件可读
文件可写
文件可执行
文件为普通文件
文件不是个目录
文件不为空
文件存在
```

Python是如何执行的

![image-20220301235449267](https://s2.loli.net/2022/03/01/AVUSJ4Y8dITpbLC.png)

python运行慢的原因

![image-20220301235631688](https://s2.loli.net/2022/03/01/hsV81C5ivgAO4LR.png)

使用pyinstaller将py文件打包为exe

### 函数

#### 形式

def 函数名(参数列表)

#### lambda函数

lambda 参数：表达式（多个参数用逗号隔开）

```
#元组使用lambda函数，map函数转变为dict
data=('a','b','c','d')
v=list[map(lambda x,y:{x,y},data[0:2],data[2:4])]
print(v)
输出：
```

![image-20220302000653081](https://s2.loli.net/2022/03/02/BhFQ82sWmNbzpCd.png)

![image-20220302084946449](https://s2.loli.net/2022/03/02/6oQ25gmsxPDuM8T.png)

注：普通函数和lambda函数的异同点

相同点：

- 都可以定义固定的方法和程序处理流程
- 都可以包含参数

不同点：

- lambda的函数代码更为简洁，但是def定义的函数更为直观，易于理解
- def定义的是普通函数，lambda是表达式
- lambda函数不可以包含分支和循环，不能包含return语句

#### python单下划线和双下划线的区别

- 单下划线（_）

  只有单下划线的情况：

  1. 在python Terminal中，单下划线表示上一条语句执行的结果，如果没有上一条语句就会报错，可以对_赋值改变上条语句的值（但是一般不这么做）

  2. 可以作为临时变量，例如使用循环时，如果对循环中的遍历得到的元素不使用，可以使用_替代，成为一个临时遍历

     ```python
     for _ in range(5):
     	print("Python")
     ```

  3. 在类的属性和方法前加入_name，表示该方法或者该属性是私有的。

     注：python不像C++一样是具有私有属性或方法，加上下划线只是代表该属性/方法不能再外部调用，是API中的非公开部分。使用import将不会被导入。

     使用 “ ______all__"可以显式让私有属性和方法包含在被导入的包中。

     ```python
     __all__=[_name,_othername,name]
     ```

- 双下划线

  名称前的双下划线： 在类中该双下划线的作用是不让父类的方法被子类轻易的覆盖

  名称前后的双下划线：表示在python内部定义的方法，可以重写这些方法，调用的时候就可以实现自己的功能，类似于重载

总结：

![image-20220302091610493](https://s2.loli.net/2022/03/02/6mdwAf7XiZKWtkD.png)

#### Python函数的传参方式

对于不可变类型（数值，字符串，元组）因为变量不可修改，因此传参属于值传递，而对于可变类型来说，传参属于引用传递。

对于函数的默认参数来说，如果是可变类型，由于默认参数只会在定义时创建一次，之后调用的函数都会使用同一个变量，有时会得到意想不到的结果，因此在使用可变默认参数时，需要注意是否会重复使用该默认参数，以防止发生问题。

例子：

![image-20220302092729691](https://s2.loli.net/2022/03/02/kMmxfABPZpIvWrb.png)



#### 闭包

定义：内部函数可以引用外部函数的参数和局部变量，当外部函数返回内部函数时，相关的参数和变量都保存在内部函数中，这种特性叫做闭包（Closure）。闭包是两个函数的嵌套，外部函数返回内部函数的引用，**外部函数一定要有参数。**

闭包的类似格式：

![image-20220302093105748](https://s2.loli.net/2022/03/02/LVEDtmFrsM9xhfi.png)

示例：

![image-20220302093538952](https://s2.loli.net/2022/03/02/RI1N4SzPiWQs5HD.png)

*args和**kwargs用于传递不确定的函数参数

*args是用来发送一个非键值对的可变熟练的参数列表给一个函数，*args会接收任意多个参数并把这些参数作为元组传递给函数，*args没有键值，以元组形式传递

**kwargs用于存储可变的关键字参数，允许使用没有事先定义的参数名，将接收到任意多个参数并作为字典传递给函数，有key值，以字典形式传递

函数参数顺序必须为*args在**kwargs前面



在函数中想要修改全局变量，需要用global 加变量名

在py文件处开启终端执行某个py文件并且附上参数，此时输入print(sys.argv)会输出执行的文件名和参数，用列表返回

递归的基本骨架

```python
def recursions(n):
	if n==1:
		#退出条件
		return 1
	else:
		#继续递归
	return n*recursions(n-1)
```

python的递归深度默认值可以用内置函数sys.getrecursionlimit()查看，无限递归会导致栈溢出和python崩溃

阶乘函数factorial ()

随机数 

```python
from random import randint
def generate_code(length=4):							     	    	code_string="abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789"
	code=""
	for _ in range(length):
		code+=code_string[randint(0,len(code_string)-1)]
	return conde
def main():
    for _ in range(10):
        print(generate_code())
if __name__=='__main__':
    main()
```

回调函数：回调函数是把函数的指针作为参数传递给另外一个函数，将整个函数作为一个对象

一行代码实现1-N分组

```
print([[x for x in range(1,10)][i:i+3] for i in range(0,10,3)])
```

#### 内置函数

1.map()函数

根据提供的函数对指定序列做映射

```
map(function,iterable)
// function : 函数
// iterable ：一个或多个序列
```

第一个参数function以参数序列中的每一个元素调用function函数，返回包含每次function函数返回值的新的迭代器

如：

```python
print(list(map(lambda x:x*x),[0,1,2]))
```

2.reduce()函数

会对参数序列中元素进行累积，reduce()函数将一个数据集合中的所有数据进行下列操作。

![image-20220303091659566](https://s2.loli.net/2022/03/03/z74aZFdSTsj2tLV.png)

3.filter()函数

用于筛选序列，把传入的函数依次作用于序列的每个元素，然后根据返回值决定是否保留该元素

![image-20220303092204960](https://s2.loli.net/2022/03/03/tyVfakWI9LRoN7l.png)

4.enumerate()函数

![image-20220303092540196](https://s2.loli.net/2022/03/03/B8oOVW7qnGur9Mc.png)



### 模块

#### os模块

os模块是负责程序和操作系统的交互，提供了访问操作系统底层的接口。

常用的os模块方法：

![image-20220302205237084](https://s2.loli.net/2022/03/02/5FGqWgPALMT9YJH.png)

使用os.getcwd()获取文件当前目录

使用os.chdir()修改当前目录

__name属性的作用：

一个模块被另外一个程序第一次引入的时候，其主程序将全部运行，如果想模块被引入时，模块中的某一程序块不执行，此时可以用______name__属性来使该程序块仅在该模块自身运行时执行

dir()的作用：找到模块内定义的所有名称并以一个字符串的列表形式返回。

使用with方法打开文件，默认在finally中执行f.close

随机数：

![image-20220302214101664](https://s2.loli.net/2022/03/02/DyQ3I9aTRE4dhbv.png)

### 装饰器

![image-20220302214747996](https://s2.loli.net/2022/03/02/TgSCMkicbq6tKFY.png)

装饰器其实就是一个以函数作为参数并返回一个替换原本函数执行的可执行函数，在不改动其他代码的情况下为其增加新的功能

### 生成器

![image-20220302215435613](https://s2.loli.net/2022/03/02/qoWmzRb1Ddik5cK.png)

1.简单生成器

将列表生成式的[]改为(),就创建了一个Generator

如：

```python
g=(x*x for x in range(0,10))
```

 访问元素可以使用next()或者for循环

```python
print(next(g))
#输出1
```

2.带yield的生成器

如果一个函数的定义中包含yield关键字，那么整个函数就不再是一个普通函数，而是一个Gennerator。

生成器是一个返回迭代器的函数，只能用于迭代操作，可以简单理解为：生成器就是一个迭代器。在调用生成器运行的过程中，每次遇到yield时，函数会暂停并保存当前所有的运行信息，返回一个yield的值，并在下一次执行next()方法时从当前位置继续运行。

例子：使用生成器实现斐波那契数列

![image-20220303081135903](https://s2.loli.net/2022/03/03/LIE3Axr8pQfi2O4.png)

![image-20220303081211711](https://s2.loli.net/2022/03/03/1plR2L7Jnku8VGm.png)

yield的作用

yield可以保存当前运行状态，然后暂停执行，即将函数挂起，将yield关键字后面的表达式的值作为返回值返回

使用next()或者send()函数可以从断点处继续执行

### 迭代器

迭代器是Python最强大的功能之一，是常用的访问集合元素的一种方式。

![image-20220303083030041](https://s2.loli.net/2022/03/03/dUa4yZfpnwu3vrQ.png)

### 浅拷贝，深拷贝，赋值

![image-20220303084557310](https://s2.loli.net/2022/03/03/GaQBAu5exTEkjwc.png)

### 内存管理

![image-20220303085427392](https://s2.loli.net/2022/03/03/VP69oDqFyBj78Nz.png)

### 面向对象

特性：

继承：将多个类的共同属性和方法封装到一个父类中，然后通过继承这个类来重用父类的属性

或者方法

封装：

将共同的属性和方法封装到同一个类当中

第一层：只能用类名或者obj.的方式取调用属性和方法

第二层：私有的属性和方法

多态：

基类的同一个方法在不同的派生类中可以有不同的实现

多态和继承无关

#### 继承

继承的特点：

![image-20220303144846735](https://s2.loli.net/2022/03/03/DkzyQCSJr3dTw59.png)

#### 多态

![image-20220303150242101](https://s2.loli.net/2022/03/03/bFH1t2eriOjR5PG.png)

#### 使用类变量的注意点

![image-20220303150653493](https://s2.loli.net/2022/03/03/GQ6yCFYbR2Aj3aM.png)

#### 类方法，静态方法，实例方法

![image-20220303151155149](https://s2.loli.net/2022/03/03/IDEbaHXfgBuwQtn.png)

![image-20220303152757683](https://s2.loli.net/2022/03/03/8xEW4YIvQSeqBfj.png)

#### 单例模式

定义：在实例化类时，无论使用什么样的参数初始化，实例化的类都是同一个（位于内存中的同一个位置）

```python
#重写__new___实现(但是按照以下的写法会在多线程状态下出现问题)
class Singeleton:
	instance=None
	def __init__(self,name):
		self.name=name
	def __new__(cls,*args,**kwargs):
		if cls.instance:
			return cls.instance
		cls.instance=object.__new__(self)
		return cls.instace
obj=Singleton('x')
print(obj)
#解决多线程问题的单例模式
import threading
class Singeleton:
	instance=None
	lock=threading.Rlock()#由于是类要使用，将锁作为类属性
	def __init__(self,name):
		self.name=name
	def __new__(cls,*args,**kwargs):
		if cls.instance:
			return cls.instance
		with cls.lock:
			if cls.instance:
				return cls.instance
			cls.instance=object.__new__(self)
			return cls.instace
def task():
    obj=Singleton('1')
    print(obj)
for i in range(10):
    t=threading.Thread(target=task)
    t.start()
    
```



#### 正则表达式

![image-20220303154302044](https://s2.loli.net/2022/03/03/738LXraMNcyvDfq.png)

![image-20220303155011976](https://s2.loli.net/2022/03/03/3YSnQ4vuAP1c8Uf.png)

查询替换文本字符串的简便方式

```python
import re
p=re.compile('(blue|white|red)')
print(p.sub('colour','blue socks and red shoes'))
print(p.sub('colour','blue socks and red shoes',count=1))

```

使用正则表达式进行解析的例子：

![image-20220303164559972](https://s2.loli.net/2022/03/03/WZzk6Uln71pYXLN.png)

### 系统编程

程序的执行：计算机在执行py程序式，内部就创建一个进程，在进程中创建了一个线程（主线程），由主线程执行代码

#### 创建线程

使用threading模块创建线程

一般来说是创建一个类继承threading.Thread这个基类，然后重写run和_____init_函数，最后进行实例化调用

例子：

```python
import threading
class MyThread(threading.Thread):
  def __init__(self,ThreadID,name,counter):
      threading.Thread.__init__(self)
      self.ThreadID=ThreadID
      self.name=name
      self.counter=counter
  def run(self):
    print('Starting'+self.name)
    print_time(self.name,self.counter,5)
    print('Exiting: '+self.name)

def print_time(name,delay,counter):
    while counter:
        time.sleep(delay)
        print('%s %s'%(name,time.ctime(time.time())))
        counter-=1

def test():
  for i in range(5):
    t = MyThread(i,'thread-%s'%i,i)
    t.start()
if __name__ == '__main__':
    test()
    print('Exiting Main Thread')

```

#### 线程同步

![image-20220304123711655](https://s2.loli.net/2022/03/04/Rwa9ptbQjyGfP1M.png)

上面的一些操作本身就是线程安全的，因此无需加锁，而下方的操作不是线程安全，需要加锁

```python
#线程同步 Rlock可以嵌套锁，嵌套Lock会造成死锁
import threading
class MyThread(threading.Thread):
  def __init__(self,ThreadID,name,counter):
      threading.Thread.__init__(self)
      self.ThreadID=ThreadID
      self.name=name
      self.counter=counter
  def run(self):
    print('Starting'+self.name)
    Threadlock.acquire()
    print('get the lock')
    print_time(self.name,self.counter,5)
    Threadlock.release()
    print('release thr lock')
    print('Exiting: '+self.name)

def print_time(name,delay,counter):
    while counter:
        time.sleep(delay)
        print('%s %s'%(name,time.ctime(time.time())))
        counter-=1
Threadlock=threading.RLock()
def test():
  for i in range(5):
    t = MyThread(i,'thread-%s'%i,i)
    t.start()
if __name__ == '__main__':
    Threadlock.acquire()
    test()
    print('Exiting Main Thread')
    Threadlock.release()
```

死锁：嵌套lock会造成死锁，当一个线程持有一把锁，另外一个线程持有另外一把锁，而第一个线程在执行过程中却想要获取第二把锁，第二个线程执行过程中获取第一把锁，那么就造成了死锁。

#### 线程池

```python
#导入模块 
from concurrent.furture import ThreadPoolExcutor
#使用方法
#创建对象
pool = ThreadPoolExcutor(10)
#执行进程
#pool.submit('函数名'，参数)
def add(10):
	return a+10
pool.submit(add,10)
print('end')
#主线程等待子线程执行完毕在继续执行
pool2=ThreadPoolExcutor(10)
def task(name):
	print('开始执行任务%s'，%(name))
	time.sleep(2)
	print('执行完毕')
	return 10
def done(response):
	print('任务执行的返回值',response.result())
name_List=['download','upload','open windows']
for name in name_list:
	future=pool2.submit(task,name)#返回一个对象，含有线程的返回值
	future.add_done_callback(done)#再某一个线程执行结束后，附加一个函数执行。
pool2.shutdown(True)#使用该函数让主线程等待子线程执行完再继续执行
print('END')


```



#### 线程优先队列模块queue

队列操作函数

![image-20220304085711337](https://s2.loli.net/2022/03/04/fs24LmdngUuNJaS.png)

1.基本FIFO队列

先进先出队列，使用例子

```python
#FIFO队列
import queue
class MyThread(threading.Thread):
  def __init__(self,ThreadID,name,counter):
      threading.Thread.__init__(self)
      self.ThreadID=ThreadID
      self.name=name
      self.counter=counter
  def run(self):
    print('Starting'+self.name)
    Threadlock.acquire()
    print('get the lock')
    print_time(self.name,self.counter,5)
    print('Exiting: '+self.name)
    Threadlock.release()
    print('release thr lock')

def print_time(name,delay,counter):
    while counter:
        time.sleep(delay)
        print('%s %s'%(name,time.ctime(time.time())))
        counter-=1
Threadlock=threading.RLock()
q=queue.Queue(3)
def test():
    i=0
    while not q.full():
        t = MyThread(i,'thread-%s'%i,i)
        q.put(t)
        i+=1
    while not q.empty():
        t=q.get()
        t.start()
if __name__ == '__main__':
    Threadlock.acquire()
    test()
    print('Exiting Main Thread')
    Threadlock.release()
```

LIFO队列

栈队列，后进先出

```python
#LIFO队列
import queue
class MyThread(threading.Thread):
  def __init__(self,ThreadID,name,counter):
      threading.Thread.__init__(self)
      self.ThreadID=ThreadID
      self.name=name
      self.counter=counter
  def run(self):
    print('Starting'+self.name)
    Threadlock.acquire()
    print('get the lock')
    print_time(self.name,self.counter,5)
    print('Exiting: '+self.name)
    Threadlock.release()
    print('release thr lock')

def print_time(name,delay,counter):
    while counter:
        time.sleep(delay)
        print('%s %s'%(name,time.ctime(time.time())))
        counter-=1
q=queue.LifoQueue(3)
def test():
    i=0
    while not q.full():
        t = MyThread(i,'thread-%s'%i,i)
        q.put(t)
        i+=1
    while not q.empty():
        t=q.get()
        t.start()
if __name__ == '__main__':
    Threadlock.acquire()
    test()
    print('Exiting Main Thread')
    Threadlock.release()
```

Priority队列

按照优先级书写队列

```python
#Priority 队列  ---有问题
import random
import queue
class MyThread(threading.Thread):
  def __init__(self,ThreadID,name,counter):
      threading.Thread.__init__(self)
      self.ThreadID=ThreadID
      self.name=name
      self.counter=counter
  def run(self):
    print('Starting'+self.name)
    Threadlock.acquire()
    print('get the lock')
    print_time(self.name,self.counter,5)
    print('Exiting: '+self.name)
    Threadlock.release()
    print('release thr lock')
  def __lt__(self,other):
      return other.ThreadID > self.ThreadID  #设置优先级

def print_time(name,delay,counter):
    while counter:
        time.sleep(delay)
        print('%s %s'%(name,time.ctime(time.time())))
        counter-=1
Threadlock=threading.RLock()
q=queue.PriorityQueue(10)
def test():
    list1=[int(random.randrange(0,10)) for i in range(10)]
    i=0
    while not q.full():
        print(list1[i])
        t = MyThread(list1[i],'thread-%s'%list1[i],list1[i])
        q.put(t)
        i+=1
    while not q.empty():
        t=q.get()
        t.start()
if __name__ == '__main__':
    Threadlock.acquire()
    test()
    print('Exiting Main Thread')
    Threadlock.release()
```

多线程开发

```python
import threading
loop=1000000
number=0
def _add(count):
	global number
	for i in range(count):
		number+=1
t=threading.Thread(targe=_add,args=(loop,))
t.start()
t.join() #让主线程等待子线程结束
print(number)
```

守护线程

```
t.setDaemon(True/False)
```

让线程变为守护模式，及主线程执行结束时不在等待子线程而是直接关闭子线程

如果是False，就会等待子进程结束在结束

```python
#守护线程
#setdemon
import threading
loop=1000000
number=0
def _add(count):
    global number
    for i in range(count):
        number+=1
    print(number)
def _sub(count):
    global number
    for i in range(count):
        number-=1
    print(number)
t=threading.Thread(target=_add,args=(loop,))
#t2=threading.Thread(target=_sub,args=(loop,))
#t.setDaemon(True)#如果是True当主线程结束，子线程自动关闭
t.setDaemon(False)#如果是False，主线程会等待子线程执行完毕在结束
t.start()
#t2.start()
#t.join() #让其他线程等待线程t结束
#t2.join()#其他线程等待线程t2结束
print(number)
```



#### 进程

进程的创建需要使用multiprocessing创建进程

注：创建进程时，主进程代码需要放在if____name____ == "____main____"中

```python
import multiprocessing
class Myprocess(multiprocessing.Process):
    def __init__(self,name,ID):
        super(multiprocessing.Process,self).__init__()
        self.name=name
        self.ID=ID
    def run(self):
        print('name: %s, ID: %s'%(self.name,self.ID))
        print(time.time())
def main():
    print(time.time())
    student=[['chw',201908010510],['fzm',201908010511],['ysx',201908010508]]
    for name,ID in student:
        p1=Myprocess(name,ID)
        p1.start()
if __name__=='__main__':
    main()
```

GIL锁 （全局解释器锁）

属于Cpython解释器的一个机制，限制只能执行一个线程，无法使用计算机的多核优势

因此利用cpu的多核优势时用进程，不使用就用线程

计算密集型操作需要使用多核cpu，使用进程

I/O操作不需要使用多核CPU，可以使用线程

使用进程时，最好使用fork的系统调用，否则在转移到unix时速度较慢，

如何使用fork模式（win下面默认spawn模式）

```python
import multiprocess
import threading
def task():
	#如果父进程的锁以及被申请，那么子进程的锁状态也是被申请的 
	print(lock)
	with lock:
		print(”执行中“)
if __name__=="__main__":
	multiprocess.set_start_method("fork")#使用fork模式
	name=[]
	lock=threading.RLock()
	lock.acquire()
	P1=mulitiprocess.Process(target=task)
	P1.start()
```

进程方法：

```

```

进程数据共享

进程是资源分配的最小单元，每个进程中都维护自己建立的数据不共享

共享的四种方法

1. 使用value和array

   ```python
   from multiprocessing import Process, Value, Array
   
   
   def func(n, m1, m2,array):
       n.value = 888
       m1.value = 'a'.encode('utf-8')
       m2.value = '物'
       array[0]=2
   
   
   if __name__ == '__main__':
       num = Value('i', 666)
       v1 = Value('c')
       v2 = Value('u')
       array=Array('i',[1,2,3,4])
       p = Process(target=func, args=(num, v1, v2,array))
       p.start()
       p.join()
       print(num.value)  # 888
       print(v1.value)  # a
       print(v2.value)  # wu
       print(array[0])
   ```

2. 使用manager

   ```python
   from multiprocessing import Process,Manager
   def f(d,l):
   	d['1']=1
   	l.append(2)
   if __name__ == '__main__':
   	with Manager as manager:
   		d = manager.dict()
   		l = manager.list()
   		
   		p = Process(target=f,args=(d,l))
   		p.start()
   		p.join()
   		
   		print(d)
   		print(l)
   ```

3. 基于队列

   ```python
   import multprocessing
   def task(q):
   	for i in range(10):
   		q.put(i)
   if __name__=='__main__':
   	queue = multiprocessing.Queue()
   	p = multiprocessing.Process(target=task,args=(queue,))
   	p.start()
   	print(’主进程‘)
   	while not q.empty():
   		print(queue.get())
   	
   ```

4. Pipe

   ```python
   import time
   import multiprocessing
   
   def task(conn):
   	time.sleep(1)
   	cond.send(111,22,33,44)
   	data = conn.recv() #阻塞
   	print('子进程接收'，data)
   	time.sleep(2)
   if __name__ == '__main__':
   	parent_conn,child_conn=multiprocessing.Pipe()
   	
   	p = multiprocessing.Process(target=task,args=(child_conn,))
   	p.start()
   	
   	info = parent_conn.recv() #阻塞
   	print('主进程接收', info)
   	parent_conn.send(666)
   ```

进程池:使用方法和线程池类似 （ 进程数据共享需要使用manager的Rlock）

```python
import time
from concurrent.futures import ProcessPoolExecutor
def task(num):
	print ('执行')
	time.sleep(2)
if __name__=='__main__':
	pool = ProcessPoolExectuor(4)
	for i in range (10):
		pool.submit(task,i)
	print(1)
	print(2)
```

### 网络编程

#### OSI七层网络模型：

1. 应用层：应用程序接口
2. 表示层：将传输数据用某种格式表示
3. 会话层：建立物理网络的连接
4. 数据传输层：进行信息的网络传输
5. 网络层：对数据进行网络传输
6. 链路层：对数据进行压缩和解压缩
7. 物理硬件层：使用位发送数据，如电磁波，光纤，电缆

#### 套接字(socket编程)

1. 函数socket创建socket对象：

   ```python
   socket(socket_family,socket_type,protocol)
   #socket_family：socket.AF_UNIX，socket.AF_INET ：UNIX用于本机通信，INETy
   #socket_type:socket.SOCK_STREAM,socket.SOCK_DGRAM
   tcp=socket.socket(socket.AF_INET,socket.SOCK_STREAM)#TCP/IP
   UDP=socket.socket(socket.AF_INET,socket.SOCK_DGRAM)#UDP
   ```

​	
