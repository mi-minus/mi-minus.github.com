---
layout: life
title: bs4(BeautifulSoup)
category: Crawlers
duoshuo: true
date: 2017-10-22
---

******

	作者: minus
	版本: V 0.0.1
	日期: 2017年10月22日

<!-- more -->

*******


中文官方教程：https://www.crummy.com/software/BeautifulSoup/bs4/doc.zh/

#### 1、导入方式  
```
使用BeautifulSoup解析这段代码,能够得到一个 BeautifulSoup 的对象,并能按照标准的缩进格式的结构输出:
frombs4importBeautifulSoup 
soup=BeautifulSoup(html_doc) 
print(soup.prettify()) 
```
 

* 直接拿到链接：
```link.get('href') ```

* 直接拿到内容：
```link.get_text()```

*直接内容去空：
```soup.get_text("|", strip=True)```

```soup.find_all("a",text="Elsie")```

```css_soup.find_all("p",class_="body strikeout")```

```soup.find_all(class_=re.compile("itl"))```

```soup.find_all("a",attrs={"class":"sister"})```

* 正则表达形式：
```userSoupList = soup.findAll(name="h1", attrs={"class":re.compile(r"h1user(\s\w+)?")});```

```soup.select("body a")```

```soup.select("html head title")```

* 找到某个tag标签下的直接子标签
```soup.select("head > title")```

几个简单的浏览结构化数据的方法:
```
soup.title
soup.title.name
soup.title.parent.name
soup.p
soup.p['class']
soup.a
soup.find_all('a')
soup.find(id="link3")
```

* 从文档中找到所有<a>标签的链接:
```forlinkinsoup.find_all('a'):print(link.get('href'))```

* 从文档中获取所有文字内容:
```print(soup.get_text())```

#### 2、安装方式

Beautiful Soup支持Python标准库中的HTML解析器,还支持一些第三方的解析器,其中一个是 lxml
```
$apt-get install Python-lxml
$ pip install lxml
```

另一个可供选择的解析器是纯Python实现的 html5lib , html5lib的解析方式与浏览器相同,可以选择下列方法来安装html5lib:
```
$easy_install html5lib
$pipinstallhtml5lib
```

* 使用方法：
```
BeautifulSoup(markup,'html.parser')
BeautifulSoup(markup,'lxml')
BeautifulSoup(markup,['lxml','xml'])
BeautifulSoup(markup,'html5lib')
```

* 导入方式：
```
from bs4 import BeautifulSoup
```

* 对象种类：
```
Beautiful Soup将复杂HTML文档转换成一个复杂的树形结构,每个节点都是Python对象,所有对象可以归纳为4种:
Tag , NavigableString, BeautifulSoup, Comment.
```

