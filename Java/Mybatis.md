---
title: Mybatis
date: 2017-06-24 20:25:50
tags: Mybatis
---

>为了摆脱繁琐和枯燥的重复操作，减少代码重复率，mybatis是一个很好的选择

<!--more-->

1. 创建实体类映射表

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

2. 配置mybatis-cfg.xml

	```
	<!--包扫描-->
	<typeAliases>
        <package name="pojo"/>
    </typeAliases>
    <environments default="development">
        <environment id="development">
            <transactionManager type="JDBC"/>
            <dataSource type="POOLED">
                <property name="driver" value="com.mysql.jdbc.Driver"/>
                <property name="url" value="jdbc:mysql://localhost:3306/how2java?characterEncoding=UTF-8"/>
                <property name="username" value="root"/>
                <property name="password" value="123456"/>
            </dataSource>
        </environment>
    </environments>
	<!--映射Category.xml-->
    <mappers>
        <mapper resource="pojo/Category.xml"/>
    </mappers>
	```

3. 配置文件Category.xml

	```
	<mapper namespace="pojo">
    <insert id="addCategory" parameterType="Category">
        INTO INTO category_ (name) VALUE (#{name})
    </insert>
    <delete id="delCategory" parameterType="Category">
        DELETE FROM category_ WHERE name = #{name}
    </delete>
    <select id="getCategory" parameterType="_int" resultType="Category">
        SELECT * FROM category_ WHERE id = #{id}
    </select>
    <update id="updateCategory" parameterType="Category">
        UPDATE category_ set name = #{name} WHERE id = #{id}
    </update>
    <select id="listCategory" resultType="Category">
        SELECT * FROM category_
    </select>
	</mapper>
	```