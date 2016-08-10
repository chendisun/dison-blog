title: markdown基本语法
date: 2015-09-01 18:16:15
categories:
- 学习
tags:
- markdown
---

## 标题

~~~html
#  H1
##  H2
###  H3
####  H4
#####  H5
######  H6
~~~
另外，H1和H2还能用以下方式显示：
~~~html
一级标题
===
 
二级标题
---
~~~
<!--more-->

## 文本强调
~~~html
*斜体* or _强调_
**加粗** or __加粗__
***粗斜体*** or ___粗斜体__
~~~
但是，如果你的 * 和 _ 两边都有空白的话，它们就只会被当成普通的符号：这是一段* 文本强调 *的说明示例。
如果要在文字前后直接插入普通的星号或底线，你可以用反斜线（转义符）：\

## 列表

--- 无序列表
~~~html
* 无序列表
* 无序列表
* 无序列表

+ 无序列表
+ 无序列表
+ 无序列表

- 无序列表
- 无序列表
- 无序列表
~~~

--- 有序列表
~~~html
1. 第一行
2. 第二行
3. 第三行
~~~

## 连接（title为可选项）
~~~html
内嵌方式：
[link text](https://www.google.com "title text")
 
引用方式：
[link text][id]
[id]: https://www.mozilla.org "title text"
 
引用存储文件：
[link text](../path/file/readme.text "title text")
 
还能这样使用：
[link text][]
[link text]: http://www.reddit.com
 
Email 邮件：
<example@example.com>
~~~

## 图片
~~~html
内嵌方式：
![alt text](https://github.com/adam-p/markdown-here/raw/master/src/common/images/icon48.png "title text")
 
引用方式：
![alt text][logo]
[logo]: https://github.com/adam-p/markdown-here/raw/master/src/common/images/icon48.png "title text"
~~~
## 代码和语法高亮
标记一小段行内代码：

本文是一篇介绍`Markdown`的语法的文章
 
如果高亮的内容包含`号，可以这样写：
~~~bash
`` `包裹起来` ``
~~~
 
语法高亮：
~~~bash
```html
    <div>Syntax Highlighting</div>
```

```css
    body{font-size:12px}
```
 
```javascript
    var s = "JavaScript syntax highlighting";
    alert(s);
```
```php
    <?php
      echo "hello, world!";
    ?>
```
```python
    s = "Python syntax highlighting"
    print s
```
~~~

## 水平分割线
```html
***
* * *
- - -
```

## 转义符(反斜杠)
Markdown 可以利用反斜杠来插入一些在语法中有其它意义的符号，例如：如果你想要用星号加在文字旁边的方式来做出强调效果，你可以在星号的前面加上反斜杠：
```html
\*literal asterisks\*
```

Markdown 支持以下这些符号前面加上反斜杠来帮助插入普通的符号：
```html
\反斜杠  `反引号  *星号  _下划线  {}花括号  []方括号  ()括弧  #井字号  +加号  -减号  .英文句 !感叹号
```

## 补充
Markdown也支持传统的HTML标签。
比如一个链接，你不太喜欢Markdown的写法，也可以直接写成
```html
<a href="http://www.baidu.com">百度</a>
```



# 转发请标明出处，谢谢！