* 遍历文档树：
```
(1)Tag: Tag 对象与XML或HTML原生文档中的tag相同:
soup=BeautifulSoup('<b class="boldest">Extremely bold</b>')tag=soup.btype(tag)# <class 'bs4.element.Tag'>
tag中最重要的属性: name和attributes
tag.name   #name # u'b'
----------------------------
tag['class']  #attribute# u'boldest'
or 
tag.attrs# {u'class': u'boldest'}
tag的属性可以被添加,删除或修改 
-----------------------------
tag.string# u'Extremely bold'
----------------------------
tag的 .contents 属性可以将tag的子节点以列表的方式输出 
字符串没有 .contents 属性,因为字符串没有子节点: 
----------------------------
通过tag的 .children 生成器,可以对tag的子节点进行循环: 
---------------------------
.descendants 属性可以对所有tag的子孙节点进行递归循环 
len(list(soup.children))# 1len(list(soup.descendants))# 25
----------------------------
如果tag中包含多个字符串 [2] ,可以使用 .strings 来循环获取: 
forstringinsoup.strings:print(repr(string))
输出的字符串中可能包含了很多空格或空行,使用 .stripped_strings 可以去除多余空白内容
forstringinsoup.stripped_strings:print(repr(string))
----------------------------
通过 .parent 属性来获取某个元素的父节点 
title_tag=soup.titletitle_tag# <title>The Dormouse's story</title>title_tag.parent# <head><title>The Dormouse's story</title></head>
-----------------------------
.parents 属性可以递归得到元素的所有父辈节点（包括外层html,body,p等一级级的都显示出来）
-----------------------------
.next_sibling 和 .previous_sibling 属性来查询兄弟节点: 
.next_siblings 和 .previous_siblings 属性可以对当前节点的兄弟节点迭代输出 
-----------------------------
.next_element 和 .previous_element：指向解析过程中下一个被解析的对象(字符串或tag),结果可能与 .next_sibling 相同,但通常是不一样的.
.next_elements 和 .previous_elements 的迭代器就可以向前或向后访问文档的解析内容,就好像文档正在被解析一样: 
-----------------------------
```
#### (2)Name: 
* 搜索文档树：
```
Beautiful Soup定义了很多搜索方法,这里着重介绍2个: find() 和 find_all() .其它方法的参数和用法类似
---------------------------
查找文档中所有的<b>标签：
soup.find_all('b')# [<b>The Dormouse's story</b>]
------------------------------
正则表达式作为参数,Beautiful Soup会通过正则表达式的 match() 来匹配内容找出所有以b开头的标签,这表示<body>和<b>标签都应该被找到:
importrefortaginsoup.find_all(re.compile("^b")):print(tag.name)# body# b
--------------------------
传入列表参数,Beautiful Soup会将与列表中任一元素匹配的内容返回.下面代码找到文档中所有<a>标签和<b>标签:
http://www.crummy.com/software/BeautifulSoup/bs4/doc/index.zh.html
--------------------------------------
soup.find_all(["a","b"])# [<b>The Dormouse's story</b>,# <a class="sister" href="http://example.com/elsie" id="link1">Elsie</a>,# <a class="sister" href="http://example.com/lacie" id="link2">Lacie</a>,# <a class="sister" href="http://example.com/tillie" id="link3">Tillie</a>]
--------------------------
True 可以匹配任何值,下面代码查找到所有的tag,但是不会返回字符串节点 
fortaginsoup.find_all(True):print(tag.name)# html# head# title# body# p# b# p# a# a# a# p
--------------------------
如果没有合适过滤器,那么还可以定义一个方法,方法只接受一个元素参数 [4] ,如果这个方法返回 True 表示当前元素匹配并且被找到,如果不是则反回 False：
下面方法校验了当前元素,如果包含 class 属性却不包含 id 属性,那么将返回 True: 
defhas_class_but_no_id(tag):return tag.has_attr('class') and not tag.has_attr('id')
soup.find_all(has_class_but_no_id)# [<p class="title"><b>The Dormouse's story</b></p>,
#  <p class="story">Once upon a time there were...</p>,
#  <p class="story">...</p>]
------------------------------------
find_all( name , attrs , recursive , text , **kwargs )
find_all() 方法搜索当前tag的所有tag子节点,并判断是否符合过滤器的条件 
soup.find_all("title")
soup.find_all("p","title")
soup.find_all("a")
soup.find_all(id="link2")
importresoup.find(text=re.compile("sisters"))
参数详解：find_all( name , attrs , recursive , text , **kwargs )
----------------------------------
name:
name 参数可以查找所有名字为 name 的tag,字符串对象会被自动忽略掉.
soup.find_all("title")
搜索 name 参数的值可以使任一类型的 过滤器 ,字符窜,正则表达式,列表,方法或是 True
----------------------------------
keyword:
如果一个指定名字的参数不是搜索内置的参数名,搜索时会把该参数当作指定名字tag的属性来搜索,如果包含一个名字为 id 的参数,Beautiful Soup会搜索每个tag的”id”属性. 
soup.find_all(id='link2')# [<a class="sister" href="http://example.com/lacie" id="link2">Lacie</a>]
-----
soup.find_all(href=re.compile("elsie"))# [<a class="sister" href="http://example.com/elsie" id="link1">Elsie</a>]
搜索指定名字的属性时可以使用的参数值包括 字符串 , 正则表达式 , 列表, True. 
----
soup.find_all(id=True)  包含id就可以
----
使用多个指定名字的参数可以同时过滤tag的多个属性: 
soup.find_all(href=re.compile("elsie"),id='link1')
---
有些tag属性在搜索不能使用,比如HTML5中的 data-* 属性: 
但是可以通过 find_all() 方法的 attrs 参数定义一个字典参数来搜索包含特殊属性的tag: 
data_soup.find_all(attrs={"data-foo": "value"})
---------------------------------
```
* Css:
```
---
soup.find_all("a",class_="sister")
---
class_ 参数同样接受不同类型的 过滤器 ,字符串,正则表达式,方法或 True : 
soup.find_all(class_=re.compile("itl"))
---
defhas_six_characters(css_class):returncss_classisnotNoneandlen(css_class)==6soup.find_all(class_=has_six_characters)
---
tag的 class 属性是 多值属性 .按照CSS类名搜索tag时,可以分别搜索tag中的每个CSS类名:
css_soup=BeautifulSoup('<p class="body strikeout"></p>')css_soup.find_all("p",class_="strikeout")# [<p class="body strikeout"></p>]
--- css_soup.find_all("p",class_="body")# [<p class="body strikeout"></p>]
css_soup.find_all("p",class_="body strikeout")# [<p class="body strikeout"></p>]
---
soup.find_all("a",attrs={"class": "sister"})
---------------------------------
```
* Text:
```
通过 text 参数可以搜搜文档中的字符串内容.与 name 参数的可选值一样, text 参数接受 字符串 , 正则表达式 , 列表, True
soup.find_all(text="Elsie")
soup.find_all(text=["Tillie", "Elsie", "Lacie"])
soup.find_all(text=re.compile("Dormouse"))
def is_the_only_string_within_a_tag(s):
    ""Return True if this string is the only child of its parent tag.""
    return (s == s.parent.string)
soup.find_all(text=is_the_only_string_within_a_tag)
---
```

* 虽然 text 参数用于搜索字符串,还可以与其它参数混合使用来过滤tag.Beautiful Soup会找到 .string 方法与 text 参数值相符的tag
```
soup.find_all("a",text="Elsie")
----------------------------------
Limit:
---
文档树中有3个tag符合搜索条件,但结果只返回了2个,因为我们限制了返回数量: 
soup.find_all("a",limit=2)
# [<a class="sister" href="http://example.com/elsie" id="link1">Elsie</a>,#  <a class="sister" href="http://example.com/lacie" id="link2">Lacie</a>]
--------------------------------
Recursive:
调用tag的 find_all() 方法时,Beautiful Soup会检索当前tag的所有子孙节点,如果只想搜索tag的直接子节点,可以使用参数 recursive=False :
find( name , attrs , recursive , text , **kwargs )
-------------
以下为等价情况
soup.find_all('title',limit=1)# [<title>The Dormouse's story</title>]soup.find('title')# <title>The Dormouse's story</title>
唯一的区别是 find_all() 方法的返回结果是值包含一个元素的列表,而 find() 方法直接返回结果. 
find_all() 方法没有找到目标是返回空列表, find() 方法找不到目标时,返回 None . 
forlinkinsoup.find_all('a'): print(link.get('href')) # http://example.com/elsie # http://example.com/lacie # http://example.com/tillie
print(soup.get_text())
```


