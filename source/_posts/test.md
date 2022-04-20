---
title: Test 测试一些 markdown 功能
date: 2021-09-01 23:21:29
tags: 
- markdown

mathjax: true
---

测试一些常用的 markdown 功能，包括代码块、表格、图片、公式（大概能基本涵盖写文章的需要？gif、视频 之类的后面再看看）。参考了 [markdown 教程](https://www.runoob.com/markdown/md-tutorial.html)

### 基础文本

第一段：关于 transformer 的一些知识。

第二段：关于 BERT 的一些知识。

### 代码块

测试一些 python 代码高亮。

``` python
for i in range(10):
    print(i)

a = "122 341 35"
a.split()

def foo(ls)：
    ls.append(1)
```

### 表格

| 左对齐 | 右对齐 | 居中对齐 |
| :-----| ----: | :----: |
| 单元格 | 单元格 | 单元格 |
| 单元格 | 单元格 | 单元格 |

### 图片

![猫猫](/images/cat.jpg "一只猫猫")

### 公式

行内公式 \\(a + b = c\\)

英文小括号和行内公式产生冲突，修改了 `post.ejs` 中如下部分：

```html
<% if (theme.mathjax.enable && page.mathjax) { %>
<script src="<%- theme.mathjax.cdn %>"></script>
<script>
    MathJax.Hub.Config({
        tex2jax: {inlineMath: [['$', '$'], ['\(', '\)']]}
    });
</script>
<% } %>
```

用 `\\(` 和 `\\)` 替换 `\(` 和 `\)`。

单独处理的公式：

$$
tanh = \frac{e^x-e^{-x}}{e^x+e^{-x}}
$$
