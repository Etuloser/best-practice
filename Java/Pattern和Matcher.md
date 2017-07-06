---
title: Pattern和Matcher
date: 2017-06-13 13:58:42
tags: J2SE
---

**实例化过程**

>Pattern用于创建匹配模式，用complie实例

```
	Pattern p = Pattern.compile("正则表达式");

	p.pattern()//以字符串的形式返回正则表达式
```

>Matcher用于执行匹配，支持分组，多次匹配，用matcher方法实例

```
	Pattern p = Pattern.compile("正则表达式");

	Matcher m = p.matcher("要匹配的字符串");

	m.pattern()//返回的是Pattern对象，由谁创建
```

<!--more-->

----------

**1.Pattern.split(CharSequence input)**

```
	Pattern p = Pattern.compile("正则表达式");

	String s[] = p.split("要分割的字符串");

	for(String str : s){
		System.out.println(str);
	}

	//输出的结果是以匹配组分割的字符串数组
```

**2.Pattern.matcher(String regex, CharSequence input)**

```
	System.out.println(Pattern.matches("\\d+","5465"));

	//输出结果是true
```

**3.Matcher.matches()/ Matcher.lookingAt()/ Matcher.find()** 

```
	//都返回布尔值
```

----------

**1.输出捕获组**

```
	 String str = "asdasdasd{abc}asdasdas{ddd}aasdasdasd{ufo}asdasd";
     Pattern p = Pattern.compile("\\{\\w{3}\\}");
     Matcher m = p.matcher(str);
     while (m.find()){
     	System.out.println(m.group().replaceAll("\\W",""));
     }

```
----------

*CharSequence是可读可写的字符串*

*String是只读字符串*

*\b 匹配数字*

*\w 匹配字母*
	
