---
title: Spring Aop
date: 2017-06-13 13:27:20
tags:Spring
---

>AOP 即 Aspect Oriental Program 面向切面编程 
首先，在面向切面编程的思想里面，把功能分为核心业务功能，和周边功能。 
所谓的核心业务，比如登陆，增加数据，删除数据都叫核心业务 
所谓的周边功能，比如性能统计，日志，事务管理等等 

>周边功能在Spring的变相切面编程AOP思想里，即被定义为切面 

>在面向切面编程AOP的思想里面，核心业务功能和切面功能分别独立进行开发 
然后把切面功能和核心业务功能 "编织" 在一起，这就叫AOP


**原理**

>切面编程核心就是拦截处理

两种实现方式：

- JDK Proxy代理

	>InvocationHandler 调用处理，使用JDK方式，必须实现接口，优势：使用反射创建对象，创建效率高

- cglib

	>asm 调用字节码class，基于子类的，基于继承的，没有接口的时候使用，优势：执行效率高
	
*面向接口编程，默认使用JDK方式*

<!--more-->

----------

**JDK Proxy实现**

1.创建接口

```
public interface UserService {

	void callName(String name);
}
```

2.实现接口

```
	public class UserServiceImpl implements UserService {

    @Override
	public void callName(String name) {
		System.out.println(name);
	    }
	}
```

3.实现UserInvocationHandler

```
	public class UserInvocationHandler implements InvocationHandler {

    private Object target;

    public UserInvocationHandler() {
    }

    public UserInvocationHandler(Object target) {
        this.target = target;
    }

    @Override
    public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
        System.out.println("调用前-->" + method.getName());
        Object obj = method.invoke(target, args);
        System.out.println("调用后-->" + method.getName());
        return obj;
    	}
	}
```

4.主函数里调用
	
```
	UserService userService = new UserServiceImpl();
    InvocationHandler handler = new UserInvocationHandler(userService);
    UserService userServiceProxy = (UserService) Proxy.newProxyInstance(userService.getClass().getClassLoader(),
                userService.getClass().getInterfaces(),handler);
    userServiceProxy.callName("Just for test");	
```

**cglib实现**

>要用到的包有asm、asm-commons、asm-util、cglib-nodep

1.创建CglibProxy代理类

```
	public class CglibProxy implements MethodInterceptor {
    
    @Override
    public Object intercept(Object o, Method method, Object[] args, MethodProxy methodProxy) throws Throwable {

        System.out.println("调用前-->"+method.getName());
        Object obj = methodProxy.invokeSuper(o,args);
        System.out.println("调用后-->"+method.getName());
        return obj;
    	}
	}
```
		
*要实现MethodIntercetor*

2.用Enhancer创建对象

```
	CglibProxy proxy = new CglibProxy();
	Enhancer enhancer = new Enhancer();
	enhancer.setSuperclass(UserServiceImpl.class);
	enhancer.setCallback(proxy);
	UserServiceImpl userService = (UserServiceImpl) enhancer.create();
```

3.实现对象方法的调用

```
	userService.callName("Just for test");
```

----------

**@Aspect**

**@Around**

**<aop:aspectj-autoproxy/>**