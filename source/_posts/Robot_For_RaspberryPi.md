---
title: 基于树莓派的多感知双足机器人
date: 2019-10-06 16:53:23
updated: 2020-03-19 06:22:48
tags: 项目
---

_You can also read a translated version of this file [英文版 in English](https://github.com/ClimbSnail/Robot_For_RaspberryPi/blob/master/README_English.md) or [in Korean 한국어]()._

项目来自我的本科毕业设计

最早之前做过一版，由单片机离线控制的。可以先预览。

Github项目[链接](https://github.com/ClimbSnail/Robot_For_RaspberryPi)

B站[视频](https://b23.tv/BV1qs411L7Pn) https://b23.tv/BV1qs411L7Pn

树莓派拓展板[视频](https://b23.tv/BV1zt411u7LR) https://b23.tv/BV1zt411u7LR

<iframe
	src="//player.bilibili.com/player.html?aid=62017744&bvid=BV1zt411u7LR&cid=107821320&page=1"
	scrolling="no"
	width="800px"
	height="600px"
	border="0"
	frameborder="no"
	framespacing="0"
	allowfullscreen="true"> 
</iframe>


整个项目为一个软硬件结合的项目，提供整个电路工程文件以及相关功能的所有源代码。

开发语言`C`、`C++`、`Python`、`C#`。

#### 机器人设计思维结构图
![RobotFrameDiagram](https://github.com/ClimbSnail/Robot_For_RaspberryPi/blob/master/Image/RobotFrameDiagram_mini.png)

![RobotFrameDiagram](https://gitee.com/ClimbSnailQ/Project_Image/raw/master/Robot_For_RaspberryPi/RobotFrameDiagram_mini.png "RobotFrameDiagram_mini.png")
<!-- 
<div align="center">
<img src="https://gitee.com/ClimbSnailQ/Project_Image/raw/master/Robot_For_RaspberryPi/RobotFrameDiagram_mini.png"/>
</div>
-->       

<!-- more -->


## Pictures and  3D-model
[Pictures](https://drive.google.com/drive/folders/175Xf5eR7ISFx6bbiMSzkLT8xGgaTwL8Q) \
[3D-model](https://drive.google.com/drive/folders/1SjDRSZ7dCbtEyQgJi2F-tcV4agTJ8wo_)


#### PCB 3D预览图
![RPI_ExpansionBoard_PCB](https://github.com/ClimbSnail/Robot_For_RaspberryPi/blob/master/Image/RPI_ExpansionBoard_PCB.jpg)


#### 文件介绍
* RPI_ExpansionBoard_Code _（树莓派拓展板内置STM32程序 MDK5工程）_
* RaspberryPi拓展板(STM32C8T6版) _（树莓派拓展板AD电路工程文件）_

#### 代码结构
整个代码的设计遵从高内聚低耦合，每个子模块都可以单独使用，内部都有对应的demo。

* robot_main.py _（整个机器人的主控制模块，controller）_
* baidu_speak.py _（百度语音识别与合成）_
* face_recognition.py _（基于opencv的人脸检测与识别）_
* GPIO.py _（树莓派拓展板的IO驱动API）_
* read_action.py _（动作组文件的读取）_
* snowboydecoder.py _（语音唤醒支撑文件）_
* snowboydetect.py _（语音唤醒支撑文件）_
* turing_robot.py _（图灵机器人对话）_
* playsound.py _（windows下音乐播放器）_
* robotsocket.py _（与即将开发的windows客户端通信）_
* config.py _（处理配置文件）_
* default.cfg _（robot_main.py使用的默认配置文件）_
* Action _（动作组存放的文件夹）_
* BaiduSpeak _（baidu_speak.py默认缓存文件夹）_
* Data _（opencv人脸检测的模型文件夹）_
* 其余的为参考图片

#### 补充

所有功能都已实现，相关内容等整立完了，统一更新。

相关的windows客户端随后也将更新。
