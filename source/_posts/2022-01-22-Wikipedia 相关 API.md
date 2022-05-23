---
title: Wikipedia 相关 API
date: 2022-01-22 17:56:40
tags: 
- NLP
categories: 
- NLP
---



## wikipedia 使用教程

https://pypi.org/project/wikipedia/

https://github.com/goldsmith/Wikipedia

https://www.codenong.com/s-getting-started-with-pythons-wikipedia-api/

### 安装

```python
pip install wikipedia 
```

### 根据title搜索维基百科文章

search()方法在Wikipedia中搜索作为其参数提供的查询，返回包含该查询的所有文章标题的列表。 


```python
import wikipedia 
print(wikipedia.search("Bill"))
# ['Bill', 'The Bill', 'Bill Nye', 'Bill Gates', 'Bills, Bills, Bills', 'Heartbeat bill', 'Bill Clinton', 'Buffalo Bill', 'Bill & Ted', 'Kill Bill: Volume 1'] 

print(wikipedia.search("Bill", results=2))
# ['Bill', 'The Bill']
```

 suggest()方法返回与作为参数输入的搜索查询相关的建议，如果找不到建议，它将返回" None"。


```python
import wikipedia
print(wikipedia.suggest("Bill cliton"))
# bill clinton
# 输入了错误的" Bill clinton"，并返回了正确的建议" bill clinton"
```



### 提取维基百科文章摘要

使用summary()方法提取Wikipedia文章的摘要。 


```python
print(wikipedia.summary("Ubuntu"))  # 提取" Ubuntu"的摘要
"""
Ubuntu ( (listen)) is a free and open-source Linux distribution based on Debian. Ubuntu is officially released in three editions: Desktop, Server, and Core (for the internet of things devices and robots). Ubuntu is a popular operating system for cloud computing, with support for OpenStack.Ubuntu is released every six months, with long-term support (LTS) releases every two years. The latest release is 19.04 ("Disco Dingo"), and the most recent long-term support release is 18.04 LTS ("Bionic Beaver"), which is supported until 2028. Ubuntu is developed by Canonical and the community under a meritocratic governance model. Canonical provides security updates and support for each Ubuntu release, starting from the release date and until the release reaches its designated end-of-life (EOL) date. Canonical generates revenue through the sale of premium services related to Ubuntu. Ubuntu is named after the African philosophy of Ubuntu, which Canonical translates as"humanity to others" or"I am what I am because of who we all are".
"""
```

 通过配置方法的sentences参数，我们可以自定义要显示的摘要文本中的句子数。


```python
print(wikipedia.summary("Ubuntu", sentences=2))
# Ubuntu ( (listen)) is a free and open-source Linux distribution based on Debian. Ubuntu is officially released in three editions: Desktop, Server, and Core (for the internet of things devices and robots).
```

如果页面不存在或页面是明确的，则wikipedia.summary将引发"歧义消除错误"。 


```python
print(wikipedia.summary("key"))  # 抛出DisambiguationError，因为有许多文章与" key"匹配。
```

通过更具体的查询，可以在输出中获得正确的摘要。


```python
print(wikipedia.summary("Key (cryptography)"))
```



### 维基百科页面对象

为了获取Wikipedia页面的内容，类别，坐标，图像，链接和其他元数据，我们必须首先获取Wikipedia页面对象或页面的页面ID，可以通过page()方法来获取。

```python
wikipedia.page("Ubuntu")  # 返回一个WikipediaPage对象
```


然后调用该类的函数或者变量来获取关于文章的更多信息。


```python
print(wikipedia.page("Python").content)  # 完整纯文本内容(不包括图像，表格等)
print(wikipedia.page("Python").url)  # 页面的URL
print(wikipedia.page("Python").references)  # 外部链接的URL
```


```python
print(wikipedia.page("Python").title)  # 提取页面标题
print(wikipedia.page("Python").categories)  # 页面的类别列表
print(wikipedia.page("Ubuntu").links)  # 获取页面中存在链接的页面标题列表
```



