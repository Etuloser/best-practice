---
title: Annotation
date: 2017-06-19 11:27:50
tags:
---

>Annotation (注释)，用来对程序进行补充说明，无论是否使用注释都不影响原程序的运行

>java.lang.annotation.Annotation 是 Annotation 的接口，只要是Annotat都必须实现此接口

```
public interface Annotation {
	
	public Class<? extends Annotataion> annotationType();
	public boolean equals(Object obj);
	String toString();
}
```

<!--more-->


**@Override**

>保证方法正确覆写

**Deprecated**

>声明一个不建议使用的方法

----------

####自定义Annotation

```
[public] @interface Annotation名称 {

	数据类型 变量名称()
}
```

**使用@interface就相当于继承了Annotation接口**