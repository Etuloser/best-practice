---

title: Maven
date: 2017-06-13 13:56:31
tags: Maven

---

**安装及配置**

<!--more-->

1. [https://maven.apache.org](https://maven.apache.org "maven")

2. 配置环境变量 `M2_HOME` 并添加到 path (E:\develop\maven)

3. 配置 settings.xml (E:\develop\maven\conf)
	

	```
	<!--本地仓库位置-->
	<localRepository>
  		F:/documents/mavenRepository
    </localRepository>
	<!--国内镜像-->
	<mirror>
      <id>nexus-aliyun</id>
      <mirrorOf>*</mirrorOf>
      <name>Nexus aliyun</name>
      <url>http://maven.aliyun.com/nexus/content/groups/public</url>
  	</mirror>
	```

4. 在 IDEA 设置 maven 相关配置

	![](http://i.imgur.com/tIqQqQ9.png)

5. 解决 archetype 加载慢的问题

	- [https://maven.apache.org/archetype/archetype-models/archetype-catalog/archetype-catalog.html](https://maven.apache.org/archetype/archetype-models/archetype-catalog/archetype-catalog.html)
	- 从以上网址找到 archetype-catalog.xml
	- 放到 F:\Documents\mavenRepository\org\apache\maven\archetype\archetype-catalog\3.0.1
	- 如下图在 IDEA 设置从本地加载 archetype-catalog.xml（-DarchetypeCatalog=local）
	![](http://i.imgur.com/u1uepvB.png)

	

----------

**Tomcat设置**：

1.添加Tomcat后到Deployment选择卡下把包放到lib下

2.在Server选择卡管理自动调起浏览器，改变Update方式

----------

**将指定目录下的xml文件也编译进输出文件夹target/class下**

需要在pom.xml设置如下
	
	```
    <build>
        <resources>
            <resource>
                <directory>src/main/java</directory>
                <includes>
                    <include>**/*.xml</include>
                </includes>
            </resource>
        </resources>
    </build>
	```