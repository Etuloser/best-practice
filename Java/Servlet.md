---
title: Servlet
date: 2017-06-22 19:21:55
tags: Servlet
---
####HttpServlet类

>如果要开发一个可以处理HTTP请求的Servlet程序，则肯定要继承HttpServlet类，而且在自定义的Servlet类中至少还要覆写HttpServlet类中提供的doGet()方法

```
protected void doGet(HttpServletRequest req,HttpServletResponse
	resp)throws ServletException,IOException
//负责处理所有的get请求，2个参数分别用来接收和回应用户的请求
```

**web.xml的配置：**

<!--more-->

需要配置的有：

```	
<servlet>
	<servlet-name></servlet-name>
    <servlet-class>包.类</servlet-class>
    </servlet>
<servlet-mapping>
	<servlet-name></servlet-name>
    <url-pattern>页面映射</url-pattern>
</servlet-mapping>
	//这些写在web-app标签里，可以配置多个servlet-mapping
```

**路径加载执行的是get请求**

**页面资源要放到web文件夹下**

----------

####Servlet生命周期

```
public void init() throws ServletException

public void init(ServletConfig config) throws ServletException

public abstract void service(ServletRequest req,ServletResponse res) throws ServletExcption,IOException
	
public void destroy()
```

**1.加载Servlet**

>Web容器负责加载Servlet，当Web容器启动是或者是在第一次使用这个Servlet时，容器会负责创建Servlet实例，但是用户必须通过部署描述符（web.xml）指定Servlet的位置（Servlet所在的包.类名称），成功加载后，Web容器会通过反射的方式对Servlet进行实例化

**2.初始化**

>当一个Servlet被实例化以后，容器将调用init()方法初始化这个对象，初始化的目的是为了让Servlet对象在处理客户端请求前完成一些初始化的工作，如建立数据库连接、读取资源信息等，如果初始化失败，则此Servlet将直接被卸载

**3.处理服务**

>当有请求提交时，Servlet将调用service()方法（常用的是doGet()或doPost()）进行处理。在service()方法中，Servlet可以通过ServletRequest接收客户的请求，也可以利用ServletResponse设置响应信息

**4.销毁**

>当Web容器关闭或者检测到一个Servlet要从容器中被删除时，会自动调用destroy()方法，以便让该实例释放掉所占用的资源

**5.卸载**

>当一个Servlet调用玩destroy()方法后，此实例将等待被垃圾收集器所回收，如果需要再次使用此Servlet时，会重新调用init()方法初始化

----------

####取得其他内置对象

	public HttpSession getSession()

	public HttpSession getSession(boolean create)
	//返回当前的session,如果没有则创建一个新的session对象返回

**ServletContext对象**

	public ServletContext getServletContext()
	

----------

####Servlet跳转

**服务器跳转：**

```
public void forward(ServletRequest request,ServletResponse response)throws ServletExcption,IOEXception

public void include(ServletRequest request,ServletResponse response)throws ServletExcption,IOEXception
```

----------