#### 根据坐标查找页面

geosearch()方法根据提供的坐标返回文章。


```python
print(wikipedia.geosearch(37.787, -122.4))
"""
['140 New Montgomery', 'New Montgomery Street', 'Cartoon Art Museum', 'San Francisco Bay Area Planning and Urban Research Association', 'Academy of Art University', 'The Montgomery (San Francisco)', 'California Historical Society', 'Palace Hotel Residential Tower', 'St. Regis Museum Tower', 'Museum of the African Diaspora']
"""
```

同样，我们可以设置page()的坐标属性，并获取与地理位置有关的文章。

```python
print(wikipedia.page(37.787, -122.4))
"""
['140 New Montgomery', 'New Montgomery Street', 'Cartoon Art Museum', 'San Francisco Bay Area Planning and Urban Research Association', 'Academy of Art University', 'The Montgomery (San Francisco)', 'California Historical Society', 'Palace Hotel Residential Tower', 'St. Regis Museum Tower', 'Museum of the African Diaspora']
"""
```


#### 语言设定

通过使用set_lang()方法可以将Wikipedia页面的语言自定义为某种语言。  每种语言都有一个标准的前缀代码，该代码作为参数传递给该方法。 


```python
wikipedia.set_lang("de")  
print(wikipedia.summary("ubuntu", sentences=2))  # 以德语获取" Ubuntu" Wiki页面的摘要文本的前两个句子。
"""
Ubuntu (auch Ubuntu Linux) ist eine Linux-Distribution, die auf Debian basiert. Der [Name](http://www.google.com/search?hl=en&q=allinurl%3Adocs.oracle.com+javase+docs+api+name) Ubuntu bedeutet auf Zulu etwa ?Menschlichkeit" und bezeichnet eine afrikanische Philosophie.
"""
```




```python
print(wikipedia.languages())  # 检查当前支持的ISO语言列表及其前缀。
```



#### 检索维基百科页面中的图像和完整HTML页面内容

从Wikipedia页面获取图像。


```python
print(wikipedia.page("ubuntu").images[0])  #  从Wikipedia的Ubuntu页面返回第一个图像的链接
```

获取HTML格式的完整Wikipedia页面。


```python
print(wikipedia.page("Ubuntu").html())
"""
<div class="mw-parser-output"><div role="note" class="hatnote navigation-not-searchable">For the African philosophy, see <a href="/wiki/Ubuntu_philosophy" title="Ubuntu philosophy">Ubuntu philosophy</a>. For other uses, see <a href="/wiki/Ubuntu_(disambiguation)" class="mw-disambig" title="Ubuntu (disambiguation)">Ubuntu (disambiguation)</a>.</div> <div class="shortdescription nomobile noexcerpt noprint searchaux" style="display:none">Linux distribution based on Debian</div> ...
"""
```



## Wikipedia API 使用教程

https://pypi.org/project/Wikipedia-API/

https://github.com/martin-majlis/Wikipedia-API/

### 安装

```
pip install Wikipedia-API
```

`Wikipedia-API`是

### 基本使用

```python
import wikipediaapi

title = "china"
wiki = wikipediaapi.Wikipedia(
    language='en',
    extract_format=wikipediaapi.ExtractFormat.WIKI
)
page = wiki.page(title)
language = "zh"
lpage = page.langlinks[language]  # fr es ...
print(lpage.text)
```

### Installation

This package requires at least Python 3.4 to install because it’s using IntEnum.

```
pip install wikipedia-api
```

### Usage

Goal of `Wikipedia-API` is to provide simple and easy to use API for retrieving informations from Wikipedia. Bellow are examples of common use cases.

#### Importing

```
import wikipediaapi
```

#### How To Get Single Page

