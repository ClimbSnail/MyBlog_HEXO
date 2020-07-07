---
title: hexo+Github搭建个人静态博客
date: 2018-06-06 08:18:12
updated: 2020-06-07 06:35:22
tags: 静态博客搭建
toc: true
---
最后的效果可参考[本人博客](https://climbsnail.github.io)
![hexo静态博客](https://gitee.com/ClimbSnailQ/Project_Image/raw/master/Note/blog.jpg)
## 概要介绍
本文主要使用hexo搭建静态博客，并使用Github作为挂载点。

##### Hexo简介
Hexo是一款基于Node.js的静态博客框架，依赖少易于安装使用，可以方便的生成静态网页托管在GitHub和Coding上，是搭建博客的首选框架。大家可以进入hexo官网进行详细查看，因为Hexo的创建者是台湾人，对中文的支持很友好，可以选择中文进行查看。
##### Github简介
Github是一个面向开源及私有软件项目的托管平台,因为只支持 Git 作为唯一的版本库格式进行托管,故名 GitHub。

## 搭建步骤
1. 注册Github账号，并创建博客挂载点的仓库。
2. 安装Nodejs
3. 使用npm安装hexo
4. 正式开始使用hexo
5. 配置hexo
6. 测试

<!-- more -->

<br>
<br>
<br>
<br>

***

## 详细搭建过程
##### 安装Git工具
linux使用`sudo apt-get install git`安装git管理工具

windows访问[Git官网](https://git-scm.com/downloads)下载合适系统的git版本并安装。

##### 安装nodejs
linux使用`sudo apt-get install nodejs`安装nodejs

windows访问[Nodejs官网](http://nodejs.cn/)下载合适系统的版本并安装。

以上操作结束，可使用`node -v`来检查Nodejs是否安装成功。

##### npm安装、cnpm安装
linux使用`sudo apt-get install npm`安装npm

windows `cmd`中直接执行下面命令(确保上面已经安装过Nodejs)
```
npm install -g cnpm --registry.npm.taobao.org
# 安装无误后进行下面的hexo安装
cnpm install -g hexo-cli

hexo -v # 来验证下hexo是否安装成功
```

##### 初始化配置hexo
```
hexo init blog # 命令格式为hexo init [目录名]
```
添加了目录名这个选项，就会默认在当前页面创建目录并初始化。若不加用户名，则会在当前目录下初始化。
```
配置hexo的_config.yml文件

subtitle: 添加你的个签
keywords: 添加你网站的关键字
permalink 配置项指定了文章生成的结构，默认会以年月日的多层结构生成文件夹结构。
多层目录结构影响了怕从程序的搜索，故简易目录结构越短越好，建议permalink如下配置
permalink: :title/  # 只保留一层结构，即目录下直接单个文章名


```

##### 启动hexo服务程序测试
```shell
hexo s
或者
hexo server
```
会启动hexo本地服务，通过http://localhost:4000就能访问预览。
    浏览器访问上面的网址(打不开，可以更换浏览器再试试)

##### 创建一篇文章
```shell
hexo n "我的第一篇文章"
```
文章创建完默认存放在`source\_posts`目录下。可以使用vi或者其他的记事本工具编写文件（文章默认后缀.md）。

##### 编写完后发布
顺序执行以下命令
```shell
hexo clean # 清理
hexo g # 重新生成
```
再次使用`hexo s`启动运行hexo本地服务。到此为止已经成功搭建了基于本地的hexo个人博客。

<br>
<br>
<br>
<br>

***

### 部署到github仓库
确认本地服务搭建成功后，就来部署到github远端仓库，这样就可以公网访问我们的静态博客了。
##### 申请一个github账号
此步骤操作有疑问，请参考百度、谷歌。
##### 通过我们的github账号创建一个仓库
github的hexo仓库名一定要是 `github用户名.github.io`，否则之后会报错。
接下来的命令全都在hexo初始化的根目录进行。
##### 本地安装hexo的git部署插件
```shell
cnpm install --save hexo-deployer-git
或者使用以下命令
cnpm install hexo-deployer-git --save
```
##### 修改hexo配置
如下，需要配置`deploy`
```shell
deploy:
  type: 'git'
  repo: https://github.com/你的git用户名/你的git用户名.github.io.git
  branch: master
```
##### 部署到远端
```shell
hexo d
```
过程中会让输入github账号与密码两个步骤
##### 可以刷新github对应仓库的页面，可以看到内容已经到github上了。
实际上hexo只有网页相关的数据(`public`文件夹下的内容)会同步到github对应的仓库中。

通过访问[https://climbsnail.github.io](https://climbsnail.github.io)就可以访问我们的博客了。

#### Hexo搭建博客系列教程
1. Hexo搭建博客系列教程1__[hexo+Github搭建个人静态博客](../hexo+Github搭建个人静态博客)
2. Hexo搭建博客系列教程2__[Hexo安装配置yilia主题](../Hexo安装配置yilia主题)
3. Hexo搭建博客系列教程3__[yilia主题添加网易云音乐插件](../yilia主题添加网易云音乐插件)
4. Hexo搭建博客系列教程4__[yilia主题添加Gitment评论插件](../yilia主题添加Gitment评论插件题)
5. Hexo搭建博客系列教程5__[让搜索引擎收录博客](../让搜索引擎收录博客)
