title: 为Hexo博客添加目录
date: 2015-12-26 18:29:00
description: 
categories:
- 建站
tags:
- 博客
- 建站
- Hexo
toc: true
author:
comments:
original:
permalink: 
---

　　**自用笔记：**本文属于自用笔记，不做详解，仅供参考。
　　在此记录自己已理解并开始遵循的前端代码规范。What How Why
　　最近，使用Hexo遇到了很多问题，在设立进行整理。

<!-- more -->

# 为Hexo博客添加目录
## 文章目录
1. 修改Landscape主题的ejs文件
2. 为目录编写CSS文件
3. 收尾工作

Hexo博客系统的核心支持生成目录（Table of Contents），但其默认的主题Landscape并不支持目录的显示。我们只需对Landscape的主题文件稍作修改并添加一点目录的CSS就可以在文章前面显示友好的目录了。

## 修改Landscape主题的ejs文件

我们首先要编辑文章显示页面的模板，也就是themes/landscape/layout/_partial/article.ejs文件。为了将目录生成在正文之前，我们首先在这个文件中找到<%- post.content %>，并在这一行之前加入如下代码：
```
<!-- Table of Contents -->
<% if (!index && post.toc){ %>
  <div id="toc" class="toc-article">
    <strong class="toc-title">文章目录</strong>
    <%- toc(post.content) %>
  </div>
<% } %>
```
这段代码的含义清晰明了，if语句中有两个条件，!index是为了不在首页的文章摘要中生成目录，post.toc确保了只在显式地标记了toc: true的文章中生成目录。若这两个条件满足，则创建一个目录的<div>。

修改完这个文件之后，找一篇包含了多个子标题的文章，并在文章开头的front-matter中添加一句toc: true，在浏览器中访问这篇文章，应该可以看到文章的开头处已经有了带链接的目录。但是这样的目录实在太难看，我们还需要添加相应的CSS来将其指定为我们想要的样式。

## 为目录编写CSS文件

要指定目录的样式，我们要修改的文件是themes/landscape/source/css/_partial/article.styl。在文件的最后，添加如下代码：

```
/*toc*/
.toc-article
  background #eee
  border 1px solid #bbb
  border-radius 10px
  margin 1.5em 0 0.3em 1.5em
  padding 1.2em 1em 0 1em
  max-width 28%

.toc-title
  font-size 120%

#toc
  line-height 1em
  font-size 0.9em
  float right
  .toc
    padding 0
    margin 1em
    line-height 1.8em
    li
      list-style-type none

  .toc-child 
    margin-left 1em
```
第一段的toc-article指定了目录整个<div>的背景色、边框色、倒角半径、各种间距以及最大的宽度。注意这里最好指定目录的最大宽度，我将其设为了28%，也就是文章正文那个框的宽度的28%，也可以设为一个固定的长度，比如在笔记本电脑上16em就是个不错的宽度，但为了能适配各种不同尺寸的屏幕，最好还是设置为百分比。如果不指定最大宽度，遇到比较长的标题时，生成的目录会非常难看。这个最大宽度的设置是我在网上其他添加目录的方法中没有见到的。

第二段的toc-title指的就是“文章目录”那四个字，这四个字要比其他字大一些，将其字号设为其他字的120%。

第三段的#toc.toc指定了目录列表的一些细节，将font-size设为0.9em会让目录的字比文章的字稍小一些。最后的.toc-child指定了二级目录的缩进量。

再次生成页面，应该已经可以显示比较美观的目录了。

## 收尾工作

通常情况下我们不需要为每一篇文章都添加目录，因为大部分文章的长度还是相对较短，或者结构简单而没有添加小标题。在我的博客上，需要添加目录的长文还是相对较少的。因为我选择了默认不生成目录，而手动为需要目录的文章添加显式地标记。

下面我就需要编辑每一篇需要添加目录的文章，在文章开头的front-matter中加入toc: true。