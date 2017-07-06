---
title: SpringMVC
date: 2017-06-22 19:04:43
tags:
---

开始学习 SpringMVC 的时候从网上找了个例子，在部署到 Tomcat 上时候遇到了一个问题，我用的是 IDEA

>在 IDEA 中导入项目后，需要手动添加 Tomcat 服务器，并且添加 artifacts，这个具体是什么我暂时不知道，留着以后探究，猜测应该是服务器 lib 依赖，这里只说如何做

![](http://i.imgur.com/rZMPbis.png)

<!--more-->

----------

**1.在建立好项目，添加好 jar 包依赖后，开始配置 web.xml**

配置 SpringMVC 的入口 DispatcherServlet

```
<servlet>
	<servlet-name>springmvc</servlet-name>
	<servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
	<load-on-startup>1</load-on-startup>
</servlet>
<servlet-mapping>
	<servlet-name>springmvc</servlet-name>
	<url-pattern>/</url-pattern>
</servlet-mapping>
```

**2.配置 Spring-servlet.xml, 这是 Spring MVC 的映射配置文件**

表示访问 /index 路径会交由 id=indexController 的bean处理

```
<bean id="simpleUrlHandlerMapping" class="org.springframework.web.servlet.handler.SimpleUrlHandlerMapping">
	<property name="mappings">
		<props>
			<prop key="/index">indexController</prop>
		/props>
	</property>
</bean>

<bean id="indexController" class="controller.IndexController"></bean>
```

**3.然后声明控制类 IndexController**

控制类 IndexController实现接口 Controller，提供方法 handleRequest 处理请求

SpringMVC 通过 ModelAndView 对象把模型和视图结合在一起

```
public class IndexController implements Controller {
    @Override
    public ModelAndView handleRequest(HttpServletRequest httpServletRequest, HttpServletResponse httpServletResponse) throws Exception {
        ModelAndView modelAndView = new ModelAndView("index.jsp");
        modelAndView.addObject("message","Hello Spring MVC");
        return  modelAndView;
    }
}
```

----------

![](http://i.imgur.com/On11dyk.png)

----------

**视图定位**

1. 通过修改 sprinmvc-servlet.xml 来实现视图定位

	```
	<bean id="viewResolver" class="org.springframework.web.servlet.view.InternalResourceViewResolver">
	   <property name="prefix" value="/WEB-INF/page/" />
	   <property name="suffix" value=".jsp" />
	</bean>
	```

2. 修改 IndexController 类

	`ModelAndView mav = new ModelAndView("index");`


为什么要这样做？

如果写死路径不利于维护修改

----------

**注解方式**

同样 springmvc 也可以用注解来实现

1. 声明 IndexController 是控制类,同时不再让IndexController实现Controller类

	```
	@Controller
	public class IndexController{...}
	```

2. 声明 handleRequest 方法是 RequestMapping 同时加上参数,表示路径/index会映射到该方法上

	```
	@RequestMapping("/index")
	public ModelAndView handleRequest(HttpServletRequest request, HttpServletResponse response){...}
	```
3. 在配置文件里添加头文件标签约束并开启包扫描

	*头文件参考spring笔记*

	<context:annotation-config></context:annotation-config>

    <context:component-scan base-package="controller"/>

----------

**接受表单数据**

>浏览器提交数据是非常常见的场景，本例演示用户提交产品名称和价格到Spring MVC Spring MVC如何接受数据

1. 个人喜欢从页面做起，先写一个提交数据的页面 addProduct.jsp

 	```
	<form action="/addProduct">
        产品名称：<input type="text" name="name" value=""><br/>
        产品价格：<input type="text" name="price" value=""><br/>
        <input type="submit" value="增加商品">
    </form>
	```
	
	该jsp页面会把数据传到 /addProduct 下

2. 声明 ProductController 控制器来处理 JSP 传过来的数据

	```
	@Controller
	public class ProductController {
	
	    @RequestMapping("/addProduct")
	    public ModelAndView add(Product product)throws Exception{
	        ModelAndView modelAndView = new ModelAndView("showProduct");
	        return modelAndView;
	    }
	}
	```
	
	add 方法接受了 jsp 传过来的参数并把它们注入到了 product 对象里，并通过此对象生成了 showProduct 页面，相当于

	modelAndView.addObject("product",product);

3. 写 showProduct.jsp 页面来显示结果，用EL表达式

	产品名称： ${product.name}<br>
	产品价格： ${product.price}

----------

**客户端跳转**
	
	```
    @RequestMapping("/jump")
    public ModelAndView jump() {

        ModelAndView modelAndView = new ModelAndView("redirect:/index");
        return modelAndView;
    }
	```

显然，通过 **redirect:** 即可完成客户端跳转

----------

**刷session**
	
	```
	@RequestMapping("check")
    public ModelAndView check(HttpSession session) {
        Integer i = (Integer) session.getAttribute("count");
        if (i == null) {
            i = 0;
        }
        i++;
        session.setAttribute("count", i);
        ModelAndView modelAndView = new ModelAndView("check");
        return modelAndView;
    }
	```

----------

**filter**

	```
	<filter>
        <filter-name>CharacterEncodingFilter</filter-name>
        <filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>
        <init-param>
            <param-name>encoding</param-name>
            <param-value>utf-8</param-value>
        </init-param>
    </filter>
    <filter-mapping>
        <filter-name>CharacterEncodingFilter</filter-name>
        <url-pattern>/*</url-pattern>
    </filter-mapping>
	```

----------

**上传文件**

```
@Controller
public class UploadController {

    @RequestMapping("/uploadImage")
    public ModelAndView upload(HttpServletRequest request, HttpServletResponse response, UploadedImageFile file) throws IOException {

        String name = RandomStringUtils.randomAlphanumeric(10);
        String newFileName = name + ".jpg";
        File newFile = new File(request.getServletContext().getRealPath("/image"),newFileName);
        newFile.getParentFile().mkdir();
        file.getImage().transferTo(newFile);

        ModelAndView modelAndView = new ModelAndView("showUploadedFile");
        modelAndView.addObject("imageName",newFileName);
        return modelAndView;
    }
}
```