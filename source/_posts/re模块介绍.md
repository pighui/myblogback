---
title: re模块介绍
comments: true
tags:
  - Python
  - 爬虫
categories:
  - 爬虫
date: 2019-05-08 09:10:26
---


正则表达式，又称规则表达式。（英语：Regular Expression，在代码中常简写为regex、regexp或RE），计算机科学的一个概念。正则表通常被用来检索、替换那些符合某个模式(规则)的文本。

许多程序设计语言都支持利用正则表达式进行字符串操作。python也不例外。python通过内置模块re对正则表达式提供了支持。

<!--more-->

## 正则语法

模式字符串使用特殊的语法来表示一个正则表达式：

字母和数字表示他们自身。一个正则表达式模式中的字母和数字匹配同样的字符串。

多数字母和数字前加一个反斜杠时会拥有不同的含义。

标点符号只有被转义时才匹配自身，否则它们表示特殊的含义。

反斜杠本身需要使用反斜杠转义。

由于正则表达式通常都包含反斜杠，所以你最好使用原始字符串来表示它们。模式元素(如 r'/t'，等价于'//t')匹配相应的特殊字符。

下表列出了正则表达式模式语法中的特殊元素。如果你使用模式的同时提供了可选的标志参数，某些模式元素的含义会改变。

