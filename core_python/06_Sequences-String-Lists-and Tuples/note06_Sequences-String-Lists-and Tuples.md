# 第6章 序列：字符串、列表和元组
序列：它们的成员有序排列，并且可以通过下标偏移量访问到它的一个或几个成员，包括字符串（普通字符串和Unicode字符串）、列表和元组类型。
## 6.1 序列 
访问模式：  

* 指定偏移量
* 切片操作
### 6.1.1 标准类型操作符
标准类型操作符一般都能适用于所有的序列类型。当然，如果作复合类型的对象比较的话，这样说可能需要有所保留，不过其他的操作绝对是完全适用的。**（啥意思呀。。。）**
### 6.1.2 序列类型操作符
#### 1.成员关系操作符（in、not in）
#### 2.连接操作符（+）
#### 3.重复操作符（*）
#### 4.切片操作符（[ ]、[:]、[::]）
访问某一个数据元素的语法如下：

	sequence[index]
sequence是序列的名字，index是想要访问的元素对应的偏移量。偏移量值：  

* 为正，从0到N-1
* 为负，从-len(sequence)<=index<=-1
访问多个元素：

	sequence[starting_index:ending_index]
整个序列：

	sequence或sequence[:]
#### 5.用步长索引来进行扩展的切片操作
序列的最后一个切片操作是扩展切片操作，它多出来的第三个索引值被用做步长参数。
	
	>>> s = 'abcde'
	>>> s[::-1] # 可以视为“翻转”操作
	>>> s[::2] # 隔一个取一个
#### 6.切片索引的更多内容

	>>> s = 'abcde'
	>>> i = -1
	>>> for i in range(-1, -len(s), -1):
	... 	print(s[:i])
	...
	abcd
	abc
	ab
	a
如果想第一次迭代的时候显示整个字符串。有一个小技巧：用None作为索引值，比如说，想用一个变量作为索引来从第一个到遍历最后一个元素的时候：

	>>> s = 'abcde'
	>>> i = -1
	>>> for i in [None] + range(-1, -len(s), -1):
	... 	print(s[:i])
	...
	abcde
	abcd
	abc
	ab
	a
### 6.1.3 内建函数（BIF）
序列本身就内含了迭代的概念，之所以会这样就是因为迭代这个概念就是从序列，迭代器，或者其他支持迭代操作的对象中泛化得来的。  
由于Python的for循环可以遍历所有的可迭代类型，在（非纯序列对象上）执行for循环时就像在一个纯序列对象上执行一样。而且Python的很多原来只支持序列作为参数的内建函数现在也开始支持迭代器或者类迭代器了。我们把这些类型统称为“可迭代对象”。
#### 1.类型转换
* list(iter)：列表    
* str(obj)：字符串（对象的字符串表示法） 
* Unicode(obj)：Unicode字符串（使用默认编码），是str()函数的Unicode版本  
* basestring()：抽象函数工厂，仅仅是为str和unicode提供父类，所以不能被实例化，也不能被调用  
* tuple(iter)：元组
为什么Python里不简单地把一个对象转换成另一个对象？  
由于，一旦一个Python的对象被建立，我们就不能更改其身份或类型。如果你把一个列表对象传递给list()函数，便会创建这个对象的浅拷贝，然后将其插入新的列表中。同样地，在做连接操作和重复操作时，我们也会这样处理。  
浅拷贝：只拷贝了对象的索引，而不是重新建立了一个对象。  
完全拷贝（深拷贝）：包括递归，如果你的对象是一个包含在容器中的容器。
#### 2.可操作
注意，len()、reversed()和sum()函数只接受序列类型对象作为参数，而剩下的还可以接受可迭代对象作为参数，另外，max()和min()函数也可以接受一个参数列表。

* enumerate(iter)：返回一个enumerate对象（同时也是一个迭代器），该对像生成由iter每个元素的index值和item值组成的元组
* len(seq)
* max(iter,key=None) or max(arg0,arg1...,key=None)：如果指定了key，这个key必须是一个可以传给sort()方法的，用于比较回调函数
* mix(iter,key=None) or mix(arg0,arg1...,key=None)：如果指定了key，这个key必须是一个可以传给sort()方法的，用于比较回调函数
* reversed(seq)：接受一个序列作为参数，返回一个以逆序访问的迭代器
* sorted(iter,func=None,key=None,reverse=False)：接受一个可迭代对象作为参数，返回一个有序的列表；可选参数func、key和reverse的含义跟list.sort()内建函数的参数含义一样
* sum(seq,init=0)：返回seq和可选参数init的总和，其效果等同于reduce(operator.add,seq,init)
* zip([it0,it1,...itN]):返回一个列表，其第一个元素是it0\it1...这些元素的第一个元素组成的一个元组，第二个...以此类推
## 6.2 字符串
Python里面单引号和双引号的作用是相同的  
字符串是一种直接量或者说是一种标量，这意味着Python解释器在处理字符串时把它作为单一值并且不会包含其他Python类型  
字符串是不可变类型  
字符串是由独立的字符组成，并且这些字符可以通过切片操作顺序访问
Python实际上有三类字符串：

