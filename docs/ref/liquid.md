---
title: Liquid 语法样例
---

## 基本语法


- 输出变量的值

> &#123;&#123;page.title}}` = {{page.title}}

- 流程：条件控制

>  
> &#123;% if user %}
>
>   Hello &#123;&#123; user.name }}!
>
> &#123;% endif %}
>

- 过滤器

> &#123;&#123; "/my/fancy/url" &#124; append: ".html" }}
>
> = {{ "/my/fancy/url" | append: ".html" }}
> 
> &#123;&#123; "adam!" &#124; capitalize &#124; prepend: "Hello " }}
> 
> = {{ "adam!" | capitalize | prepend: "Hello " }}


## 操作符

`> == != > < >= <= or and`

> &#123;% if product.type == "Shirt" or product.type == "Shoes" %}

`contains`

> &#123;% if product.tags contains 'Hello' %}


## 变量赋值

{% raw %}
```
赋值 
{% assign my_variable = false %}

{% assign favorite_food = 'pizza' %}

{% assign age = 35 %}

{% capture my_variable %}
I am being captured.
{% endcapture %}

{% increment var %} # 自增
{% decrement variable %} # 自减
```
{% endraw %}


|code|value|
|:---|:---:|
|assign val01 = false {% assign val01 = false %}|{{val01}}|
|assign val02 = 'string' {% assign val02 = 'string' %}|{{val02}}|
|assign val03 = 56 {% assign val03 = 56 %}|{{val03}}|
|capture val04 {% capture val04 %}some messages{% endcapture %}|{{val04}}|
|assign val05 = '1,2,3'&#124;split: ',' {% assign val05 = '1,2,3'|split: ',' %}|{{val05}}|
|increment var06 {% increment var06 %}|{{var06}}|
|decrement var06 {% increment var06 %}|{{var07}}|

## `truthy or falsy`

> truthy : 
> `true` `string` `empty string`
> `0` `integer` `float` 
> `array` `empty array`
> `page` `EmptyDrop`

> falsy :
> `false` `nil`

## 类型

`string`
> "string"

`Number`
> `25` `39.756`

`Boolean`
> `true` `false`

`Nil`
> Nil is a special empty value that is returned when Liquid code has no results. 

`Array`
> &#123;% for user in site.users %}
> &#123;&#123; site.users[0] }}

> `for val in beatles`
{% assign beatles = "John, Paul, George, Ringo" | split: ", " %}
{% for val in beatles %}
>> {{-val-}}
{% endfor %} 
>> {{beatles[1]}}

## 过滤流程中的空白字符

&#123;&#123;-,-}}
&#123;%-,-%}


## 注释
&#123;% comment %}
&#123;% endcomment %}

> &#123;% comment %} 一些注释 &#123;% endcomment %}
> {% comment %} 一些注释 {% endcomment %}


## 控制流

```
% if product.title == 'Awesome Shoes' %
... 
% elsif customer.name == 'anonymous' %
...
% endif %
```

```
% unless product.title == 'Awesome Shoes' %
...
% endunless %
```

```
% assign handle = 'cake' %
% case handle %
  % when 'cake' %
     This is a cake
  % when 'cookie' %
     This is a cookie
  % else %
     This is not a cake nor a cookie
% endcase %
```

## 迭代

```
% for product in collection.products %
...
% endfor %
```

```
% for i in (1..5) %
  % if i == 4 %
    % break %
  % else %
     i 
     % continue %
  % endif %
% endfor %
```

```
<!-- if array = [1,2,3,4,5,6] -->
% for item in array limit:2 %
  > item  # 1 2
% endfor %
```

```
<!-- if array = [1,2,3,4,5,6] -->
% for item in array offset:2 %
  > item  # 3 4 5 6
% endfor %
```

```
% assign num = 4 %
% for i in (1..num) %
% for item in array reversed %
```

## cycle

```
% cycle 'one', 'two', 'three' % # one
% cycle 'one', 'two', 'three' % # two
% cycle 'one', 'two', 'three' % # three
% cycle 'one', 'two', 'three' % # one
```

## table 

```
% tablerow product in collection.products %  # tr class=row1
  > product.title # td class=col1, td class=col2
% endtablerow %
```

