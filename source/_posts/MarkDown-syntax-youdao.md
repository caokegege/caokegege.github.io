title: MarkDown syntax 有道云笔记
tags:
  - markdown
categories:
  - markdown
date: 2018-04-20 22:05:34
---
利用GitHub把个人博客搭建完成了，就想着以后要多写点博客，才对的起GitHub提供的便利。写博客用到的都是markdown语法，因为以前一直用有道云笔记来记录东西。所以熟悉有道云的语法，虽说和主流的markdown语法有很大的出入，但是基本的操作都是有了。有道的流程图功能很强大，但是放到这里不太好用了，真是个很大的遗憾。

# 一个#是一级标题

## 两个##是二级标题

### 三个###是三级标题

#### 四个####是四级标题

##### 五个#####是乌鸡标题

###### 六个######是六级标题


表格
```
title1 | header 2 | title3
---|---|---
row 1 col 1 | row 1 col 2 | row 1 col 3
row 2 col 1 | row 2 col 2 | row 2 col 3
```

title1 | header 2 | title3
---|---|---
row 1 col 1 | row 1 col 2 | row 1 col 3
row 2 col 1 | row 2 col 2 | row 2 col 3

<!--more-->

代码用 \`\`\`  code  \`\`\`包围
```
public static void main(){
    sout("这是插入代码")
}
```
图片
```
![image](url)
```
![image](http://note.youdao.com/favicon.ico)

链接
```
[点这里可以跳转](url)
```

[点这里可以跳转](http://note.youdao.com/)


**这个是加黑字体**
```
**这个是加黑字体**
```

*这个是斜体*
```
*这个是斜体*
```

~~这个是横线~~
```
~~这个是横线~~
```

==这个是加背景颜色的字体==
```
==这个是加背景颜色的字体==
```

分割线
```
---是分割线
```
---

没有排序的列表
```
- a
  - a.a
  - a.b
    - a.b.a
    - a.b.b
        - a.b.b.a
- b
- - b.a
- - b.b
- - - b.b.a
- c
```
- a
  - a.a
  - a.b
    - a.b.a
    - a.b.b
        - a.b.b.a
- b
- - b.a
- - b.b
- - - b.b.a
- c

有序列表
```
1. 第一个层级
    1. 这是1.1
    2. 这是1.2
        1. 这是1.2.1
        2. 这是1.2.2
2. 第二个层级
```
1. 第一个层级
    1. 这是1.1
    2. 这是1.2
        1. 这是1.2.1
        2. 这是1.2.2
    3. 这是第三个
2. 第二个层级

待办事项
```
- [ ] 没有完成的作业
- [x] 已经完成的工作
```
- [ ] 没有完成的作业
- [x] 已经完成的工作

html代码可以执行出来
```
<html>
<!--在这里插入内容-->
在这里可以写入html的内容<br/>
<hr/>
<a href='http://github.com'>点击可以跳转到github</a><br/>
以上都是html的内容
</html>
```
<html>
<!--在这里插入内容-->
在这里可以写入html的内容
<hr/>
<a href='http://github.com'>点击可以跳转到github</a><br/>
以上都是html的内容
</html>

下面是数学公式和时许图，有道云笔记的功能，好像拿出来不好用了

```math
E = mc^2
```

```
graph LR
A-->B
```

```
sequenceDiagram
A->>B: How are you?
B->>A: Great!
```

```
gantt
dateFormat YYYY-MM-DD
section S1
T1: 2014-01-01, 9d
section S2
T2: 2014-01-11, 9d
section S3
T3: 2014-01-02, 9d
```