* 通常意义的字符串，str
* unicode字符串，Unicode
* 抽象类basestring
### 1. 字符串的创建和赋值
使用单引号、双引号和str()  
### 2. 如果访问字符串的值（字符和子串）
Python里面没有字符这个类型，而是用长度为1的字符串来表示这个概念，当然，这其实也是一个子串。
### 3. 如何改变字符串
通过变量赋值（或者重新赋值）的方式“更新”一个已有的字符串。  
跟数字类型一样，字符串类型也是不可变得，所以要改变一个字符串就必须通过创建一个新字符串或者拼凑一个旧字符串来实现。
### 4.如何删除字符和字符串
删除字符串中的某一个字符，也是通过重组后的重新赋值来实现。  
通过赋一个空字符串或者使用del语句来清空或者删除一个字符串。  
当然，定义这个字符串的代码最终会结束，那时Python会自动释放这些字符串。
## 6.3 字符串和操作
#### 6.3.1 标准类型操作符

	>>> str1 = 'abc'
	>>> str2 = 'lmn'
	>>> str1 < str2
	True
在做比较操作的时候，字符串是按照ASCII值的大小来比较的。
#### 6.3.2 序列操作符切片([ ]和[:])
* 正向索引：从0开始，到N-1结束
* 反向索引：从-len(aString)开始，到-1结束
* 默认索引
##### 1. 成员操作符（in，not in）
有一个性能问题：如果把重复操作作为参数放到循环里面进行是非常低效的！  
string模块预定义的字符串：

	>>> import string
	>>> string.uppercase
	'ABCDEFGHIJKLMNOPQRSTUVWXYZ'
	>>> string.lowercase
	'abcdefghijklmnopqrstuvmxyz'
	>>> string.letters
	'abcdefghijklmnopqrstuvmxyzABCDEFGHIJKLMNOPQRSTUVWXYZ'
	>>> string.digits
	'0123456789'
##### 2. 连接符（+）
string.upper()方法，可以把字符串的所有字符都变为大写  
从性能考虑，不建议使用string模块。  
原因是：Python必须为每一个参加连接操作的字符串分配新的内存，包括产生新的字符串。  
推荐用法：使用字符串格式化操作符(%)，或者把所有的字符串放到一个列表中去，然后用一个josn()方法来把它们连接在一起。

	>>> '%s %s' % ('Spanish', 'Inquisition')
	'Spanish Inquisition'
	>>> 
	>>> s = ''.join(('Spanish', 'Inquisition', 'Made Easy'))
	>>> s
	'Spanish Inquisition Made Easy'
	>>> 
	>>> # no need to import string to user string.upper():
	>>> ('%s%s' % (s[:3], s[20])).upper()
	'SPAM'
##### 3. 编译时字符串连接
可以把长的字符串分词几部分来写，而不用加反斜杠。这种写法的好处是可以把注释加进来。
##### 4. 普通字符串转化为Unicode字符串
如果把普通字符串和一个Unicode字符串做连接处理，Python会在连接操作前先把普通字符串转化为Unicode字符串：

	>>> 'Hello' + u' ' + 'World' + u'!'
	u'Hello World!'
## 6.4 只适用于字符串的操作符
### 6.4.1 格式化操作符(%)
字符串格式化符号：
	
	格式化字符         转化方式
	%c         转换成字符（ASCII码值，或者长度为一的字符串）
	%r         优先用repr()函数进行字符串转换
	%s         优先用str()函数进行字符串转换
	%d/%i      转成有符号十进制数
	%u         转成无符号十进制数
	%o         转成无符号八进制数
	%x/%X      转成无符号十六进制数（x/X代表转换后的十六进制字符的大小写）
	%e/%E      转成科学计数法（e/E控制输出e/E）
	%f/%F      转成浮点型（小数部分自然截断）
	%g/%G      %e和%f/%E和%F的简写
	%%         输出%
Python支持两种格式的输入参数：    
	1. 元组，这基本上是一种的C printf()风格的转换参数集  
	2. 字典形式，字典其实是一个哈希键-值对的集合。  
字典：键是作为格式字符串出现，相对应的值作为参数在进行转化时提供给格式字符串。格式字符串既可以跟print语句一起用来向终端用户输出数据，又可以用来合并字符串形成新字符串，而且还可以直接显示到GUI界面上去。  
格式化操作符辅助指令：
 
	符号      作用
	*	 定义宽度或者小数点精度
	-	 用做左对齐
	+	 在正数前面显示加号
	<sp>	 在正数前面显示空格
	#	 在八进制数前面显示('0')，在十六进制前面显示'0x'或者'0X'
	0	 显示的数字前面填充'0'而不是默认的空格
	%	 '%%'输出一个单一的'%'
	(var)	 映射变量（字典参数）	
	m.n	 m是显示的最小总宽度，n是小数点后的位数（如果可用的话）
字符串格式化操作符不仅很酷、易用、上手快，而且是一个非常有用的调试工具。
### 6.4.2 字符串模板：更简单的替代品