```
% tablerow product in collection.products cols:2 % # tr class=row1,tr class=row2
  > product.title # td class=col1, td class=col2
% endtablerow %
```

```
% tablerow product in collection.products cols:2 limit:3 %
% tablerow product in collection.products cols:2 offset:3 %
```

## raw 

```
% raw % 
...
% endraw %
```
{% raw %}
  In Handlebars, {{ this }} will be HTML-escaped, but
  {{{ that }}} will not.
{% endraw %}


## filter 过滤器

{% raw %}
>*-* filter 需要被`{{`-`}}`或`{%`-`%}`包围才能起作用，样例中省略了`{}`  
>*-* value|filter:arg 在样例中省略为 value:arg  
{% endraw %}

|filter|example|desc|
|:---:|---|---|
|**数字**|||
|abs| -17 >> {{-17|abs}}|绝对值,对纯数字的字符串有效，如"-19.82"|
|ceil|1.2 >> {{ 1.2 | ceil }}||
|floor|1.2 >> {{ 1.2 | floor }}||
|divided_by|16:4 >> {{ 16 | divided_by: 4 }} <br> 16.0:4 >> {{ 16.0 | divided_by: 4 }} <br> 20:7 >>{{ 20 | divided_by: 7 }} <br> 20:7.0 >> {{ 20 | divided_by: 7.0 }} <br> 20.0 >> 7 {{ 20.0 | divided_by: 7 }}|除法|
|times|16:4 >> {{ 16 | times: 4 }} <br> 16.0:4 >> {{ 16.0 | times: 4 }}|乘法|
|minus|4:2 >> {{ 4 | minus: 2 }}|减法|
|plus|4:2 >> {{ 4 | plus: 2 }}|加法|
|modulo|3:2 >> {{ 3 | modulo: 2 }}|取余|
|round|1.2 >> {{ 1.2 | round }}|四舍五入|
|at_least|4 :5 {{ 4 | at_least: 5 }} <br> 4 :3 >> {{ 4 | at_least: 3 }}||
|at_most|4 :5 >> {{ 4 | at_most: 5 }} <br> 4 :3 >> {{ 4 | at_most: 3 }}||
|**字符串**|||
|append|a :b >> {{'a'|append:'b'}}||
|prepend|a:b >> {{'a'|prepend:'b'}}||
|capitalize|'great title' >> {{ "great title" | capitalize }}|字符串首字母大写|
|downcase|Parker Moore >> {{ "Parker Moore" | downcase }}||
|upcase|||
|escape|"='a&b'?" >> `{{ "='a&b'?" | escape }}`||
|escape_once|`2 &amp; 3` >> `{{ "2 &amp; 3" | escape_once }}`||
|strip|||
|lstrip|'   s   '>>{{ '   s   ' | lstrip }}.||
|rstrip|||
|strip_html||删除html标签|
|strip_newlines||删除换行|
|remove|'abcbd':'b' >> {{'abcbd'|remove:'b'}}||
|remove_first|||
|replace|'abcbd':'b','e' >> {{'abcbd'|replace:'b','e'}}||
|replace_first|||
|newline_to_br| |\n转换成&lt;br&gt;|
|size|||
|slice|'Liquid':-3,2 >> {{ "Liquid" | slice: -3, 2 }}|下标[,长度] 当一个参数时返回下标所在字符|
|truncate|'一些文字描述':5>>{{'一些文字描述'|truncate:5,'..'}}|长度[,替换字符] 截断字符串并添加...|
|truncatewords||截断词组|
|url_decode|||
|url_encode|||
|**日期**|||
|date|'now':%Y-%m-%d %H:%M:%S >> {{ "now" | date: "%Y-%m-%d %H:%M:%S" }} <br> '2018-12-13 23:13:24 +0800':"%F %T" >> {{'2018-12-13 23:13:24 +0800'|date:"%F %T"}}||
|**工具**||| 
|default|undefined-val : 'undefined' >> {{ undefined-val | default: 'undefined' }}|变量未定义或为值为空时输出默认值|
|**数组**|[1,2] >> '1,2'&#124;split:','||
|split|'1,2':',' >> {{'1,2'|split:','}}||
|join|[1,2]:'-' >> {{ '1,2'|split:',' | join: "-" }}||
|array.first|[1,2].first >> {% assign arr01 = '1,2'|split:','%} {{arr01.first}}||
|array.last|[1,2].last >> {{arr01.last}}||
|compact|assign site_categories = site.pages &#124; map: 'category' &#124; compact |删除数组中所有 nil 值|
|concat|a=1,2;b=5,6;a :b >> {% assign a = '1,2' | split: ',' %} {% assign b = '5,6' | split: ',' %} {{a|concat:b}}|连接两个数组|
|map|&#123;% assign cs = site.pages &#124; map: "category" %}|提取pages中每个page的category属性，组成新的数组 cs|
|reverse|[1,2]>>{{'1,2' | split: ','|reverse}}||
|size|[1,2] >> {{'1,2' | split: ','|size}}|支持array.size和字符串|
|slice|[1,2,3,4,5]:2,4 >> {{'1,2,3,4,5'|split:','|slice:2,4}}||
|sort|||
|sort_natural||排序忽略大小写|
|uniq|[1,2,3,3,2,2]>>{{'1,2,3,3,2,2'|split:','|uniq}}|删除重复数据，保留唯一值|


