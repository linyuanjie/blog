---
title: 谷歌浏览器 跨域设置
date: 2019-09-18 08:43:33
tags:
    - IT技术
    - 前端
comments: true
---
## 一.版本号49之前的跨域设置：
1：找到桌面的谷歌浏览器快捷方式（一定是快捷方式，没有的话就找到安装目录发到桌面一个）右键属性
<!-- more -->
   ![](chrome.webp)

{% blockquote （注意：--前面是有空格的！不加空格会报错！！） %}
在 目标一栏里  加入  --disable-web-security.
{% endblockquote %}
再次打开浏览器，出现提示“你使用的是不受支持的命令标记 --disable-web-security”，那么说明配置成功。

## 二.版本号49之后的chrome跨域设置

{% blockquote %}
1.在电脑上新建一个目录，例如：C:\MyChromeDevUserData

2.在属性页面中的目标输入框里加上 --disable-web-security --user-data-dir=C:\MyChromeDevUserData
（ --user-data-dir的值就是刚才新建的目录，<b>前面还是要加空格)</b>

3.再次打开chrome，发现有“--disable-web-security”相关的提示，说明成功。
{% endblockquote %}

## 三.下载chrome跨域插件

1.从chrome应用商店下载跨域插件Allow-Control-Allow-Origin .crx文件
2.将文件后缀名修改为.rar 压缩文件类型
3.解压压缩文件
4.打开chrome浏览器-设置-更多工具-扩展程序-将解压的文件拖进扩展程序
5.chrome浏览器右上角会出现一个cors小图标 每次登录跨域站点的时候点击开启成绿色说明跨域插件已启用

设置成功如下所示：
![](chrome.png)


