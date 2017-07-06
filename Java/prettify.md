---
title: prettify
date: 2017-03-01 12:57:33
tags: Sublime
---
使用Sublime text 3 编写代码是一种享受，使用Sublime text 3 格式化HTML代码，需要安装插件，具体安装步骤如下：

1、打开菜单->首选项->插件控制，输入 install package

2、等待程序进入插件管理功能，再输入插件名称：TAG

3、点击安装插件html-css-js prettify 。

4、插件安装成功后，在需要格式化的HTML代码中，选中代码，然后按Ctrl+Alt+H对代码进行格式化。

html-css-js prettify 格式化CSS会再每个CSS后面都添加一个换行，取消该换行的方法：

打开：菜单>tools>html/css/js prettify>set prettify preferences
修改设置newline_between_rules的参数为false