| 元字符       | 描述                                                         |
| ------------ | :----------------------------------------------------------- |
| \            | 将下一个字符标记符、或一个向后引用、或一个八进制转义符。例如，“\\n”匹配\n。“\n”匹配换行符。序列“\\”匹配“\”而“\(”则匹配“(”。即相当于多种编程语言中都有的“转义字符”的概念。 |
| ^            | 匹配输入字符串的开始位置。如果设置了RegExp对象的Multiline属性，^也匹配“\n”或“\r”之后的位置。 |
| $            | 匹配输入字符串的结束位置。如果设置了RegExp对象的Multiline属性，$也匹配“\n”或“\r”之前的位置。 |
| *            | 匹配前面的子表达式任意次。例如，zo*能匹配“z”，也能匹配“zo”以及“zoo”。*等价于o{0,} |
| +            | 匹配前面的子表达式一次或多次(大于等于1次）。例如，“zo+”能匹配“zo”以及“zoo”，但不能匹配“z”。+等价于{1,}。 |
| ?            | 匹配前面的子表达式零次或一次。例如，“do(es)?”可以匹配“do”或“does”中的“do”。?等价于{0,1}。 |
| {n}          | n是一个非负整数。匹配确定的n次。例如，“o{2}”不能匹配“Bob”中的“o”，但是能匹配“food”中的两个o。 |
| {n,}         | n是一个非负整数。至少匹配n次。例如，“o{2,}”不能匹配“Bob”中的“o”，但能匹配“foooood”中的所有o。“o{1,}”等价于“o+”。“o{0,}”则等价于“o*”。 |
| {n,m}        | m和n均为非负整数，其中n<=m。最少匹配n次且最多匹配m次。例如，“o{1,3}”将匹配“fooooood”中的前三个o为一组，后三个o为一组。“o{0,1}”等价于“o?”。请注意在逗号和两个数之间不能有空格。 |
| ?            | 当该字符紧跟在任何一个其他限制符（*,+,?，{n}，{n,}，{n,m}）后面时，匹配模式是非贪婪的。非贪婪模式尽可能少的匹配所搜索的字符串，而默认的贪婪模式则尽可能多的匹配所搜索的字符串。例如，对于字符串“oooo”，“o+”将尽可能多的匹配“o”，得到结果[“oooo”]，而“o+?”将尽可能少的匹配“o”，得到结果 ['o',   'o', 'o', 'o'] |
| .点          | 匹配除“\r\n”之外的任何单个字符。要匹配包括“\r\n”在内的任何字符，请使用像“[\s\S]”的模式。 |
| (pattern)    | 匹配pattern并获取这一匹配。所获取的匹配可以从产生的Matches集合得到，在VBScript中使用SubMatches集合，在JScript中则使用$0…$9属性。要匹配圆括号字符，请使用“\(”或“\)”。 |
| (?:pattern)  | 非获取匹配，匹配pattern但不获取匹配结果，不进行存储供以后使用。这在使用或字符“(\|)”来组合一个模式的各个部分时很有用。例如“industr(?:y\|ies)”就是一个比“industry\|industries”更简略的表达式。 |
| (?=pattern)  | 非获取匹配，正向肯定预查，在任何匹配pattern的字符串开始处匹配查找字符串，该匹配不需要获取供以后使用。例如，“Windows(?=95\|98\|NT\|2000)”能匹配“Windows2000”中的“Windows”，但不能匹配“Windows3.1”中的“Windows”。预查不消耗字符，也就是说，在一个匹配发生后，在最后一次匹配之后立即开始下一次匹配的搜索，而不是从包含预查的字符之后开始。 |
| (?!pattern)  | 非获取匹配，正向否定预查，在任何不匹配pattern的字符串开始处匹配查找字符串，该匹配不需要获取供以后使用。例如“Windows(?!95\|98\|NT\|2000)”能匹配“Windows3.1”中的“Windows”，但不能匹配“Windows2000”中的“Windows”。 |
| (?<=pattern) | 非获取匹配，反向肯定预查，与正向肯定预查类似，只是方向相反。例如，“(?<=95\|98\|NT\|2000)Windows”能匹配“2000Windows”中的“Windows”，但不能匹配“3.1Windows”中的“Windows”。 |
| (?<!pattern) | 非获取匹配，反向否定预查，与正向否定预查类似，只是方向相反。例如“(?<!95\|98\|NT\|2000)Windows”能匹配“3.1Windows”中的“Windows”，但不能匹配“2000Windows”中的“Windows”。这个地方不正确，有问题   此处用或任意一项都不能超过2位，如“(?<!95\|98\|NT\|20)Windows正确，“(?<!95\|980\|NT\|20)Windows   报错，若是单独使用则无限制，如(?<!2000)Windows   正确匹配 |
| x\|y         | 匹配x或y。例如，“z\|food”能匹配“z”或“food”(此处请谨慎)。“[zf]ood”则匹配“zood”或“food”。 |
| [xyz]        | 字符集合。匹配所包含的任意一个字符。例如，“[abc]”可以匹配“plain”中的“a”。 |
| [^xyz]       | 负值字符集合。匹配未包含的任意字符。例如，“abc”可以匹配“plain”中的“plin”。 |
| [a-z]        | 字符范围。匹配指定范围内的任意字符。例如，“[a-z]”可以匹配“a”到“z”范围内的任意小写字母字符。   注意:只有连字符在字符组内部时,并且出现在两个字符之间时,才能表示字符的范围; 如果出字符组的开头,则只能表示连字符本身. |
| [^a-z]       | 负值字符范围。匹配任何不在指定范围内的任意字符。例如，“a-z”可以匹配任何不在“a”到“z”范围内的任意字符。 |
| \b           | 匹配一个单词边界，也就是指单词和空格间的位置（即正则表达式的“匹配”有两种概念，一种是匹配字符，一种是匹配位置，这里的\b就是匹配位置的）。例如，“er\b”可以匹配“never”中的“er”，但不能匹配“verb”中的“er”。 |
| \B           | 匹配非单词边界。“er\B”能匹配“verb”中的“er”，但不能匹配“never”中的“er”。 |
| \cx          | 匹配由x指明的控制字符。例如，\cM匹配一个Control-M或回车符。x的值必须为A-Z或a-z之一。否则，将c视为一个原义的“c”字符。 |
| \d           | 匹配一个数字字符。等价于[0-9]。grep 要加上-P，perl正则支持   |
| \D           | 匹配一个非数字字符。等价于0-9。grep要加上-P，perl正则支持    |
| \f           | 匹配一个换页符。等价于\x0c和\cL。                            |
| \n           | 匹配一个换行符。等价于\x0a和\cJ。                            |
| \r           | 匹配一个回车符。等价于\x0d和\cM。                            |
| \s           | 匹配任何不可见字符，包括空格、制表符、换页符等等。等价于[ \f\n\r\t\v]。 |
| \S           | 匹配任何可见字符。等价于   \f\n\r\t\v。                      |
| \t           | 匹配一个制表符。等价于\x09和\cI。                            |
| \v           | 匹配一个垂直制表符。等价于\x0b和\cK。                        |
| \w           | 匹配包括下划线的任何单词字符。类似但不等价于“[A-Za-z0-9_]”，这里的"单词"字符使用Unicode字符集。 |
| \W           | 匹配任何非单词字符。等价于“A-Za-z0-9_”。                     |
| \xn          | 匹配n，其中n为十六进制转义值。十六进制转义值必须为确定的两个数字长。例如，“\x41”匹配“A”。“\x041”则等价于“\x04&1”。正则表达式中可以使用ASCII编码。 |
| \num         | 匹配num，其中num是一个正整数。对所获取的匹配的引用。例如，“(.)\1”匹配两个连续的相同字符。 |
| \n           | 标识一个八进制转义值或一个向后引用。如果\n之前至少n个获取的子表达式，则n为向后引用。否则，如果n为八进制数字（0-7），则n为一个八进制转义值。 |
| \nm          | 标识一个八进制转义值或一个向后引用。如果\nm之前至少有nm个获得子表达式，则nm为向后引用。如果\nm之前至少有n个获取，则n为一个后跟文字m的向后引用。如果前面的条件都不满足，若n和m均为八进制数字（0-7），则\nm将匹配八进制转义值nm。 |
| \nml         | 如果n为八进制数字（0-7），且m和l均为八进制数字（0-7），则匹配八进制转义值nml。 |
| \un          | 匹配n，其中n是一个用四个十六进制数字表示的Unicode字符。例如，\u00A9匹配版权符号（&copy;）。 |
| \p{P}        | 小写   p 是 property 的意思，表示 Unicode   属性，用于   Unicode   正表达式的前缀。中括号内的“P”表示Unicode 字符集七个字符属性之一：标点字符。   其他六个属性：   L：字母；   M：标记符号（一般不会单独出现）；   Z：分隔符（比如空格、换行等）；   S：符号（比如数学符号、货币符号等）；   N：数字（比如阿拉伯数字、罗马数字等）；   C：其他字符。   *注：此语法部分语言不支持，例：javascript。 |
| <   >        | 匹配词（word）的开始（<）和结束（>）。例如正则表达式\<the\>能够匹配字符串"for   the wise"中的"the"，但是不能匹配字符串"otherwise"中的"the"。注意：这个元字符不是所有的软件都支持的。 |
| ( )          | 将( 和 ) 之间的表达式定义为“组”（group），并且将匹配这个表达式的字符保存到一个临时区域（一个正则表达式中最多可以保存9个），它们可以用 \1 到\9 的符号来引用。 |
| \|           | 将两个匹配条件进行逻辑“或”（Or）运算。例如正则表达式(him\|her) 匹配"it   belongs to him"和"it   belongs to her"，但是不能匹配"it   belongs to them."。注意：这个元字符不是所有的软件都支持的。 |

## re模块使用

使用re的一般步骤是先将正则表达式的字符串形式编译为Pattern实例，然后使用Pattern实例处理文本并获得匹配结果（一个Match实例），最后使用Match实例获得信息，进行其他的操作。下面代码是一个简单的应用示例：

```python
#encoding: UTF-8 
import re 

# 将正则表达式编译成Pattern对象 
pattern = re.compile(r’hello’)
# 使用Pattern匹配文本，获得匹配结果，无法匹配时将返回None 
match = pattern.match(‘hello world!’) 
if match: # 使用Match获得分组信息 
    print (match.group())    
```

**compile**

re.compile(strPattern[, flag]):

这个方法是Pattern类的工厂方法，用于将字符串形式的正则表达式编译为Pattern对象。 第二个参数flag是匹配模式，取值可以使用按位或运算符'|'表示同时生效，比如re.I | re.M。另外，你也可以在regex字符串中指定模式，比如re.compile('pattern', re.I | re.M)与re.compile('(?im)pattern')是等价的。 

可选值有：

re.I(re.IGNORECASE): 忽略大小写（括号内是完整写法，下同）

re.M(MULTILINE): 多行模式，改变'^'和'$'的行为

re.S(DOTALL): 点任意匹配模式，改变'.'的行为

re.L(LOCALE): 使预定字符类 \w \W \b \B \s \S 取决于当前区域设定

re.U(UNICODE): 使预定字符类 \w \W \b \B \s \S \d \D 取决于unicode定义的字符属性

re.X(VERBOSE): 详细模式。这个模式下正则表达式可以是多行，忽略空白字符，并可以加入注释

例如，以下两个正则表达式是等价的：

```python
a = re.compile(r“”“\d+ 

  \. 

  \d* “””, re.X) 

b = re.compile(r“\d+\.\d*”)
```

​    re提供了众多模块方法用于完成正则表达式的功能。这些方法可以使用Pattern实例的相应方法替代，唯一的好处是少写一行re.compile()代码，但同时也无法复用编译后的Pattern对象。这些方法将在Pattern类的实例方法部分一起介绍。如上面这个例子可以简写为：

```python
m = re.match(r’hello’, ‘hello world!’) 
print m.group()
```

**反斜杠的困扰**

正则表达式使用反斜杆（\）来转义特殊字符，使其可以匹配字符本身，而不是指定其他特殊的含义。这可能会和python字面意义上的字符串转义相冲突，这也许有些令人费解。比如，要匹配一个反斜杆本身，你也许要用‘\\\\’来做为正则表达式的字符串，因为正则表达式要是\\，而字符串里，每个反斜杆都要写成\\。
 你也可以在字符串前加上 r 这个前缀来避免部分疑惑，因为 r 开头的python字符串是 原生字符串(raw字符串)，所以里面的所有字符都不会被转义，比如r'\n'这个字符串就是一个反斜杆加上一字母n，而'\n'我们知道这是个换行符。因此，上面的'\\\\'你也可以写成r'\\'，这样，应该就好理解很多了。

### Match

re.match(pattern, string[, flags]):
这个方法将会从string（我们要匹配的字符串）的开头开始，尝试匹配pattern，一直向后匹配，如果遇到无法匹配的字符，立即返回 None，如果匹配未结束已经到达string的末尾，也会返回None。两个结果均表示匹配失败，否则匹配pattern成功，同时匹配终止，不再对 string向后匹配。下面我们通过一个例子理解一下:

```python
#encoding=utf-8
#导入re模块
import re
  
# 将正则表达式编译成Pattern对象，注意hello前面的r的意思是“原生字符串”
pattern = re.compile(r'\w{3,5}-\d{3}')
  
# 使用re.match匹配文本，获得匹配结果，无法匹配时将返回None
result1 = re.match(pattern,'hello-123')
result2 = re.match(pattern,'hello-345o CQC!')
result3 = re.match(pattern,'he-123 CQC!')
result4 = re.match(pattern,'hello-1 CQC!')
'''
result1 = pattern.match('hello')
result2 = pattern.match('helloo CQC!')
result3 = pattern.match('helo CQC!')
result4 = pattern.match('hello CQC!')
'''
  
#如果1匹配成功
if result1:
  # 使用Match获得分组信息
  print(result1.group())
else:
  print('1匹配失败！')
  
#如果2匹配成功
if result2:
  # 使用Match获得分组信息
  print(result2.group())
else:
  print('2匹配失败！')
  
#如果3匹配成功
if result3:
  # 使用Match获得分组信息
  print(result3.group())
else:
  print('3匹配失败！')
  
#如果4匹配成功
if result4:
  # 使用Match获得分组信息
  print (result4.group())
else:
  print('4匹配失败！')

```

匹配分析

1. 第一个匹配，pattern正则表达式为'hello'，我们匹配的目标字符串string也为hello，从头至尾完全匹配，匹配成功。
2. 第二个匹配，string为helloo CQC，从string头开始匹配pattern完全可以匹配，pattern匹配结束，同时匹配终止，后面的o CQC不再匹配，返回匹配成功的信息。
3. 第三个匹配，string为helo CQC，从string头开始匹配pattern，发现到 ‘o' 时无法完成匹配，匹配终止，返回None
4. 第四个匹配，同第二个匹配原理，即使遇到了空格符也不会受影响。

我们还看到最后打印出了result.group()，这个是什么意思呢？下面我们说一下关于match对象的的属性和方法
 Match对象是一次匹配的结果，包含了很多关于此次匹配的信息，可以使用Match提供的可读属性或方法来获取这些信息。

Match对象是一次匹配的结果，包含了很多关于此次匹配的信息，可以使用Match提供的可读属性或方法来获取这些信息。

**属性：**

•string: 匹配时使用的文本。

•re: 匹配时使用的Pattern对象。

•pos: 文本中正则表达式开始搜索的索引。值与Pattern.match()和Pattern.seach()方法的同名参数相同。

•endpos: 文本中正则表达式结束搜索的索引。值与Pattern.match()和Pattern.seach()方法的同名参数相同。

•lastindex: 最后一个被捕获的分组在文本中的索引。如果没有被捕获的分组，将为None。

•lastgroup: 最后一个被捕获的分组的别名。如果这个分组没有别名或者没有被捕获的分组，将为None。

**方法：**

start([group]): 
 返回指定的组截获的子串在string中的起始索引（子串第一个字符的索引）。group默认值为0。

end([group]): 
 返回指定的组截获的子串在string中的结束索引（子串最后一个字符的索引+1）。group默认值为0。

span([group]): 
 返回(start(group), end(group))。

expand(template): 
 将匹配到的分组代入template中然后返回。template中可以使用\id或\g<id>、\g<name>引用分组，但不能使用编号0。\id与\g<id>是等价的；但\10将被认为是第10个分组，如果你想表达\1之后是字符'0'，只能使用\g<1>0。

示例代码：

```python
import re 
m = re.match(r'(\w+) (\w+)(?P<sign>.*)', 'hello world!') 
print ("m.string:", m.string) 
print ("m.re:", m.re) 
print "m.pos:", m.pos 
print "m.endpos:", m.endpos 
print "m.lastindex:", m.lastindex 
print "m.lastgroup:", m.lastgroup 
print "m.group(1,2):", m.group(1, 2) 
print "m.groups():", m.groups() 
print "m.groupdict():", m.groupdict() 
print "m.start(2):", m.start(2) 
print "m.end(2):", m.end(2) 
print "m.span(2):", m.span(2) 
print r"m.expand(r'\2 \1\3'):", m.expand(r'\2 \1\3')

```

### search

re.search(pattern, string[, flags])

search方法与match方法极其类似，区别在于match()函数只检测re是不是在string的开始位置匹配，search()会扫描整个string查找匹配，match（）只有在0位置匹配成功的话才有返回，如果不是开始位置匹配成功的话，match()就返回None。同样，search方法的返回对象同样match()返回对象的方法和属性。

```python
#导入re模块

import re
# 将正则表达式编译成Pattern对象
pattern = re.compile(r’world’)
# 使用search()查找匹配的子串，不存在能匹配的子串时将返回None
# 这个例子中使用match()无法成功匹配
match = re.search(pattern,’hello world!’)

if match:
    # 使用Match获得分组信息
    print match.group()
```

### split

re.split(pattern, string[, maxsplit])

按照能够匹配的子串将string分割后返回列表。maxsplit用于指定最大分割次数，不指定将全部分割。

```python
#导入re模块
import re 

pattern = re.compile(r'\d+')
print re.split(pattern,'one1two2three3four4')
```

### findall

re.findall(pattern, string[, flags]) 
搜索string，以列表形式返回全部能匹配的子串。

```python
import re 
pattern = re.compile(r'\d+')
print re.findall(pattern,'one1two2three3four4')
```

### sub

re.sub(pattern, repl, string[, count])
使用repl替换string中每一个匹配的子串后返回替换后的字符串。当repl是一个字符串时，可以使用\id或\g、\g引用分组，但不能使用编号0。当repl是一个方法时，这个方法应当只接受一个参数（Match对象），并返回一个字符串用于替换（返回的字符串中不能再引用分组）。count用于指定最多替换次数，不指定时全部替换。

```python
import re,sys

pattern = re.compile(r'(\w+) (\w+)')
s = 'i say, hello world!'

#sys.exit()  
print(re.sub(pattern,r'\2 \1', s))
 
def func(m):
    return m.group(1).title() + '-' + m.group(2).title()
#I-Say,Hello-World!  
print(re.sub(pattern,func, s))

```

### subn

re.subn(pattern, repl, string[, count])
返回 (sub(repl, string[, count]), 替换次数)

```python
import re
  
pattern = re.compile(r'(\w+) (\w+)')
s = 'i say, hello world!'
  
print re.subn(pattern,r'\2 \1', s)
  
def func(m):
    return m.group(1).title() + ' ' + m.group(2).title()
  
print re.subn(pattern,func, s)
```

作业：任意一个html页面中图片地址取出（所有）

例如 \<img  src = "xxxx" title ='xxx' style='xxx' class ='xxx'/\> 

取出 src之后的xxxx