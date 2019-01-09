---
title: 博客系统搭建和Python学习
tags:
  - 博客
  - python
categories:
  - 笔记
mathjax: true
date: 2018-04-01 23:47:06
---

## 博客系统

今天用hexo在GitHub上搭了一个博客。遇到了无数的坑这个完了说。

晚上用Gitment做了评论系统，按照网上的教程做完发现一个巨大的坑是初始化评论的问题

解决方法如下：

> issue的标签label有长度限制！labels的最大长度限制是50个字符。
>
> `id: '页面 ID', // 可选。默认为 location.href`
>
> 这个id的作用，就是针对一个文章有唯一的标识来判断这篇本章。
>
> 在issues里面，可以发现是根据网页标题来新建issues的，然后每个issues有两个labels（标签），一个是gitment，另一个就是id。
>
> 所以明白了原理后，就是因为id太长，导致初始化失败，现在就是要让id保证在50个字符内。
>
> 对应配置的id为：
>
> ```
> id: '<%= page.title %>'
>
> ```
>
> 如果用网页标题也不能保证在50个字符！
>
> 最后，我用文章的时间，这样长度是保证在50个字符内，完美解决！（避免了文章每次更新标题或路径时，会重新创建一个issue评论的问题。）
>
> 在 themes\next\layout_third-party\comments 目录下修改gitments.swig，找到以下代码修改
>
> function renderGitment(){
> var gitment = new {{CommentsClass}}({
> - id: window.location.pathname,
> + id: '{{ page.date }}',
>   owner: '{{ theme.gitment.github_user }}',
>   repo: '{{ theme.gitment.github_repo }}',
>   {% if theme.gitment.mint %}
>   lang: "{{ theme.gitment.language }}" || navigator.language || navigator.systemLanguage || navigator.userLanguage,
>   {% endif %}
>
> 之后重新hexo g -d就ok了，请保证没有浏览器缓存。

就这样。

## python学习

这个完了再更新。今天看了一下列表和for循环。还没练习。明天再说吧。