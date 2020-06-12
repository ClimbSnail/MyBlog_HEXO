---
title: Hexo安装配置yilia主题
date: 2019-06-06 10:13:12
updated: 2019-06-07 06:35:22
tags: 静态博客搭建
---
最后的效果可参考[本人博客](https://climbsnail.github.io)
![hexo静态博客](https://gitee.com/ClimbSnailQ/Project_Image/raw/master/Note/blog.jpg)

## 高级玩法之更换hexo主题
##### 使用hexo-theme-yilia主题
1. 在命令行中确保在本博客的根目录下，输入以下命令。
```bash
git clone https://github.com/litten/hexo-theme-yilia.git themes/yilia
# 注：themes/yilia意为将本次下载下来的yilia主题放在themes目录下
```
2. 修改本博客根目录的`_config.yml`文件中的`theme`字段的参数，更改为`yilia`。
```bash
theme: yilia
```
3. 部分配置项介绍
```
favicon 为网页打开后的标签图标
avatar  为网页主页的个人图标
```

<!-- more -->

##### 文章截断功能
文章篇幅大的时候，主页将会被长篇占据，影响美观。

Yilia中可以使用\<!-- more -->在目标文中标记(一定是在文章中)，表示当该文章在主页显示的时候，只展现\<!-- more -->标记之前的内容。

可以注释`excerpt_link`这个配置项，如下：
```bash
# excerpt_link: more
```
##### 开启tag栏的文章搜索
修改yilia的`_config.yml`文件中的`showTags`配置项值为`true`。
```bash
# slider的设置
slider:
  # 是否默认展开tags板块
  showTags: true
```

##### Yilia主题的所有文章功能不能用
点击左侧"所有文章"无法正常使用，则请参考以下操作。
1. node.js版本必须6.2以上 
2. 在hexo根目录下执行命令：
```bash
npm i hexo-generator-json-content --save
```
3. 在hexo的配置文件_config.yml最后添加
```bash
jsonContent:
    meta: false
    pages: false
    posts:
      title: true
      date: true
      path: true
      text: false
      raw: false
      content: false
      slug: false
      updated: false
      comments: false
      link: false
      permalink: false
      excerpt: false
      categories: false
      tags: true
```

4. 删除页面右下角的"Hexo Theme Yilia by Litten"
```html
打开themes\yilia\layout_partial\footer.ejs,修改如下：

<div class="footer-right">
</div>
```

5. 添加后重新发布就行了。
```bash
hexo clean && hexo g && hexo d
```

#### Hexo搭建博客系列教程
1. Hexo搭建博客系列教程1__[hexo+Github搭建个人静态博客](../hexo+Github搭建个人静态博客)
2. Hexo搭建博客系列教程2__[Hexo安装配置yilia主题](../Hexo安装配置yilia主题)
3. Hexo搭建博客系列教程3__[yilia主题添加网易云音乐插件](../yilia主题添加网易云音乐插件)
4. Hexo搭建博客系列教程4__[yilia主题添加Gitment评论插件](../yilia主题添加Gitment评论插件题)
5. Hexo搭建博客系列教程5__[让搜索引擎收录博客](../让搜索引擎收录博客)
