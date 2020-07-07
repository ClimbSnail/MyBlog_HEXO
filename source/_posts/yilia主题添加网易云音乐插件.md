---
title: yilia主题添加网易云音乐插件
date: 2018-06-06 14:35:43
updated: 2019-06-07 08:13:22
tags: 静态博客搭建
---

##### 添加网易云音乐播放插件
1. 打开网易云音乐首页，复制选择的背景音乐分享外链

在[网易云音乐](https://music.163.com/) 网页中选中想要使用的音乐，进入播放界面，点击`生成外链播放器`，这里由于版权问题，网易云音乐无法对有版权的音乐生成外链！！！
![生成外链播放器](https://gitee.com/ClimbSnailQ/Project_Image/raw/master/Note/wangyiyunyinyue.jpg)
2. 引入播放器代码

在themes/yilia/layout/_partial/left-col.ejs文件nav标签中添加如下代码，代码中id后的`1334445174`为默认音乐的id号

将代码中的红色部分和刚刚复制的网易云外链代码进行对照，将对应部分进行替换（不替换的话使用的是 纸短情长 歌曲）

```html
<!-- 网易云音乐插件 -->
<% if (theme.music && theme.music.enable){ %>
   <div style="position:absolute; bottom:120px left:auto; width:85%">
      <iframe frameborder="no" border="0" marginwidth="0" marginheight="0" width="240" height="52" src="//music.163.com/outchain/player?type=2&id=<%=theme.music.id||1433584979%>&auto=<%=theme.music.autoplay?1:0%>&height=32"></iframe>
   </div>
<% } %>
```
<!-- more -->

添加位置如图：
![音乐插件添加](https://gitee.com/ClimbSnailQ/Project_Image/raw/master/Note/left_col.jpg "音乐插件添加的位置")
3. 回到hexo的配置文件`_config.yml`新增以下配置，更换音乐只需要改动`_config.yml`文件此处的id号。

![](https://gitee.com/ClimbSnailQ/Project_Image/raw/master/Note/wangyiyunchajian.jpg)
```html
music:
  enable: true
  id: 1433584979  # 网易云分享的ID,ID可以随时替换
  autoplay: true  # 是否开启自动播放
（注：在KeXueShangWang条件下，无法自动播放）
```


#### Hexo搭建博客系列教程
1. Hexo搭建博客系列教程1__[hexo+Github搭建个人静态博客](../hexo+Github搭建个人静态博客)
2. Hexo搭建博客系列教程2__[Hexo安装配置yilia主题](../Hexo安装配置yilia主题)
3. Hexo搭建博客系列教程3__[yilia主题添加网易云音乐插件](../yilia主题添加网易云音乐插件)
4. Hexo搭建博客系列教程4__[yilia主题添加Gitment评论插件](../yilia主题添加Gitment评论插件题)
5. Hexo搭建博客系列教程5__[让搜索引擎收录博客](../让搜索引擎收录博客)
