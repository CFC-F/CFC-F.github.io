---
title: Hexo+markdown之引用图片方法汇集
date: 2020-03-11 15:20:10
tags: Hexo博客  markdown
categories: 解决思路
description: 【Hexo博客】整理引用图片的方法
---

## 1、概述

最近在hexo中准备写点文章，但是发现文章中图片一直不显示，查了很多资料，在这里整理了一下，分享给大家，希望能够帮助大家。

 首先，网页中图片无法显示可能存在的一些问题。

在Markdown语法中，插入图片格式为`![图片标题随便](图片路径/**.jpg)`，如果这里选的是电脑本地的图片，则路径就是自己电脑文件夹路径，网页中的图片当然链接不到自己电脑里面的图片了。通过插件的作用就是在将图片添加到博客源文件中，并且设置好路径。这样，图片上传到GitHub仓库内，网页就可以从Github仓库中链接到自己的图片了。

可能会出现的几个问题

(1)在SEO优化中，为了缩短博文的链接，会将链接的的日期字段去掉，然后在后面添加上.html，这样就会使得这个图片插件失效

(2)当添加的图片比较多或者比较大，会使得网站部署的比较慢，也会使得自己本地的博客源文件比较臃肿

(3)我的主页配置文件_config.yml 里面根本就么有post_asset_folder这个选项

引用图片的方法：

## 2、本地图片引用

需要先安装上传本地图片的插件，在Hexo项目的根目录下输入

    npm install https://github.com/CodeFalling/hexo-asset-image --save

（注：在找到的资料中，有的显示需要修改一下插件文件，可以先安装后试试，如果不能引用图片，在参考：[修改插件内容](https://blog.csdn.net/xjm850552586/article/details/84101345?depth_1-utm_source=distribute.pc_relevant.none-task&utm_source=distribute.pc_relevant.none-task)进行修改）

### 2.1、绝对路径本地引用

在source里建立一个文件夹（如images），将图片统一放到source/images文件夹中，通过markdown语法访问它们。

 
     ![](images/image.png) 

### 2.2、相对路径本地引用
图片可以放在文章所在的目录中，需要先在hexo目录下的配置文件_config.yml中`post_asset_folder: flase`修改为`post_asset_folder: true`

将配置项post_asset_folder设为true后，执行命令$ hexo new article_name，在source/_posts中会生成文章article_name.md和同名文件夹article_name。将图片资源放在article_name文件夹中，文章就可以使用相对路径引用图片资源了。

    ![图片标题](image.png)

### 2.3、标签插件语法引用
图片在文章和首页中同时显示，可以使用标签插件语法。

    {% asset_img image.png 说明 %}

## 3、插入网络图片

现在已经有很多免费/收费图床和方便传图的小工具可选，只需要在基础语法的括号中填入图片的网络链接即可。


插入语法例如：

    ![图片标签](网络图片地址)   

### 3.1、 图床外链

图床网站可以用阿里云OSS、贴图库、七牛云

得到该图片在该网站上的链接地址，写博客的时候，图片的链接就填改地址

### 3.2、有道云笔记

2.2.1、将图片保存在有道云笔记中
步骤：新建一个笔记，上传（或复制）图片到有道云笔记中
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200311210236224.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzNDAxNTUy,size_16,color_FFFFFF,t_70)

2.2.2、分享图片，会得到1个文件的分享URL，复制这个URL，在浏览器中打开，会看到图片
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200311210502649.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzNDAxNTUy,size_16,color_FFFFFF,t_70)
右键点击图片，选择【复制图片地址】
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200311210519249.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzNDAxNTUy,size_16,color_FFFFFF,t_70)

将图片地址放到

    ![图片标签](图片网络地址)

2.2.3、还可以打开网页版有道云笔记，直接点击图片进行放大，右击图片，选择【复制图片地址】
（注：还未尝试，不知是否可行）
### 3.3、其他网络图片引用方法
采用CSDN、微博等作为图床，进行图片引用
`![图片说明（可填可不填）](图片的网络地址)`
## 4、把图片存入markdown文件

### 4.1、基础用法

    ![avatar](data:image/png;base64,iVBORw0......)

这是会发现插入的这一长串字符串会把整个文章分割开，非常影响编写文章时的体验。如果能够把大段的base64字符串放在文章末尾，然后在文章中通过一个id来调用，文章就不会被分割的这么乱了。

### 4.2、高级用法
比如：
```
![avatar][base64str]
[base64str]:data:image/png;base64,iVBORw0......
```
base64的图片编码得来的方法：

①用base64转码工具把图片转成一段字符串，然后把字符串填到基础格式中链接的那个位置。

②使用python将图片转化为base64字符串

```
import base64
f=open('723.png','rb') #二进制方式打开
ls_f=base64.b64encode(f.read()) #读取文件内容，转换为base64编码
f.close()
print(ls_f)
```

base64字符串转化为图片
```
import base64
bs='iVBORw0KGgoAAAANSUhEUg....' # 太长了省略
imgdata=base64.b64decode(bs)
file=open('2.jpg','wb')
file.write(imgdata)
file.close()
```
以上是我整理的网上搜索到的一些关于在hexo下用markdown语法引用图片的方法

在上面几种方法可能不是每一种方法都能帮你解决问题（有一些可能会在本地查看显示不正常,但是部署到github上就显示正常了），但总会有一种方法会帮助到你的。
（我自己采用的是第三种方法，引用（插入）网络图片）

参考链接：

1、<https://www.jianshu.com/p/b1b551b7d80d>

2、<https://www.jianshu.com/p/c4729f037547>

3、<https://www.jianshu.com/p/280c6a6f2594>

4、<https://www.jianshu.com/p/3db6a61d3782>

5、<https://blog.csdn.net/u010828718/article/details/55505631>

6、<https://blog.csdn.net/luzezhuo9992/article/details/86530262>

7、<https://fuhailin.github.io/Hexo-images>










