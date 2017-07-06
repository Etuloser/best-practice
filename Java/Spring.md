---

title: Spring-IOC、DI
date: 2017-06-19 12:53:25
tags: Spring

---

>Spring 的核心就是 IOC、DI 和 AOP

>IOC (Inversion Of Controller) 反转控制，简单来说就是由 new 关键字创建对象变成交由Spring 容器来创建

>DI (Dependency Inject) 依赖注入，简单来说就是拿到的对象，已经被注入好相关值了，直接使用即可

**由一个例子来演示 IOC 和 DI**

<!--more-->

首先创建一个 POJO

```
public class Category {

    private int id;
    private String name;

    public int getId() {
        return id;
    }

    public void setId(int id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }
}
```

由 Spring 创建对象,并注入了 name


```
<bean name="Category" class="com.etuloser.POJO.Category">

	<property name="name" value="category"/>
</bean>
```

测试

```
public class TestCategory {

    public static void main(String[] args) {
        ApplicationContext context = new ClassPathXmlApplicationContext("spring-cfg.xml");
        Category category = (Category) context.getBean("Category");
        System.out.println(category.getName());
    }
}
```

![](http://i.imgur.com/HyFThdi.png)



也可以把一个对象注入到另一个对象里

`<property name="category" ref="Category"/>`

注意要用 ref

----------

**以上是通过 XML 的方式来注入对象，我们也可以用注解的方式来完成注入对象的效果**

首先在 xml 文件头文件里添加标签约束

	```
	<?xml version="1.0" encoding="UTF-8"?>
	<beans xmlns="http://www.springframework.org/schema/beans"
	       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:aop="http://www.springframework.org/schema/aop"
	       xmlns:tx="http://www.springframework.org/schema/tx" xmlns:context="http://www.springframework.org/schema/context"
	       xsi:schemaLocation="
	   http://www.springframework.org/schema/beans
	   http://www.springframework.org/schema/beans/spring-beans-3.0.xsd
	   http://www.springframework.org/schema/aop
	   http://www.springframework.org/schema/aop/spring-aop-3.0.xsd
	   http://www.springframework.org/schema/tx
	   http://www.springframework.org/schema/tx/spring-tx-3.0.xsd
	   http://www.springframework.org/schema/context
	   http://www.springframework.org/schema/context/spring-context-3.0.xsd">
	```

然后告知 Spring 要用注解的方式进行配置

`<context:annotation-config/>`

再使用 @Autowired 或者 @Resource 注解让类或者方法自动装载

以上是对**注入对象行为**进行注解，那么 Bean 对象本身是否可以也通过注解而脱离xml配置文件进行呢？答案是可以的

**在 xml 文件中声明开启包扫描**

`<context:component-scan base-package="com.how2java.pojo"/>`

通过 **@Component** 注解声明此类是Bean

`@Component("Category")`

----------


**Other**

*xml 配置文件中 <bean> 标签的 id 属性和 name 属性基本上没有什么区别，但是使用 id 会更加符合规范，因为 xml 中 id 要求是唯一的*