Getting single page is straightforward. You have to initialize `Wikipedia` object and ask for page by its name. It’s parameter language has be one of [supported languages](http://meta.wikimedia.org/wiki/List_of_Wikipedias).

```
import wikipediaapi
    wiki_wiki = wikipediaapi.Wikipedia('en')

    page_py = wiki_wiki.page('Python_(programming_language)')
```

#### How To Check If Wiki Page Exists

For checking, whether page exists, you can use function `exists`.

```
page_py = wiki_wiki.page('Python_(programming_language)')
print("Page - Exists: %s" % page_py.exists())
# Page - Exists: True

page_missing = wiki_wiki.page('NonExistingPageWithStrangeName')
print("Page - Exists: %s" %     page_missing.exists())
# Page - Exists: False
```

#### How To Get Page Summary

Class `WikipediaPage` has property `summary`, which returns description of Wiki page.

```
import wikipediaapi
    wiki_wiki = wikipediaapi.Wikipedia('en')

    print("Page - Title: %s" % page_py.title)
    # Page - Title: Python (programming language)

    print("Page - Summary: %s" % page_py.summary[0:60])
    # Page - Summary: Python is a widely used high-level programming language for
```

#### How To Get Page URL

`WikipediaPage` has two properties with URL of the page. It is `fullurl` and `canonicalurl`.

```
print(page_py.fullurl)
# https://en.wikipedia.org/wiki/Python_(programming_language)

print(page_py.canonicalurl)
# https://en.wikipedia.org/wiki/Python_(programming_language)
```

#### How To Get Full Text

To get full text of Wikipedia page you should use property `text` which constructs text of the page as concatanation of summary and sections with their titles and texts.

```
wiki_wiki = wikipediaapi.Wikipedia(
        language='en',
        extract_format=wikipediaapi.ExtractFormat.WIKI
)

p_wiki = wiki_wiki.page("Test 1")
print(p_wiki.text)
# Summary
# Section 1
# Text of section 1
# Section 1.1
# Text of section 1.1
# ...


wiki_html = wikipediaapi.Wikipedia(
        language='en',
        extract_format=wikipediaapi.ExtractFormat.HTML
)
p_html = wiki_html.page("Test 1")
print(p_html.text)
# <p>Summary</p>
# <h2>Section 1</h2>
# <p>Text of section 1</p>
# <h3>Section 1.1</h3>
# <p>Text of section 1.1</p>
# ...
```

#### How To Get Page Sections

To get all top level sections of page, you have to use property `sections`. It returns list of `WikipediaPageSection`, so you have to use recursion to get all subsections.

```
def print_sections(sections, level=0):
        for s in sections:
                print("%s: %s - %s" % ("*" * (level + 1), s.title, s.text[0:40]))
                print_sections(s.sections, level + 1)


print_sections(page_py.sections)
# *: History - Python was conceived in the late 1980s,
# *: Features and philosophy - Python is a multi-paradigm programming l
# *: Syntax and semantics - Python is meant to be an easily readable
# **: Indentation - Python uses whitespace indentation, rath
# **: Statements and control flow - Python's statements include (among other
# **: Expressions - Some Python expressions are similar to l
```

#### How To Get Page In Other Languages

If you want to get other translations of given page, you should use property `langlinks`. It is map, where key is language code and value is `WikipediaPage`.

```
def print_langlinks(page):
        langlinks = page.langlinks
        for k in sorted(langlinks.keys()):
            v = langlinks[k]
            print("%s: %s - %s: %s" % (k, v.language, v.title, v.fullurl))

print_langlinks(page_py)
# af: af - Python (programmeertaal): https://af.wikipedia.org/wiki/Python_(programmeertaal)
# als: als - Python (Programmiersprache): https://als.wikipedia.org/wiki/Python_(Programmiersprache)
# an: an - Python: https://an.wikipedia.org/wiki/Python
# ar: ar - بايثون: https://ar.wikipedia.org/wiki/%D8%A8%D8%A7%D9%8A%D8%AB%D9%88%D9%86
# as: as - পাইথন: https://as.wikipedia.org/wiki/%E0%A6%AA%E0%A6%BE%E0%A6%87%E0%A6%A5%E0%A6%A8

page_py_cs = page_py.langlinks['cs']
print("Page - Summary: %s" % page_py_cs.summary[0:60])
# Page - Summary: Python (anglická výslovnost [ˈpaiθtən]) je vysokoúrovňový sk
```

#### How To Get Links To Other Pages

If you want to get all links to other wiki pages from given page, you need to use property `links`. It’s map, where key is page title and value is `WikipediaPage`.

```
def print_links(page):
        links = page.links
        for title in sorted(links.keys()):
            print("%s: %s" % (title, links[title]))

print_links(page_py)
# 3ds Max: 3ds Max (id: ??, ns: 0)
# ?:: ?: (id: ??, ns: 0)
# ABC (programming language): ABC (programming language) (id: ??, ns: 0)
# ALGOL 68: ALGOL 68 (id: ??, ns: 0)
# Abaqus: Abaqus (id: ??, ns: 0)
# ...
```

#### How To Get Page Categories

If you want to get all categories under which page belongs, you should use property `categories`. It’s map, where key is category title and value is `WikipediaPage`.

```
def print_categories(page):
        categories = page.categories
        for title in sorted(categories.keys()):
            print("%s: %s" % (title, categories[title]))


print("Categories")
print_categories(page_py)
# Category:All articles containing potentially dated statements: ...
# Category:All articles with unsourced statements: ...
# Category:Articles containing potentially dated statements from August 2016: ...
# Category:Articles containing potentially dated statements from March 2017: ...
# Category:Articles containing potentially dated statements from September 2017: ...
```

#### How To Get All Pages From Category

To get all pages from given category, you should use property `categorymembers`. It returns all members of given category. You have to implement recursion and deduplication by yourself.

```
def print_categorymembers(categorymembers, level=0, max_level=1):
        for c in categorymembers.values():
            print("%s: %s (ns: %d)" % ("*" * (level + 1), c.title, c.ns))
            if c.ns == wikipediaapi.Namespace.CATEGORY and level < max_level:
                print_categorymembers(c.categorymembers, level=level + 1, max_level=max_level)


cat = wiki_wiki.page("Category:Physics")
print("Category members: Category:Physics")
print_categorymembers(cat.categorymembers)

# Category members: Category:Physics
# * Statistical mechanics (ns: 0)
# * Category:Physical quantities (ns: 14)
# ** Refractive index (ns: 0)
# ** Vapor quality (ns: 0)
# ** Electric susceptibility (ns: 0)
# ** Specific weight (ns: 0)
# ** Category:Viscosity (ns: 14)
# *** Brookfield Engineering (ns: 0)
```

#### How To See Underlying API Call

If you have problems with retrieving data you can get URL of undrerlying API call. This will help you determine if the problem is in the library or somewhere else.

```
import wikipediaapi
import sys
wikipediaapi.log.setLevel(level=wikipediaapi.logging.DEBUG)

# Set handler if you use Python in interactive mode
out_hdlr = wikipediaapi.logging.StreamHandler(sys.stderr)
out_hdlr.setFormatter(wikipediaapi.logging.Formatter('%(asctime)s %(message)s'))
out_hdlr.setLevel(wikipediaapi.logging.DEBUG)
wikipediaapi.log.addHandler(out_hdlr)

wiki = wikipediaapi.Wikipedia(language='en')

page_ostrava = wiki.page('Ostrava')
print(page_ostrava.summary)
# logger prints out: Request URL: http://en.wikipedia.org/w/api.php?action=query&prop=extracts&titles=Ostrava&explaintext=1&exsectionformat=wiki
```

### External Links

- [GitHub](https://github.com/martin-majlis/Wikipedia-API/)
- [PyPi](https://pypi.python.org/pypi/Wikipedia-API/)
- [Travis](https://travis-ci.org/martin-majlis/Wikipedia-API/)
- [ReadTheDocs](http://wikipedia-api.readthedocs.io/)

