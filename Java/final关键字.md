---
title: final关键字
date: 2017-06-19 11:21:03
tags:
---

>最终，被final修饰的类叫最终类，如String类。

- 使用final修饰的类不能派生子类
- 使用final修饰的方法不能被子类所覆写
- 使用final修饰的变量即成为常量，常量不能修改

**String类用final修饰有多方面原因，主要是不想让String被修改，涉及到hash值、常量池引用同一个字面量**
