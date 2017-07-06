---
title: EL表达式
date: 2017-06-22 20:16:35
tags:
---

>E L（Expression Language） 目的：为了使 JSP 写起来更加简单。表达式语言的灵感来自于 ECMAScript 和 XPath 表达式语言，它提供了在 JSP 中简化表达式的方法，让Jsp的代码更加简化

果然是从前端借鉴过来的。。。

<!--more-->


----------

1. 最好在 <%@page%> 标签中加上 isELIgnored="false",以开启 Tomcat 对 EL 表达式的支持

2. 作用域优先级

	**pageContext>request>session>application**

3. 可以方便的访问 JavaBean 中的属性

	如：${user.name}

4. 结合JSTL的 <c:foEach> 使用，进一步简化代码

	```
	<c:forEach items="${heros}" var="hero" varStatus="st"  >
    <tr>
        <td>${st.count}</td>
        <td>${hero}</td>
    </tr>
	</c:forEach>
	```

5. 取参

	EL表达式还可以做到request.getParameter("name") 这样的形式获取浏览器传递过来的参数
	先把jstl.jsp代码改为如例所示，然后访问如下地址
	
	>http://127.0.0.1/jstl.jsp?name=abc
	
	<%@ page language="java" contentType="text/html; charset=UTF-8"
	    pageEncoding="UTF-8" import="java.util.*" isELIgnored="false"%>
	 
	${param.name}

6. 进行比较