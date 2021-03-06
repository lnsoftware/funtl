# [#](https://funtl.com/zh/mybatis/第一个-MyBatis-对象关系映射.html#第一个-mybatis-对象关系映射)第一个 MyBatis 对象关系映射

## [#](https://funtl.com/zh/mybatis/第一个-MyBatis-对象关系映射.html#本节视频)本节视频

- [【视频】MyBatis 数据持久化-第一个 MyBatis 对象关系映射](https://www.bilibili.com/video/av24818481/)

## [#](https://funtl.com/zh/mybatis/第一个-MyBatis-对象关系映射.html#pom)POM

编写完相关代码后，我们可以使用单元测试查看 MyBatis 的执行效果，需要增加单元测试相关依赖，配置如下：

```xml
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-test</artifactId>
    <version>4.3.17.RELEASE</version>
</dependency>
<dependency>
    <groupId>junit</groupId>
    <artifactId>junit</artifactId>
    <version>4.12</version>
</dependency>
```

## [#](https://funtl.com/zh/mybatis/第一个-MyBatis-对象关系映射.html#导入-sql)导入 SQL

群共享中已经为大家准备好了练习用的 SQL，位置： `Java 微服务架构相关环境资料-SQL/myshop.zip`，有需要的同学可以加群获取

## [#](https://funtl.com/zh/mybatis/第一个-MyBatis-对象关系映射.html#定义实体类)定义实体类

以 `tb_user` 表为例，实体类代码如下：

```java
package com.funtl.my.shop.domain;

import java.io.Serializable;
import java.util.Date;

public class TbUser implements Serializable {
    private Long id;
    private String username;
    private String password;
    private String phone;
    private String email;
    private Date created;
    private Date update;

    public Long getId() {
        return id;
    }

    public void setId(Long id) {
        this.id = id;
    }

    public String getUsername() {
        return username;
    }

    public void setUsername(String username) {
        this.username = username;
    }

    public String getPassword() {
        return password;
    }

    public void setPassword(String password) {
        this.password = password;
    }

    public String getPhone() {
        return phone;
    }

    public void setPhone(String phone) {
        this.phone = phone;
    }

    public String getEmail() {
        return email;
    }

    public void setEmail(String email) {
        this.email = email;
    }

    public Date getCreated() {
        return created;
    }

    public void setCreated(Date created) {
        this.created = created;
    }

    public Date getUpdate() {
        return update;
    }

    public void setUpdate(Date update) {
        this.update = update;
    }
}
```

## [#](https://funtl.com/zh/mybatis/第一个-MyBatis-对象关系映射.html#定义数据访问接口)定义数据访问接口

注意：Spring 集成 MyBatis 后，不需要手动实现 DAO 层的接口，所有的 SQL 执行语句都写在对应的关系映射配置文件中。

```java
package com.funtl.my.shop.web.admin.dao;

import com.funtl.my.shop.domain.TbUser;
import org.springframework.stereotype.Repository;

import java.util.List;

@Repository
public interface TbUserDao {

    /**
     * 查询全部用户信息
     * @return
     */
    public List<TbUser> selectAll();
}
```

## [#](https://funtl.com/zh/mybatis/第一个-MyBatis-对象关系映射.html#定义业务逻辑接口)定义业务逻辑接口

```java
package com.funtl.my.shop.web.admin.service;

import com.funtl.my.shop.domain.TbUser;

import java.util.List;

public interface TbUserService {

    /**
     * 查询全部用户信息
     * @return
     */
    public List<TbUser> selectAll();
}
```

## [#](https://funtl.com/zh/mybatis/第一个-MyBatis-对象关系映射.html#实现业务逻辑接口)实现业务逻辑接口

```java
package com.funtl.my.shop.web.admin.service.impl;

import com.funtl.my.shop.domain.TbUser;
import com.funtl.my.shop.web.admin.dao.TbUserDao;
import com.funtl.my.shop.web.admin.service.TbUserService;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

import java.util.List;

@Service
public class TbUserServiceImpl implements TbUserService {

    @Autowired
    private TbUserDao tbUserDao;

    @Override
    public List<TbUser> selectAll() {
        return tbUserDao.selectAll();
    }
}
```

## [#](https://funtl.com/zh/mybatis/第一个-MyBatis-对象关系映射.html#定义映射文件)定义映射文件

映射文件，简称为 Mapper，主要完成 DAO 层中 SQL 语句的映射。映射文件名随意，一般放在 `src/resources/mapper` 文件夹中。这里映射文件名称定为 `TbUserMapper.xml`。

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN" "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="com.funtl.my.shop.web.admin.dao.TbUserDao">
    <select id="selectAll" resultType="TbUser">
        SELECT
          a.id,
          a.username,
          a.password,
          a.phone,
          a.email,
          a.created,
          a.updated
        FROM
          tb_user AS a
    </select>
</mapper>
```

## [#](https://funtl.com/zh/mybatis/第一个-MyBatis-对象关系映射.html#创建单元测试)创建单元测试

所有工作准备就绪，我们就可以测试 MyBatis 是否能够正常执行了。创建一个单元测试类，代码如下：

```java
package com.funtl.my.shop.web.admin.service.test;

import com.funtl.my.shop.domain.TbUser;
import com.funtl.my.shop.web.admin.dao.TbUserDao;
import org.junit.Test;
import org.junit.runner.RunWith;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.test.context.ContextConfiguration;
import org.springframework.test.context.junit4.SpringJUnit4ClassRunner;

import java.util.List;

@RunWith(SpringJUnit4ClassRunner.class)
@ContextConfiguration({"classpath:spring-context.xml", "classpath:spring-context-druid.xml", "classpath:spring-context-mybatis.xml"})
public class TbUserServiceTest {

    @Autowired
    private TbUserDao tbUserDao;

    @Test
    public void testSelectAll() {
        List<TbUser> tbUsers = tbUserDao.selectAll();
        for (TbUser tbUser : tbUsers) {
            System.out.println(tbUser.getUsername());
        }
    }
}
```

成功执行测试后，控制台输出如下：

```shell
2018-06-13 08:00:40,069 INFO [org.springframework.test.context.support.DefaultTestContextBootstrapper] - Loaded default TestExecutionListener class names from location [META-INF/spring.factories]: [org.springframework.test.context.web.ServletTestExecutionListener, org.springframework.test.context.support.DirtiesContextBeforeModesTestExecutionListener, org.springframework.test.context.support.DependencyInjectionTestExecutionListener, org.springframework.test.context.support.DirtiesContextTestExecutionListener, org.springframework.test.context.transaction.TransactionalTestExecutionListener, org.springframework.test.context.jdbc.SqlScriptsTestExecutionListener]
2018-06-13 08:00:40,106 INFO [org.springframework.test.context.support.DefaultTestContextBootstrapper] - Using TestExecutionListeners: [org.springframework.test.context.web.ServletTestExecutionListener@4b9e13df, org.springframework.test.context.support.DirtiesContextBeforeModesTestExecutionListener@2b98378d, org.springframework.test.context.support.DependencyInjectionTestExecutionListener@475530b9, org.springframework.test.context.support.DirtiesContextTestExecutionListener@1d057a39, org.springframework.test.context.transaction.TransactionalTestExecutionListener@26be92ad, org.springframework.test.context.jdbc.SqlScriptsTestExecutionListener@4c70fda8]2018-06-13 08:00:40,213 INFO [org.springframework.beans.factory.xml.XmlBeanDefinitionReader] - Loading XML bean definitions from class path resource [spring-context.xml]
2018-06-13 08:00:40,513 INFO [org.springframework.beans.factory.xml.XmlBeanDefinitionReader] - Loading XML bean definitions from class path resource [spring-context-druid.xml]
2018-06-13 08:00:40,565 INFO [org.springframework.beans.factory.xml.XmlBeanDefinitionReader] - Loading XML bean definitions from class path resource [spring-context-mybatis.xml]
2018-06-13 08:00:40,586 INFO [org.springframework.context.support.GenericApplicationContext] - Refreshing org.springframework.context.support.GenericApplicationContext@55d56113: startup date [Wed Jun 13 08:00:40 CST 2018]; root of context hierarchy
2018-06-13 08:00:41,650 INFO [com.alibaba.druid.pool.DruidDataSource] - {dataSource-1} inited
zhangsan
zhangsan1
zhangsan2
zhangsan3
zhangsan5
lisi
lisi1
jd_gogogo
tidy
tidy1
niuniu
niuniu2
niuniu3
niuniu4
test01
test02
2018-06-13 08:00:42,143 INFO [org.springframework.context.support.GenericApplicationContext] - Closing org.springframework.context.support.GenericApplicationContext@55d56113: startup date [Wed Jun 13 08:00:40 CST 2018]; root of context hierarchy
2018-06-13 08:00:42,149 INFO [com.alibaba.druid.pool.DruidDataSource] - {dataSource-1} closed
```

上次更新: 2018-12-29 1:45:15