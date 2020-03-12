---
title: Hexo博客更换主题时 使用 hexo g 所遇到的问题
date: 2020-03-03 13:06:36
tags: Github  Hexo博客
categories: 解决思路
description: 【Hexo博客】更换Hexo主题，使用hexo g命令时，出现Template render error:(unknown path)的解决思路
---
# 前言
【Hexo博客】更换Hexo主题，使用hexo g命令时，出现Template render error:(unknown path)
初次通过Github Pages + Hexo 来搭建博客，在进行主题设置时，出现了一点小问题。现已
解决问题，将方法留在此处，和大家一起分享。
报错信息如下：

![01](https://img-blog.csdnimg.cn/20200302231237562.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzNDAxNTUy,size_16,color_FFFFFF,t_70)

根据提示：可以参考网站https://hexo.io/docs/troubleshooting.html

问题出现的一般解决方案如下：
1、可能在主题的配置文件 _config.yml 中改动时出现有问题，原因是由于配置文件没有空
格隔开

![](https://img-blog.csdnimg.cn/20200302231336616.png)

查找方法：如上图，在配置文件中，有问题的相关配置项会变成白色
配置项正确格式

```
#正确格式
search:
  path: 参数
  field: 参数
#错误格式
search：
  path:参数
  field:参数
#正确格式是在“path:”配置项后面有一个空格，再加上参数
```
 给初次搭建博客的盆友们一点小建议，在修改博客或者主题的一些相关配置时（特别是在>修改博客主题配置文件时）保险起见，可以修改一部分配置信息后，使用命令
    ``hexo g``
    ``hexo s``
通过本地地址 http://localhost:4000 进行博客主题改动预览，进而查看主题改动的情况>。

