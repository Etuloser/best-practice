---
title: favicon
date: 2017-03-01 13:24:04
tags: HTML
---

在HTML中可以使用link标签来实现shortcut icon。

```
<link rel="shortcut icon" type="images/x-icon"href="http://www.baidu.com favicon.ico">  
```

把href换成自己网站的favicon即可。

<!--more-->
参考：http://zh.wikipedia.org/wiki/Favicon

这里的favicon必须是16*16或者32*32的，必须是8位色或者24位色的，格式必须是png或者ico或者gif。
16*16/32*32 且 8位或24位色 且 png/ico/gif。

另一种实现favicon的方法是把名为favicon.ico的图片放在WEB根目录下。这种方法不推荐，因为这种方法违反了互联网规范，这个图片的访问是没有被授权的。

参考：http://www.w3.org/2005/10/howto-favicon