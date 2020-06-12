---
title: yilia主题添加Gitment评论插件
date: 2019-06-06 16:53:23
updated: 2019-06-07 06:22:48
tags: 静态博客搭建
---

##### Gitment评论插件的使用
1. Gitment模块
> * Gitment 是基于 GitHub Issues 的评论系统。
> * 支持在前端直接引入，不需要任何后端代码。
> * 可以在页面进行登录、查看、评论、点赞等操作.
> * 同时有完整的 Markdown / GFM 和代码高亮支持。
> * 尤为适合各种基于 GitHub Pages 的静态博客或项目页面。
> * 想了解具体效果，可以点击查看官方Demo Page：Gitment Demo。

<!-- more -->

2. 注册 OAuth Application

> 首先在点击[注册](https://github.com/settings/applications/new)自己OAuth Application<br>

> 填写相关信息，注意：在Authorization callback URL填自己的网站url，例如我的https://climbsnail.github.io<br>

![](https://gitee.com/ClimbSnailQ/Project_Image/raw/master/Note/gitment.jpg)

> 创建成功后，你会得到一个`client ID`和一个`client secret`，这个将被用于之后的用户登录。<br>

3. 修改yilia的配置文件`_config.yml`
```
#5、Gitment
gitment_owner: ClimbSnail      #你的 GitHub ID
gitment_repo: 'Gitment'          #存储评论的 repo
gitment_oauth:
  client_id: ''           #client ID
  client_secret: ''  #client secret
  
# 其中的client ID 和 client secret换成你自己的就行了。
```

#### Hexo搭建博客系列教程
1. Hexo搭建博客系列教程1__[hexo+Github搭建个人静态博客](../hexo+Github搭建个人静态博客)
2. Hexo搭建博客系列教程2__[Hexo安装配置yilia主题](../Hexo安装配置yilia主题)
3. Hexo搭建博客系列教程3__[yilia主题添加网易云音乐插件](../yilia主题添加网易云音乐插件)
4. Hexo搭建博客系列教程4__[yilia主题添加Gitment评论插件](../yilia主题添加Gitment评论插件题)
5. Hexo搭建博客系列教程5__[让搜索引擎收录博客](../让搜索引擎收录博客)