## filters in jekyll

|filter|example|desc|
|:---:|---|---|
|relative_url|||
|absolute_url|||
|where|site.members:"graduation_year","2014"|member.graduation_year==2014|
|where_exp|site.members:"item","item.graduation_year < 2014" |>=3.2.0|
|group_by|site.members:"graduation_year" <br> >> [{"name"=>"2013", "items"=>[...]},{"name"=>"2014", "items"=>[...]}]||
|group_by_exp|site.members: "item", "item.graduation_year &#124;truncate: 3, ''" <br> >>[{"name"=>"201", "items"=>[...]},{"name"=>"200", "items"=>[...]}]|>=3.4.0|
|xml_escape|||
|cgi_escape||%XX|
|uri_escape|||
|number_of_words|||
|array_to_sentence_string|[1,2,3]>>{{'1,2,3'|split:','|array_to_sentence_string:'or'}}|[最后的连接字符串]|
|markdownify||md to html|
|smartify|||
|sassify|||
|scssify|||
|slugify| {{ "The _config.yml file" | slugify }} <br> {{ "The _config.yml file" | slugify: "pretty" }} <br> {{ "The _cönfig.yml file" | slugify: "ascii" }} <br> {{ "The cönfig.yml file" | slugify: "latin" }}|参数：none<br>raw 过滤空白字符<br>default 非数字和字符串<br>pretty 特殊字符<br>ascii<br>latin  >=3.7.0<br>]|
|jsonify|[1,2,3]>>{{'1,2,3'|split:','|jsonify}}|to JSON|
|normalize_whitespace||替换多余的空白为单个空格|
|sort|site.pages: "title", "last" |[属性],[first,last]依据属性值排序,当属性不存在时排序在前或在后|
|sample|[1,2,3,4]:2 >> {{'1,2,3,4'|split:','|sample:2}} |[个数]随机获取元素|
|array filters||push:val <br> pop <br> shift <br> unshift:val|
|inspect|[1,2,3] >> {{'1,2,3'|split:','|inspect}}|转换对象为字符串 用于调试|


## jekyll tags

**- highlight**

{% raw %}
{% highlight ruby linenos%}
def foo
  puts 'foo'
end
{% endhighlight %}
{% endraw %}
>
{% highlight ruby linenos %}
def foo
  puts 'foo'
end
{% endhighlight %}

**- link**

link 和 post_url 的目标文件必须已存在
{% raw %}
{{ site.baseurl }}{% link about.md %}
{{ site.baseurl }}{% post_url 2010-07-21-name-of-post %}
{% endraw %}
{{ site.baseurl }}{% link about.md %}
[end]


* [liquid](http://shopify.github.io/liquid)
* liquid - [cn](https://liquid.bootcss.com/basics/introduction/)
* [jekyll liquid](https://jekyllrb.com/docs/liquid/filters/)
* dateformat [sftime](http://strftime.net/)
* date input format [time](https://ruby-doc.org/stdlib-2.5.3/libdoc/time/rdoc/Time.html#method-c-parse)

* highlight [lexers](http://pygments.org/docs/lexers/)
* highlight [languages](https://github.com/jneen/rouge/wiki/List-of-supported-languages-and-lexers)
