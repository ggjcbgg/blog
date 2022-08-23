---
title: Spring5
abbrlink: 58c6
date: 2022-08-14 15:04:17
tags: spring #文章标签
categories: [spring] #文章分类
keywords: #关键字
top_img: false #文章顶部图片
cover: https://webplus-cn-shenzhen-s-61b0219cf968dd14ce7355c5.oss-cn-shenzhen.aliyuncs.com/1.jpg #文章缩略图(如果没有设置top_img,文章页顶部将显示缩略图，可设为false/图片地址/留空)
comments: true #显示文章评论模块(默认 true)
footer_bg: true
sticky: 1 #文章置顶
swiper_index: 1 #置顶轮播图顺序，非负整数，数字越大越靠前
#background: /img/1.jpg
---

<div align='center'> <font size='50'>Spring5框架</font></div>


## 1.Spring概念 [（视频链接）](https://www.bilibili.com/video/BV1Vf4y127N5?p=4&spm_id_from=pageDriver)

1. spring是轻量级的开源的Java EE框架

2. Spring可以解决企业应用开发的复杂性

3. Spring有两个核心部分：IOC和Aop

   > **(1)**  IOC:控制反转，把创建对象过程交给Spring进行管理（<font color='red'>不需要new创建对象</font>）
   >
   > **（2）** Aop：面向切面，不修改源代码进行功能增强

4. Spring特点：

   * 方便解耦，简化开发

   * Aop编程的支持

   * 方便程序测试

   * 方便和其他框架进行整合

   * 方便进行事务操作

   * 降低API开发难度

     ***

     

   ### Spring5下载文件

   ![image-20210913093926874](C:\Users\江流\AppData\Roaming\Typora\typora-user-images\image-20210913093926874.png)

   Spring中每种有三个文件：

   * 第一个为架包
   * 第二个-javadoc为文档
   * 第三个-sources为源代码

   ***

   ![image-20210913094557402](C:\Users\江流\AppData\Roaming\Typora\typora-user-images\image-20210913094557402.png)



* Core Container：核心部分
* Beans、Core：对应IOC
* Context：上下文
* Expression：表达式



## 2.IOC容器

##### IOC(概念和原理）

> 1、什么是IOC

> > * 控制反转，把对象创建和对象之间的调用过程，交给Spring进行管理
> > * 使用IOC的目的：为了耦合度降低
>
> 2、IOC底层原理：
>
> >xml解析、工厂模式、反射
>
> 3、画图讲解IOC底层原理
>
> <font color='red' ><b>调用另一个类的方法:</b></font>
>
> ![image-20210913120109189](C:\Users\江流\AppData\Roaming\Typora\typora-user-images\image-20210913120109189.png)
>
> ![image-20210913120814177](C:\Users\江流\AppData\Roaming\Typora\typora-user-images\image-20210913120814177.png)
>
> ![image-20210913162824150](C:\Users\江流\AppData\Roaming\Typora\typora-user-images\image-20210913162824150.png)

##### IOC接口

1. IOC思想基于IOC容器完成，IOC容器底层就是对象工厂

2. Spring提供IOC容器实现两种方式：（两个接口）

   > (1) BeanFactory : IOC容器基本实现，是Spring内部的使用接口，不提供开发人员进行使用
   >
   > + 加载配置文件的时候不会创建对象，在获取对象（使用）的时候才去创建对象
   >
   > (2) ApplicationContext : BeanFactory接口的子接口，提供更多更强大的功能，一般由开发人员使用
   >
   > + 加载配置文件的时候就会把配置文件对象进行创建

3. ApplicationContext接口有实现类

   ![image-20210913165428836](C:\Users\江流\AppData\Roaming\Typora\typora-user-images\image-20210913165428836.png)

***

##### IOC操作Bean管理（概念）

1. 什么是Bean管理
   * Bean管理指的是两个操作
   * Spring创建对象
   * Spring注入属性
2. Bean管理操作有两种方式
   * 基于xml配置文件方式实现
   * 基于注解方式实现

##### IOC操作Bean管理（基于xml方式）

```java
<!--配置User对象创建-->
    <bean id="user" class="com.spring.test.User"></bean>
```

（1）在spring配置文件中，使用bean标签，标签里面添加对应属性，就可以实现对象创建

（2）在bean标签有很多属性，介绍常用的属性

> * id属性：唯一标识
> * class属性：类全路径（包类路径）

（3）创建对象的时候，默认也是执行无参数构造方法完成对象创建

2. 基于xml方式注入属性

   > （1）DI：依赖注入，就是注入属性
   >
   > <img src="C:\Users\江流\AppData\Roaming\Typora\typora-user-images\image-20210913215126794.png" alt="image-20210913215126794" style="zoom:60%;" />

3. 第一种注入方式：使用set方法进行注入

   （1）创建类，定义属性和对应的set方法

   ```java
   /*
   演示使用set方法进行注入属性
    */
   public class Book {
       //创建属性
       private String bname;
       private String bauthor;
       //创建属性对应的set方法
   
       public void setBname(String bname) {
           this.bname = bname;
       }
   
       public void setBauthor(String bauthor) {
           this.bauthor = bauthor;
       }
   ```

   (2) 在spring配置文件配置对象创建，配置属性注入

   ```java
   <!--2 set 方法注入属性-->
       <bean id="book" class="com.spring.test.Book">
       <!--使用property完成属性注入
       name:类里面属性名称
       value：向属性注入的值
       -->
       <property name="bname" value="xiaoai"></property>
       <property name="bauthor" value="xiao"></property>
   
       </bean>
   ```

4. 第二种注入方式：使用有参数构造进行注入

   (1) 创建类，定义属性，创建属性对应有参数构造方法

   ![image-20210913231927303](C:\Users\江流\AppData\Roaming\Typora\typora-user-images\image-20210913231927303.png)

   (2) 在spring配置文件中进行配置

   ```java
   <!--有参数构造属性-->
       <bean id="orders" class="com.spring.test.Orders">
           <constructor-arg name="oname" value="电脑"> </constructor-arg>
           <constructor-arg name="address" value="China"></constructor-arg>
       </bean>
       
   ```

   

5. ![image-20210915194052986](C:\Users\江流\AppData\Roaming\Typora\typora-user-images\image-20210915194052986.png)



***

##### IOC操作Bean管理（注入属性）

1. 字面量

   （1）null值

   ```java
   <!--null值-->
   <property name="address">
       <null/>
   </property>
   ```

   （2）属性值包含特殊符号

   ```java
   <!--属性值包含特殊符号
      1 把<>进行转义 &lt; &gt;
      2 把特殊符号内容写进CDATA 格式为：<![CDATA[内容]]>
   -->
   <property name="address">
       <value><![CDATA[<<南京>>]]></value>
   </property>
   ```

2. ##### 注入属性-外部bean

   > * 创建两个类service类和dao类
   > * 在service调用dao里的方法
   > * 在spring配置文件中进行配置
   >
   > ```java
   > public class UserService {
   > 
   >     //创建UserDao类型属性，生成set方法
   >     private UserDao userDao;
   >     public void setUserDao(UserDao userDao) {
   >         this.userDao = userDao;
   >     }
   > 
   >     public void add(){
   >         System.out.println("service add..........");
   >         userDao.update();
   >      }
   > }
   > ```
   >
   > ```java
   > <!--1 service和dao对象创建  接口不能new对象，只能找接口的实现类-->
   >     <bean id="userService" class="com.spring.test.service.UserService">
   >         <!--注入userDao对象
   >         name属性值：类里面属性名称
   >         ref属性：创建userDao对象bean标签的id值
   >         -->
   >         <property name="userDao" ref="userDao"></property>
   >     </bean>
   >     <bean id="userDao" class="com.spring.test.dao.UserDaoImpl"></bean>
   > ```
   >
   > 

3. 注入属性-内部bean

   （1）一对多关系：部门和员工

   一个部门有多个员工，一个员工属于一个部门

   部门是一，员工是多

   （2）在实体类之间表示一对多关系，员工表示所属的部门，使用对象类型属性进行表示

   ```java
   //部门类
   public class Dept {
       private String dname;
   
       public void setDname(String dname) {
           this.dname = dname;
       }
       
   }
   ```

   ```java
   //员工类
   public class Emp {
       private String ename;
       private String gender;
       //员工属于某一个部门，使用对象形式表示
       private Dept dept;
   
       public void setDept(Dept dept) {
           this.dept = dept;
       }
   
       public void setEname(String ename) {
           this.ename = ename;
       }
   
       public void setGender(String gender) {
           this.gender = gender;
       }
   }
   ```

   （3）在spring配置文件中进行配置

   ```java
   <!--内部bean-->
   <bean id="emp" class="com.spring.test.bean.Emp">
       <!--设置两个普通属性-->
       <property name="ename" value="lucy"></property>
       <property name="gender" value="女"></property>
       <!--设置对象类型属性-->
       <property name="dept">
           <bean id="dept" class="com.spring.test.bean.Dept">
               <property name="dname" value="安保部"></property>
           </bean>
       </property>
   </bean>
   ```

   

4. 注入属性-级联赋值

   （1）第一种写法

   ```java
   <!--级联赋值-->
   <bean id="emp" class="com.spring.test.bean.Emp">
       <!--设置两个普通属性-->
       <property name="ename" value="lucy"></property>
       <property name="gender" value="女"></property>
       <!--级联赋值-->
       <property name="dept" ref="dept"></property>
   </bean>
   
   <bean id="dept" class="com.spring.test.bean.Dept">
       <property name="dname" value="财务部"></property>
   </bean>
   ```

   第二种写法：

   前提：dept要有get方法

   ```java
   <!--级联赋值-->
   <bean id="emp" class="com.spring.test.bean.Emp">
       <!--设置两个普通属性-->
       <property name="ename" value="lucy"></property>
       <property name="gender" value="女"></property>
       <!--级联赋值-->
       <property name="dept" ref="dept"></property>
       <property name="dept.dname" value="技术部"></property>
   </bean>
   
   <bean id="dept" class="com.spring.test.bean.Dept">
       <property name="dname" value="财务部"></property>
   </bean>
   ```

   ***

   

##### IOC操作Bean管理（xml注入集合属性）

1. 注入数组类型属性
2. 注入List集合类型属性
3. 注入Map集合类型属性

（1）创建类，定义数组，list，map，set类型属性，生成对应set方法

```java
//1 数组类型属性
private String[] courses;
//2 list集合类型属性
private List<String> list;
//3 map集合类型属性
private Map<String,String> maps;
//4 set集合类型属性
private Set<String> sets;

public void setSets(Set<String> sets) {
    this.sets = sets;
}

public void setList(List<String> list) {
    this.list = list;
}

public void setMaps(Map<String, String> maps) {
    this.maps = maps;
}

public void setCourses(String[] courses) {
    this.courses = courses;
}
```

（2）在sprin配置文件进行配置

```java
<!--1 集合类型属性注入-->
<bean id="stu" class="com.spring5.collectiontype.Stu">
    <!--数组类型属性注入-->
    <property name="courses">
        <array>
            <value>java课程</value>
            <value>数据库课程</value>
        </array>
    </property>
    <!--list类型属性注入-->
    <property name="list">
        <list>
            <value>张三</value>
            <value>李四</value>
        </list>
    </property>
    <!--map类型属性注入-->
    <property name="maps">
        <map>
            <entry key="JAVA" value="java"></entry>
            <entry key="PHP" value="php"></entry>
        </map>
    </property>
    <!--set类型属性注入-->
    <property name="sets">
        <set>
            <value>Mysql</value>
            <value>Redis</value>
        </set>
    </property>
</bean>
```

4. 在集合里面设置对象类型值

   ```java
   <!--创建多个course对象-->
   <bean id="course1" class="com.spring5.collectiontype.Course">
       <property name="cname" value="Spring5框架"></property>
   </bean>
   <bean id="course2" class="com.spring5.collectiontype.Course">
       <property name="cname" value="MyBatis框架"></property>
   </bean>
   ```

   ```java
   <!--注入list集合类型，值是对象-->
   <property name="courseList">
       <list>
           <ref bean="course1"></ref>
           <ref bean="course2"></ref>
       </list>
   </property>
   ```

5. 把集合注入的部分提取出来

   （1）在spring配置文件中引入名称空间 util

   ```java
   xmlns:util="http://www.springframework.org/schema/util"
   xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd http://www.springframework.org/schema/util https://www.springframework.org/schema/util/spring-util.xsd">
   ```

   （2）使用util标签完成list集合注入提取

   ```java
   <!--1 提取list集合类型属性注入-->
   <util:list id="bookList">
       <value>语文</value>
       <value>数学</value>
       <value>英语</value>
   </util:list>
   <!--2 提取list集合类型属性注入使用-->
   <bean id="book" class="com.spring5.collectiontype.Book">
       <property name="list" ref="bookList"></property>
   </bean>
   ```

##### IOC操作Bean管理（FactoryBean）

1. Spring有两种类型bean，一种是普通的bean，另外一种是工厂bean（FactoryBean）

2. 普通bean：在配置文件中定义bean类型就是返回类型

3. 工厂bean：在配置文件定义bean类型可以和返回类型不一样

   > 第一步：创建类，让这个类作为工厂bean，实现接口FactoryBean
   >
   > 第二步：实现接口里面的方法，在实现的方法中定义返回的bean类型

```java
public class MyBean implements FactoryBean {

    //定义返回bean
    @Override
    public Course getObject() throws Exception {
        Course course = new Course();
        course.setCname("abc");
        return course;
    }

    @Override
    public Class<?> getObjectType() {
        return null;
    }

    @Override
    public boolean isSingleton() {
        return false;
    }
}
```

```r
bean3.xml:
<bean id="myBean" class="com.spring5.factorybean.MyBean"> </bean>
```

```java
@Test
public void testCollection3(){
    ApplicationContext context = new ClassPathXmlApplicationContext("bean3.xml");
    Course myBean = context.getBean("myBean", Course.class);
    System.out.println(myBean);
}
```

##### IOC操作Bean管理（bean作用域）

1. 在Spring里面，设置创建bean实例是单实例还是多实例

2. 在Spring里面，默认情况下，bean是单实例对象

   ![Screenshot_20210917_185341](E:\桌面\Screenshot_20210917_185341.jpg)

3. 如何设置单实例还是多实例

   （1）在spring配置文件bean标签里面有属性（scope）用于设置单实例还是多实例

   （2）scope属性值

   第一个值 默认值：singletton 表示单实例对象

   第二个值 prototype,表示是多实例对象

   ```java
   <bean id="book" class="com.spring5.collectiontype.Book" scope="prototype">
       <property name="list" ref="bookList"></property>
   </bean>
   ```

   ![image-20210917191941074](F:\笔记\image-20210917191941074.png)

   （3）singleton和prototype区别

   第一：singleten 单实例，prototype 多实例

   第二：设置scope值是singleten或空的时候，加载spring配置文件时候就会创建单实例对象

   ​          设置scope值是prototype的时候，不是在加载spring配置文件时候创建对象，在调用getBean方法的时候创建多实例

   

   ##### IOC操作Bean管理（bean生命周期）

   1. 生命周期：

      （1）从对象创建到对象销毁的过程

   2. bean生命周期：

      （1）通过构造器创建bean实例（无参数构造）

      （2）为bean的属性设置值和对其他bean引用（调用set方法）

      （3）调用bean的初始化的方法（需要进行配置初始化的方法）

      （4）bean可以使用了（对象已经获取到了）

      （5）当容器关闭时候，调用bean的销毁的方法（需要进行配置销毁的方法）

   3. 演示bean生命周期

   ```java
   public class Orders {
       //无参数构造
       public Orders(){
           System.out.println("第一步 执行无参数构造创建bean实例");
       }
   
       private String oname;
   
       public void setOname(String oname) {
           this.oname = oname;
           System.out.println("第二步 调用set方法设置属性值");
       }
   
       //创建执行的初始化的方法
       public void initMethod(){
           System.out.println("第三步 执行初始化的方法");
       }
       
       //创建执行的初始化的方法
       public void destroyMethod(){
           System.out.println("第五步 执行销毁的方法");
       }
   
   }
   ```

   ```java
   <bean id="orders" class="com.spring5.bean.Orders" init-method="initMethod" destroy-method="destroyMethod">
       <property name="oname" value="手机"></property>
   </bean>
   ```

   ```java
     @Test
       public void testBean3(){
           //ApplicationContext context = new ClassPathXmlApplicationContext("bean4.xml");
           ClassPathXmlApplicationContext context = new ClassPathXmlApplicationContext("bean4.xml");
           Orders orders = context.getBean("orders", Orders.class);
           System.out.println("第四步 获取创建bean实例对象");
           System.out.println(orders);
           
           //手动让bean实例销毁
           context.close();
       }
   ```

   ![image-20210918114613583](C:\Users\江流\AppData\Roaming\Typora\typora-user-images\image-20210918114613583.png)

4. bean的后置处理器，生命周期有七步

   （1）通过构造器创建bean实例（无参数构造）

   （2）为bean的属性设置值和对其他bean引用（调用set方法）

   （3）把bean实例传递bean后置处理器的方法 postProcessBeforeInitialization

   （4）调用bean的初始化的方法（需要进行配置初始化的方法）

   （5）把bean实例传递bean后置处理器的方法 postProcessAfterInitialization

   （6）bean可以使用了（对象已经获取到了）

   （7）当容器关闭时候，调用bean的销毁的方法（需要进行配置销毁的方法）

5. 演示添加后置处理器效果

   （1）创建类，实现接口BeanPostProcessor，创建后置处理器

   ```java
   public class MyBeanPost implements BeanPostProcessor {
   
       @Override
       public Object postProcessBeforeInitialization(Object bean, String beanName) throws BeansException {
           System.out.println("在初始化之前执行的方法");
           return bean;
       }
   
       @Override
       public Object postProcessAfterInitialization(Object bean, String beanName) throws BeansException {
           System.out.println("在初始化之后执行的方法");
           return bean;
       }
   }
   ```

   ```java
   <!--配置后置处理器-->
   <bean id="myBeanPost" class="com.spring5.bean.MyBeanPost"></bean>
   ```

   ![image-20210919151426938](C:\Users\江流\AppData\Roaming\Typora\typora-user-images\image-20210919151426938.png)

   

##### IOC操作Bean管理（xml自动装配）

1. 什么是自动装配

   （1）根据指定装配规则（属性名称或者属性类型），Spring自动将匹配的属性值注入

2. 演示自动装配过程

   （1）根据属性名称自动注入

   ```java
   <!--实现自动装配
       bean标签属性autowire，配置自动装配
       autowire属性常用两个值：
           byName根据属性名称注入，注入值bean的id值和类属性名称一样  
           byType根据属性类型注入
   -->
   <bean id="emp" class="com.spring5.autowire.Emp" autowire="byName">
       <!--<property name="dept" ref="dept"></property>-->
   </bean>
   <bean id="dept" class="com.spring5.autowire.Dept"></bean>
   ```

   （2）根据属性类型自动注入

   ```java
   <!--实现自动装配
       bean标签属性autowire，配置自动装配
       autowire属性常用两个值：
           byName根据属性名称注入，注入值bean的id值和类属性名称一样  
           byType根据属性类型注入
   -->
   <bean id="emp" class="com.spring5.autowire.Emp" autowire="byType">
       <!--<property name="dept" ref="dept"></property>-->
   </bean>
   <bean id="dept" class="com.spring5.autowire.Dept"></bean>
   ```



##### IOC操作Bean管理（外部属性文件）

1. 直接配置数据库信息

   （1）配置德鲁伊连接池

   （2）引入德鲁伊连接池依赖jar包

   ```java
   <!--直接配置连接池-->
   <bean id="dataSource" class="com.alibaba.druid.pool.DruidDataSource">
       <property name="driverClassName" value="com.mysql.jdbc.Driver"><!--驱动名称--></property>
       <property name="url" value="jdbc:mysql://localhost:3306/userDb"><!--数据库地址--></property>
       <property name="username" value="root"></property>
       <property name="password" value="12345678"></property>
   </bean>
   ```

   

2. 引入外部属性文件配置数据库连接池

   （1）创建外部属性文件，properties格式文件，写数据库信息

   ![image-20210920230259870](C:\Users\江流\AppData\Roaming\Typora\typora-user-images\image-20210920230259870.png)

   （2）把外部properties属性文件引入到spring配置文件中

   > 引入context名称空间
   >
   > ```java
   > xmlns:context="http://www.springframework.org/schema/context"
   > xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd 
   > http://www.springframework.org/schema/util https://www.springframework.org/schema/util/spring-util.xsd
   > http://www.springframework.org/schema/context https://www.springframework.org/schema/context/spring-context.xsd">
   > ```
   >
   > 在spring配置文件使用标签引入外部属性文件
   >
   > ```java
   > <!--引入外部的属性文件-->
   > <context:property-placeholder location="classpath:jdbc.properties"/>
   > <!--配置连接池-->
   >  <bean id="dataSource" class="com.alibaba.druid.pool.DruidDataSource">
   >      <property name="driverClassName" value="${prop.driverClass}"><!--驱动名称--></property>
   >      <property name="url" value="${prop.url}"><!--数据库地址--></property>
   >      <property name="username" value="${prop.userName}"></property>
   >      <property name="password" value="${prop.password}"></property>
   >  </bean>
   > ```

***

##### <font color="red">IOC操作Bean管理（基于注解方式）</font>

1. 什么是注解

   （1）注解是代码特殊标记，格式：@注解名称（属性名称=属性值，属性名称=属性值.....）

   （2）使用注解，注解作用在类上面，方法上面，属性上面

   （3）使用注解目的：简化xml配置

2. Spring针对Bean管理中创建对象提供注解

   （1）@Component：是基础注解，表示一个 JavaBean 可以被注入到 Spring 容器中

   （2）@Service：用在业务层，用来处理业务逻辑

   （3）@Controller：用在表现层，对来自前端的请求进行转发处理与重定向

   （4）@Repository：用在持久层，标注 DAO 类，表示这个类可以对数据库进行数据的读取或者写入

   > 上面四个注解功能是一样的，都可以用来创建bean实例

3. 基于注解方式实现对象创建

   第一步：引入依赖![image-20210921101116564](C:\Users\江流\AppData\Roaming\Typora\typora-user-images\image-20210921101116564.png)

   第二步：开启组件扫描

   ```java
      <!--开启组件扫描
      1 如果扫描多个包，多个包使用逗号隔开
      2 扫描包的上层目录 
      -->
   <context:component-scan base-package="com.spring5"></context:component-scan>
   ```

   第三步：创建类，在类上面添加创建对象注解

   ```java
   //在注解里面value属性值可以省略不写，
   //默认值是类名称，首字母小写 UserService--userService
   @Service(value = "userService") 
   //<bean id="userService" class="com.service.UserService">
   public class UserService {
       public void add(){
           System.out.println("service add....");
       }
   }
   ```

4. 开启组件扫描细节配置

   ```java
   <!--示例1
   use-default-filters="false 表示现在不使用默认的filter，自己配置filter
   context:include-filter，设置扫描哪些内容
   -->
   <context:component-scan base-package="com.spring5" use-default-filters="false">
       <context:include-filter type="annotation" expression="org.springframework.stereotype.Controller"/>
       <!--设置扫描注解为Controller的内容-->
   </context:component-scan>
   
   <!--示例2
   下面配置扫描包所有内容
   context:exclude-filter:设置哪些内容不进行扫描
   -->
   <context:component-scan base-package="com.spring5"jiy>
       <context:exclude-filter type="annotation" expression="org.springframework.stereotype.Controller"/>
       <!--设置不扫描注解为Controller的内容-->
   </context:component-scan>
   ```

5. 基于注解方式实现属性注入

   (1) @Autowired：根据属性类型进行自动装配

   > 第一步：把service和dao对象创建，在service和dao类添加创建对象注释
   >
   > 第二步：在service注入dao对象，在service类添加dao类型属性，在属性上面使用注释
   >
   > ```java
   > @Service
   > public class UserService {
   >  //定义dao类型属性
   >  //不需要添加set方法
   >  // 添加注入属性注解
   >  @Autowired  //根据类型进行注入
   >  private UserDao userDao;
   > 
   >  public void add(){
   >      System.out.println("service add....");
   >      userDao.add();
   >  }
   > }
   > ```

   (2) @Qualifier：根据名称进行注入

   > 这个@Qualifier注解的使用，和上面@Autowired一起使用
   >
   > ```java
   > @Service
   > public class UserService {
   >  //定义dao类型属性
   >  //不需要添加set方法
   >  // 添加注入属性注解
   >  @Autowired //根据类型进行注入
   >  @Qualifier(value = "userDaoImpl1")  //根据名称进行注入
   >  private UserDao userDao;
   > 
   >  public void add(){
   >      System.out.println("service add....");
   >      userDao.add();
   >  }
   > }
   > ```
   >
   > ```java
   > @Repository(value = "userDaoImpl1")
   > public class UserDaoImpl implements UserDao{
   >  @Override
   >  public void add() {
   >      System.out.println("dao add....");
   >  }
   > }
   > ```

   (3) @Resource：可以根据类型注入，可以根据名称注入  (在javax拓展包中，不是spring提供的)

   > ```java
   > //@Resource  //根据类型进行注入
   > @Resource(name = "userDaoImpl1") //根据名称进行注入
   > private UserDao userDao;
   > ```

   (4) @Value：注入普通类型属性

   > ```java
   > @Value(value = "abc")
   > private String name;
   > public void add(){
   >      System.out.println("service add...."+name);
   >      userDao.add();
   >  }
   > ```
   >
   > ![image-20210921170841353](C:\Users\江流\AppData\Roaming\Typora\typora-user-images\image-20210921170841353.png)


##### IOC完全注解开发

（1）创建配置类，替代xml配置文件

> ```java
> @Configuration //作为配置类，替代xml配置文件
> @ComponentScan(basePackages = {"com.spring5"}) //开启组件扫描
> public class SpringConfig {
> 
> }
> ```

（2）编写测试类

> ```java
> //Annotation:注解
> //Config:配置
> //ApplicationContext:配置文件
> @Test
> public void testService2() {
>  //加载配置类
>  ApplicationContext context = new AnnotationConfigApplicationContext(SpringConfig.class);
>  UserService userService=context.getBean("userService", UserService.class);
>  System.out.println(userService);
>  userService.add();
> }
> ```



## 3.Aop

##### AOP(概念)

1. 什么是AOP

   （1）面向切面编程（方面），利用AOP可以对业务逻辑的各个部分进行隔离，从而使得业务逻辑各部分之间的[耦合度](https://baike.baidu.com/item/耦合度/2603938)降低，提高程序的可重用性，同时提高了开发的效率。

   （2）通俗描述：不通过修改源代码方式，在主干功能里添加新功能

   （3）使用登录的例子说明AOP

   <img src="file:///C:\Users\江流\Documents\Tencent Files\1746644290\Image\C2C\499DF78997C0A5E663C1263BA6405902.jpg" alt="img" style="zoom:80%;" />

   

##### AOP（底层原理）

1. AOP底层使用动态代理

   （1）有两种情况动态代理

   > 第一种：有接口情况，使用JDK动态代理
   >
   > * 创建接口实现类代理对象，增强类的方法
   >
   > ![image-20210921195834206](C:\Users\江流\AppData\Roaming\Typora\typora-user-images\image-20210921195834206.png)
   >
   > 第二种：没有接口情况，使用CGLIB代理
   >
   > * 创建子类的代理对象，增强类的方法
   >
   > ![image-20210922194435974](C:\Users\江流\AppData\Roaming\Typora\typora-user-images\image-20210922194435974.png)

   ***

##### AOP（JDK动态代理）

1. 使用JDK动态代理，使用Proxy类里面的方法创建代理对象

   <img src="C:\Users\江流\AppData\Roaming\Typora\typora-user-images\image-20210922195132462.png" alt="image-20210922195132462"  align="left" />

   （1）调用newProxyInstance方法

   ![image-20210922195809368](C:\Users\江流\AppData\Roaming\Typora\typora-user-images\image-20210922195809368.png)

   方法有三个参数：

   第一参数，类加载器

   第二参数，增强方法所在的类，这个类实现的接口，支持多个接口

   第三参数，实现这个接口InvocationHandler，创建代理对象，写增强的方法

2. JDK动态代理代码

   （1）创建接口，定义方法

   ```java
   public interface UserDao {
       public int add(int a,int b);
       public String update(String id);
   }
   ```

   （2）创建接口实现类，实现方法

   ```java
   public class UserDaoImpl implements UserDao{
       @Override
       public int add(int a, int b) {
           return a+b;
       }
   
       @Override
       public String update(String id) {
           return id;
       }
   }
   ```

   （3）使用Proxy类创建接口代理对象

   ```java
   package com.spring5;
   import java.lang.reflect.InvocationHandler;
   import java.lang.reflect.Method;
   import java.lang.reflect.Proxy;
   import java.util.Arrays;
   
   public class JDKProxy {
   
       public static void main(String[] args) {
           //创建接口实现类代理对象
           Class[] interfaces = {UserDao.class};
   //        Proxy.newProxyInstance(JDKProxy.class.getClassLoader(), interfaces, new InvocationHandler() {
   //            @Override
   //            public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
   //                return null;
   //            }
   //        });
           UserDaoImpl userDao = new UserDaoImpl();
           UserDao dao = (UserDao) Proxy.newProxyInstance(JDKProxy.class.getClassLoader(), interfaces,new UserDaoProxy(userDao));
           int result = dao.add(1,2);
           System.out.println("result:"+result);
       }
   }
   
   //创建代理对象代码
   class UserDaoProxy implements InvocationHandler{
       //1 把创建的是谁的代理对象，把谁传递过来
       //有参数构造传递
       private Object obj;
       public UserDaoProxy(Object obj){
           this.obj=obj;
       }
       //增强的逻辑
       @Override
       public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
           //方法之前
           System.out.println("方法之前执行...."+method.getName()+":参数的传递...."+ Arrays.toString(args));
           //被增强的方法执行
           Object res =method.invoke(obj,args);
           //方法之后
           System.out.println("方法之后执行..."+obj);
           return res;
       }
   }
   ```

   ![image-20210923203904005](C:\Users\江流\AppData\Roaming\Typora\typora-user-images\image-20210923203904005.png)



##### AOP(术语)

1. 连接点 ：类里面哪些方法可以被增强，这些方法称为连接点

2. 切入点 ：实际被真正增强的方法，称为切入点

3. 通知（增强）

   （1）实际增强的逻辑部分称为通知（增强）

   （2）通知有多种类型

   * 前置通知
   * 后置通知
   * 环绕通知
   * 异常通知
   * 最终通知：finally

4. 切面：是动作

   （1）把通知应用到切入点过程

   ***

##### AOP操作（准备）

1. Spring框架一般都是基于AspectJ实现AOP操作

   （1）什么是AspectJ

   * AspectJ不是Spring组成部分，是独立AOP框架，一般把AspectJ和Spring框架一起使用，进行AOP操作

2. 基于AspectJ实现AOP操作

   （1）基于xml配置文件实现

   （2）基于注解方式实现（一般使用）

3. 在项目工厂里面引入AOP相关依赖

   <img src="C:\Users\江流\AppData\Roaming\Typora\typora-user-images\image-20210924131644127.png" alt="image-20210924131644127" style="zoom:80%;" align="left"/>

   

4. 切入点表达式

   （1）切入点表达式作用：知道对哪个类里面的哪个方法进行增强

   （2）语法结构：

   * execution([权限修饰符] [返回类型] [类全路径] [方法名称] ([参数列表]))

   > 举例1：对com.dao.BookDao类里面的add进行增强
   >
   > * execution(* com.dao.BookDao.add(...));
   > * [权限修饰符]为*任意类型   [返回类型] 可不写  
   > * [类全路径] 为com.dao.BookDao ：  [方法名称]为add  ：([参数列表])为(...)
   >
   > 举例2：对com.dao.BookDao类里面的所有方法进行增强
   >
   > * execution(* com.dao.BookDao.*(...));
   >
   > 举例3：对com.dao包里面所有类和类里面方法进行增强
   >
   > * execution(* com.dao.*. *(...));

***

##### AOP操作（AspectJ注解）

1. 创建类，在类里面定义方法

   ```java
   public class User {
       public void add(){
           System.out.println("add.......");
       }
   }
   ```

2. 创建增强类（编写增强逻辑）

   （1）在增强类里面创建方法，让不同方法代表不同通知类型

   ```java
   //增强的类
   public class UserProxy {
       //前置通知
       public void before(){
           System.out.println("before.....");
       }
   }
   ```

3. 进行通知的配置

   （1）在Spring配置文件中，开启注解扫描

   ```java
   <?xml version="1.0" encoding="UTF-8"?>
   <beans xmlns="http://www.springframework.org/schema/beans"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xmlns:context="http://www.springframework.org/schema/context"
          xmlns:aop="http://www.springframework.org/schema/aop"
          xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
                              http://www.springframework.org/schema/context  http://www.springframework.org/schema/context/spring-context.xsd
                              http://www.springframework.org/schema/aop http://www.springframework.org/schema/aop/spring-aop.xsd">
   
       <!--开启注解扫描-->
       <context:component-scan base-package="com.spring5.aopanno"></context:component-scan>
   
   </beans>
   ```

   （2）使用注解创建User和UserProxy对象

   <img src="C:\Users\江流\AppData\Roaming\Typora\typora-user-images\image-20210924142243587.png" alt="image-20210924142243587" style="zoom:80%;" align="left"/><img src="C:\Users\江流\AppData\Roaming\Typora\typora-user-images\image-20210924142337049.png" alt="image-20210924142337049" style="zoom:80%;" />

   （3）在增强类什么添加注解@Aspect

   ```java
   //增强的类
   @Component
   @Aspect  //生成代理对象
   public class UserProxy {
       //前置通知
       public void before(){
           System.out.println("before.....");
       }
   }
   ```

   （4）在spring配置文件中开启生成代理对象

   ```java
   <!--开启Aspect生成代理对象-->
   <aop:aspectj-autoproxy></aop:aspectj-autoproxy>
   ```

4. 配置不同类型的通知

   （1）在增强类的里面，在作为通知方法上面添加通知类型注解，使用切入点表达式配置

   ```java
   //增强的类
   @Component
   @Aspect  //生成代理对象
   public class UserProxy {
       //前置通知
       //@Before注解表示作为前置通知
       @Before(value = "execution(* com.spring5.aopanno.User.add())")
       public void before(){
           System.out.println("before.....");
       }
   }
   ```

   ```java
   //增强的类
   @Component
   @Aspect  //生成代理对象
   public class UserProxy {
       //前置通知
       //@Before注解表示作为前置通知
       @Before(value = "execution(* com.spring5.aopanno.User.add())")
       public void before(){
           System.out.println("before.....");
       }
   
       //最终通知
       @After(value = "execution(* com.spring5.aopanno.User.add())")
       public void after(){
           System.out.println("after.....");
       }
   
       //后置通知（返回通知）
       @AfterReturning(value = "execution(* com.spring5.aopanno.User.add())")
       public void afterReturn(){
           System.out.println("afterReturn.....");
       }
   
       //异常通知
       @AfterThrowing(value = "execution(* com.spring5.aopanno.User.add())")
       public void afterThrowing(){
           System.out.println("afterThrowing.....");
       }
   
       //环绕通知
       @Around(value = "execution(* com.spring5.aopanno.User.add())")
       public void around(ProceedingJoinPoint proceedingJoinPoint) throws Throwable{
           System.out.println("环绕之前.....");
           //被增强的方法执行
           proceedingJoinPoint.proceed();
           System.out.println("环绕之后.....");
       }
   }
   ```

   <img src="C:\Users\江流\AppData\Roaming\Typora\typora-user-images\image-20210924162427057.png" alt="image-20210924162427057" style="zoom:80%;" />

5. 相同的切入点抽取

   ```java
   //相同的切入点抽取
   @Pointcut(value = "execution(* com.spring5.aopanno.User.add())")
   public void pointdemo(){
       
   }
   
   //前置通知
   //@Before注解表示作为前置通知
   @Before(value = "pointdemo()")
   public void before(){
       System.out.println("before.....");
   }
   ```

6. 有多个增强类对同一个方法进行增强，设置增强类优先级

   （1）在增强类上面添加注解@Order(数字类型的值)，数字类型值越小优先级越高

   ```java
   //增强的类
   @Component
   @Aspect  //生成代理对象
   @Order(1)
   public class PersonProxy {
       //前置通知
       //@Before注解表示作为前置通知
       @Before(value = "execution(* com.spring5.aopanno.User.add(..))")
       public void before(){
           System.out.println("Person before.....");
       }
   }
   ```

***

##### AOP操作（AspectJ配置文件）

1. 创建两个类，增强类和被增强类，创建方法

2. 在spring配置文件中创建两个类对象

   ```java
   <!--创建对象-->
   <bean id="book" class="com.spring5.aopxml.Book"></bean>
   <bean id="bookProxy" class="com.spring5.aopxml.BookProxy"></bean>
   ```

3. 在spring配置文件中配置切入点

   ```java
   <!--配置aop增强-->
   <aop:config>
       <!--切入点-->
       <aop:pointcut id="p" expression="execution(* com.spring5.aopxml.Book.buy(..))"/>
       <!--配置切面 ref指的是增强类-->
       <aop:aspect ref="bookProxy">
           <!--增强作用在具体的方法上 pointcut-ref指的是作用在哪个类即被增强类-->
           <aop:before method="before" pointcut-ref="p"></aop:before>
       </aop:aspect>
   </aop:config>
   ```

##### AOP完全注解开发

创建配置类，不需要创建xml配置文件

```java
package com.spring5.config;

import org.springframework.context.annotation.ComponentScan;
import org.springframework.context.annotation.Configuration;
import org.springframework.context.annotation.EnableAspectJAutoProxy;

@Configuration
@ComponentScan(basePackages = {"com"}) //开启组件扫描
@EnableAspectJAutoProxy(proxyTargetClass = true) //开启Aspect生成代理对象
public class ConfigAop {
}
```



## 4.JdbcTemplate

##### JdbcTemplate（概念和准备工作）

1. 什么是JdbcTemplate

   * Spring框架对JDBC进行封装，使用JdbcTemplate方便实现数据库操作

2. 准备工作

   * 引入相关jar包

     <img src="C:\Users\江流\AppData\Roaming\Typora\typora-user-images\image-20210925113817534.png" alt="image-20210925113817534" style="zoom: 80%;" align="left"/>

   * 在spring配置文件配置数据库连接池

     ```java
     <!--数据库连接池-->
     <bean id="dataSource" class="com.alibaba.druid.pool.DruidDataSource" destroy-method="close">
         <property name="url" value="jdbc:mysql:///user_db"></property>
         <property name="username" value="root"></property>
         <property name="password" value="10250511biubiu"></property>
         <property name="driverClassName" value="com.mysql.jdbc.Driver"></property>
     </bean>
     ```

   * 配置JdbcTemplate对象，注入DataSource

     ```java
     <!--JdbcTemplate对象-->
     <bean id="jdbcTemplate" class="org.springframework.jdbc.core.JdbcTemplate">
         <!--注入dataSource-->
         <property name="dataSource" ref="dataSource"></property>
     </bean>
     ```

   * 创建service类，创建dao类，在dao注入JdbcTemplate对象

     > 配置文件
     >
     > ```java
     > <!--组件扫描-->
     > <context:component-scan base-package="com.spring5"></context:component-scan>
     > ```
     >
     > Service文件：
     >
     > ```java
     > @Service
     > public class BookService {
     >  //注入dao
     >  @Autowired
     >  private BookDao bookDao;
     > 
     > }
     > ```
     >
     > Dao文件：
     >
     > ```java
     > @Repository
     > public class BookDaoImpl implements BookDao{
     > 
     >  //注入JdbcTemplate
     >  @Autowired
     >  private JdbcTemplate jdbcTemplate;
     > }
     > ```



##### JdbcTemplate操作数据库（添加）

1. 对应数据库创建实体类

   ```java
   public class Book {
       private String userId;
       private String username;
       private String ustatus;
   
       public void setUserId(String userId) {
           this.userId = userId;
       }
       public void setUsername(String username) {
           this.username = username;
       }
       public void setUstatus(String ustatus) {
           this.ustatus = ustatus;
       }
   
       public String getUserId() {
           return userId;
       }
       public String getUsername() {
           return username;
       }
       public String getUstatus() {
           return ustatus;
       }
   }
   ```

2. 编写service和dao

   * 在dao进行数据库添加操作

   * 调用JdbcTemplate对象里面update方法实现添加操作

     * 有两个参数

     * 第一个参数：sql语句

     * 第二个参数：可变参数。设置sql语句值

       ```java
       @Repository
       public class BookDaoImpl implements BookDao{
       
           //注入JdbcTemplate
           @Autowired
           private JdbcTemplate jdbcTemplate;
       
           //添加的方法
           @Override
           public void add(Book book) {
               //1 创建sql语句
               String sql="insert into t_book value(?,?,?)";
               //2 调用方法实现
               Object[] args = {book.getUserId(),book.getUsername(),book.getUstatus()};
               int update = jdbcTemplate.update(sql,args);
               //int update = jdbcTemplate.update(sql,book.getUserId(),book.getUsername(),book.getUstatus());
               System.out.println(update);
           }
       }
       ```

     * 测试类

       ```java
       public class TestBook {
       
           @Test
           public void testJdbcTemplate(){
               ApplicationContext context =
                       new ClassPathXmlApplicationContext("bean1.xml");
               BookService bookService =context.getBean("bookService", BookService.class);
               Book book = new Book();
               book.setUserId("1");
               book.setUsername("java");
               book.setUstatus("a");
               bookService.addBook(book);
           }
       }
       ```

       ***

       

##### JdbcTemplate操作数据库（修改和删除）

```java
//修改的方法
@Override
public void update(Book book) {
    //1 创建sql语句
    String sql="update t_book set username = ?,ustatus=? where user_id=?";
    //2 调用方法实现
    Object[] args = {book.getUsername(),book.getUstatus(),book.getUserId()};
    int update = jdbcTemplate.update(sql,args);
    System.out.println(update);
}

//删除的方法
@Override
public void delete(String id) {
    String sql="delete from t_book where user_id=?";
    int update= jdbcTemplate.update(sql,id);
    System.out.println(update);
}
```



##### JdbcTemplate操作数据库（查询返回某个值）

1. 查询表里面有多少条记录，返回某个值

2. 使用JdbcTemplate实现查询返回某个值代码

   ![image-20210926103038444](C:\Users\江流\AppData\Roaming\Typora\typora-user-images\image-20210926103038444.png)

   * 有两个参数

   * 第一个参数：sql语句

   * 返回类型Class

     ```java
     //查询表记录数
     @Override
     public int selectCount() {
         String sql="select count(*) from t_book";
         Integer count = jdbcTemplate.queryForObject(sql,Integer.class);
         return count;
     }
     ```

     ***

##### JdbcTemplate操作数据库（查询返回对象）

1. 场景：查询图书详情

2. JdbcTemplate实现查询返回对象

   ![image-20210926104758358](C:\Users\江流\AppData\Roaming\Typora\typora-user-images\image-20210926104758358.png)

   * 有三个参数

   * 第一个参数：sql语句

   * 第二个参数：RowMapper ：是接口，返回不同类型的数据，使用这个接口里面实现类完成数据封装

   * 第三个参数：sql语句值

     ```java
     //查询返回对象
     @Override
     public Book findBookInfo(String id) {
         String sql="select * from t_book where user_id=?";
         //调用方法
         Book book = jdbcTemplate.queryForObject(sql,new BeanPropertyRowMapper<Book>(Book.class));
         return book;
     }
     ```



##### JdbcTemplate操作数据库（查询返回集合）

1. 场景：查询图书列表分页...

2. 调用JdbcTemplate方法实现查询返回集合

   ![image-20210926111418111](C:\Users\江流\AppData\Roaming\Typora\typora-user-images\image-20210926111418111.png)

   * 有三个参数

   * 第一个参数：sql语句

   * 第二个参数：RowMapper ：是接口，返回不同类型的数据，使用这个接口里面实现类完成数据封装

   * 第三个参数：sql语句值

     ```java
     //查询返回集合
     @Override
     public List<Book> findAllBook() {
         String sql = "select * from t_book";
         //调用方法
         List<Book> bookList=jdbcTemplate.query(sql,new BeanPropertyRowMapper<Book>(Book.class));
         return bookList;
     }
     ```

   ***

##### JdbcTemplate操作数据库（批量操作）

1. 批量操作：操作表里面多条记录

2. JdbcTemplate实现批量添加操作

   ![image-20210926112243272](C:\Users\江流\AppData\Roaming\Typora\typora-user-images\image-20210926112243272.png)

   * 有两个参数

   * 第一个参数：sql语句

   * 第二个参数：List集合，添加多头记录数据

     ```java
     //批量添加
     @Override
     public void batchAddBook(List<Object[]> batchArgs) {
         String sql = "insert into t_book value(?,?,?)";
         int[] ints = jdbcTemplate.batchUpdate(sql,batchArgs);
         System.out.println(Arrays.toString(ints));
     }
     ```

     ```java
     //批量添加测试
     List<Object[]> batchArgs = new ArrayList<>();
     Object[] o1 = {"3","java","a"};
     Object[] o2 = {"4","java","b"};
     Object[] o3 = {"5","java","c"};
     batchArgs.add(o1);
     batchArgs.add(o2);
     batchArgs.add(o3);
     //调用批量添加
     bookService.batchAdd(batchArgs);
     ```

3. JdbcTemplate实现批量修改操作

   ```java
   //批量修改
   @Override
   public void batchUpdateBook(List<Object[]> batchArgs) {
       String sql="update t_book set username = ?,ustatus=? where user_id=?";
       int[] ints = jdbcTemplate.batchUpdate(sql,batchArgs);
       System.out.println(Arrays.toString(ints));
   }
   ```

   ```java
   //批量修改
   List<Object[]> batchArgs = new ArrayList<>();
   Object[] o1 = {"java12","a","3"};
   Object[] o2 = {"java123","b","4"};
   Object[] o3 = {"java134","c","5"};
   batchArgs.add(o1);
   batchArgs.add(o2);
   batchArgs.add(o3);
   //调用方法实现批量修改
   bookService.batchUpdate(batchArgs);
   ```

4. JdbcTemplate实现批量删除操作

   ```java
   //批量删除
   @Override
   public void batchDeleteBook(List<Object[]> batchArgs) {
       String sql="delete from t_book where user_id=?";
       int[] ints = jdbcTemplate.batchUpdate(sql,batchArgs);
       System.out.println(Arrays.toString(ints));
   }
   ```

   ```java
   //批量删除
   List<Object[]> batchArgs = new ArrayList<>();
   Object[] o1 = {"3"};
   Object[] o2 = {"4"};
   batchArgs.add(o1);
   batchArgs.add(o2);
   //调用方法实现批量删除
   bookService.batchDelete(batchArgs);
   ```



## 5.事务管理

##### 事务概念

1. 什么事务

   （1）事务是数据库操作最基本单元，逻辑上一组操作，要么都成功，如果有一个失败所有

   （2）典型场景：银行转账

   ​         lucy 转出 少钱

   ​         mary 收到转账 多钱

2. 事务四个特性（ACID）

   （1）原子性： 

   （2）一致性：

   （3）隔离性：

   （4）持久性：

##### 事务操作（搭建事务操作环节）

![image-20210927091108527](C:\Users\江流\AppData\Roaming\Typora\typora-user-images\image-20210927091108527.png)

1. 创建数据库表，添加记录

   ![image-20210927091534733](C:\Users\江流\AppData\Roaming\Typora\typora-user-images\image-20210927091534733.png)

2. 创建service，搭建dao，完成对象创建和注入关系

   * service注入dao，在dao注入JdbcTemplate，在JdbcTemplate注入DataSource

     ```java
     @Service
     public class UserService {
     
         //注入dao
         @Autowired
         private UserDao userDao;
     }
     ```

     ```java
     @Repository
     public class UserDaoImpl implements UserDao{
     
         @Autowired
         private JdbcTemplate jdbcTemplate;
     }
     ```

3. 在dao创建两个方法，多钱和少钱的方法，在service中创建方法（转账的方法）

   ```java
   @Repository
   public class UserDaoImpl implements UserDao{
   
       @Autowired
       private JdbcTemplate jdbcTemplate;
   
       //lucy转账100给mary
       //多钱
       @Override
       public void addMoney() {
           String sql = "update t_account set money=money-? where username=?";
           jdbcTemplate.update(sql,100,"lucy");
   
       }
   
       //少钱
       @Override
       public void reduceMoney() {
           String sql = "update t_account set money=money+? where username=?";
           jdbcTemplate.update(sql,100,"mary");
       }
   }
   ```

   ```java
   @Service
   public class UserService {
   
       //注入dao
       @Autowired
       private UserDao userDao;
   
       //转账的方法
       public void accountMoney(){
           //lucy少100
           userDao.reduceMoney();
           //mary多100
           userDao.addMoney();
       }
   }
   ```

   测试：

   ```java
   @Test
   public void testAccount(){
       ApplicationContext context =
               new ClassPathXmlApplicationContext("bean1.xml");
       UserService userService=context.getBean("userService", UserService.class);
       userService.accountMoney();
   
   }
   ```

4. 上面代码，如果正常执行是没有问题的，但是如果代码执行过程中出现异常，有问题

   ```java
   //转账的方法
   public void accountMoney(){
       //lucy少100
       userDao.reduceMoney();
   
       //模拟异常
       int i=10/0;
   
       //mary多100
       userDao.addMoney();
   }
   ```

   > * 上面问题如何解决
   >
   >   * 使用事务进行解决
   >
   > * 事务操作过程
   >
   >   <img src="C:\Users\江流\AppData\Roaming\Typora\typora-user-images\image-20210927101720001.png" alt="image-20210927101720001" style="zoom:80%;" />

***

##### 事务操作（Spring事务管理介绍）

1. 事务添加到javaEE三层结构里面Service层（业务逻辑层）

2. 在Spring进行事务管理操作

   * 有两种方式：编程式事务管理和声明式事务管理（一般使用）

3. 声明式事务管理

   * 基于注解方式（一般使用）
   * 基于xml配置文件方式

4. 在Spring进行声明式事务管理，底层使用AOP原理

   <font color="red" >***事务管理，底层使用AOP原理***</font>

5. Spring事务管理API

   * 提供一个接口，代表事务管理器，这个接口针对不同的框架提供不同的实现类

     ![image-20210927104045496](C:\Users\江流\AppData\Roaming\Typora\typora-user-images\image-20210927104045496.png)



##### 事务操作（注解声明式事务管理）

1. 在spring配置文件配置事务管理器

   ```java
   <!--创建事务管理器-->
   <bean id="transactionManager" class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
       <!--注入数据源-->
       <property name="dataSource" ref="dataSource"></property>
   </bean>
   ```

2. 在spring配置文件中，开启事务注解

   * 在spring配置文件中引入名称空间tx

     ```java
     <?xml version="1.0" encoding="UTF-8"?>
     <beans xmlns="http://www.springframework.org/schema/beans"
            xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
            xmlns:context="http://www.springframework.org/schema/context"
            xmlns:aop="http://www.springframework.org/schema/aop"
            xmlns:tx="http://www.springframework.org/schema/tx"
            xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
                                http://www.springframework.org/schema/context  http://www.springframework.org/schema/context/spring-context.xsd
                                http://www.springframework.org/schema/aop http://www.springframework.org/schema/aop/spring-aop.xsd
                                http://www.springframework.org/schema/tx http://www.springframework.org/schema/tx/spring-tx.xsd">
     ```

   * 开启事务注解

     ```java
     <!--开启事务注解 transaction-manager指的是开启的事务管理器名称-->
     <tx:annotation-driven transaction-manager="transactionManager"></tx:annotation-driven>
     ```

3. 在service类上面（获取service类里面方法上面）添加事务注解

   * @Transactional，这个注解添加到类声明，也可以添加到方法上面

   * 如果把这个注解添加到类上面，这个类里面所有的方法都添加事务

   * 如果把这个注解添加到方法上面，则为这个方法添加事务

     ```java
     @Service
     @Transactional
     public class UserService {
     ```

***

##### 事务操作（声明式事务管理参数配置）

1. 在service类上面添加注解@Transactional，在这个注解里面可以配置事务相关参数

   ![image-20210927163736787](C:\Users\江流\AppData\Roaming\Typora\typora-user-images\image-20210927163736787.png)

   ![image-20210927163938362](C:\Users\江流\AppData\Roaming\Typora\typora-user-images\image-20210927163938362.png)

2. propagation：事务传播行为

   <img src="C:\Users\江流\AppData\Roaming\Typora\typora-user-images\image-20210927173542880.png" alt="image-20210927173542880" style="zoom:50%;" />

   * 多事务方法直接进行调用，这个过程中事务是如何进行管理的

     ![image-20210927173927555](C:\Users\江流\AppData\Roaming\Typora\typora-user-images\image-20210927173927555.png)

     ```java
     @Service
     @Transactional(propagation = Propagation.REQUIRED) //默认情况
     public class UserService {
     ```

3. ioslation：事务隔离级别

   * 事务由特性称为隔离性，多事务操作之间不会产生影响，不考虑隔离性产生很多问题

   * 有三个读问题：脏读、不可重复读、虚（幻）读

   * 脏读：一个未提交事务读取到另一个未提交事务的数据

     ![image-20210927175733413](C:\Users\江流\AppData\Roaming\Typora\typora-user-images\image-20210927175733413.png)

   * 不可重复读：一个未提交事务读取到另一提交事务修改数据

     ![image-20210927180610796](C:\Users\江流\AppData\Roaming\Typora\typora-user-images\image-20210927180610796.png)

     ***

   * 虚（幻）读：一个未提交事务读取到另一提交事务添加数据

     ***

   * 解决：通过设置事务隔离级别，解决读问题

     ![image-20210927184441489](C:\Users\江流\AppData\Roaming\Typora\typora-user-images\image-20210927184441489.png)

     ```java
     @Service
     @Transactional(propagation = Propagation.REQUIRED,isolation = Isolation.REPEATABLE_READ) //默认情况
     public class UserService {
     ```

   

4. timeout：超时时间

   * 事务需要在一定时间内进行提交，如果不提交进行回滚
   * 默认值是-1，设置时间以秒单位进行，-1为永不超时，无限大

5. readOnly：是否只读

   * 读：查询操作，写：添加修改删除操作
   * readOnly默认值false，表示可以查询，可以添加修改删除操作
   * 设置readOnly值是true，设置成true之后，只能查询

6. rollbackFor：回滚

   * 设置出现哪些异常进行事务回滚

7. noRollbackFor：不回滚

   * 设置出现哪些异常不进行事务回滚



***

##### 事务操作（XML声明式事务管理）

1. 在spring配置文件中进行配置

   * 第一步：配置事务管理器

   * 第二步：配置通知（增强的部分）

   * 第三步：配置切入点和切面

     ```java
     <?xml version="1.0" encoding="UTF-8"?>
     <beans xmlns="http://www.springframework.org/schema/beans"
            xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
            xmlns:context="http://www.springframework.org/schema/context"
            xmlns:aop="http://www.springframework.org/schema/aop"
            xmlns:tx="http://www.springframework.org/schema/tx"
            xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
                                http://www.springframework.org/schema/context  http://www.springframework.org/schema/context/spring-context.xsd
                                http://www.springframework.org/schema/aop http://www.springframework.org/schema/aop/spring-aop.xsd
                                http://www.springframework.org/schema/tx http://www.springframework.org/schema/tx/spring-tx.xsd">
     
         <!--组件扫描-->
         <context:component-scan base-package="com.spring5"></context:component-scan>
     
         <!--数据库连接池-->
         <bean id="dataSource" class="com.alibaba.druid.pool.DruidDataSource" destroy-method="close">
             <property name="url" value="jdbc:mysql:///user_db"></property>
             <property name="username" value="root"></property>
             <property name="password" value="10250511biubiu"></property>
             <property name="driverClassName" value="com.mysql.jdbc.Driver"></property>
         </bean>
     
         <!--JdbcTemplate对象-->
         <bean id="jdbcTemplate" class="org.springframework.jdbc.core.JdbcTemplate">
             <!--注入dataSource-->
             <property name="dataSource" ref="dataSource"></property>
         </bean>
     
         <!--1 创建事务管理器-->
         <bean id="transactionManager" class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
             <!--注入数据源-->
             <property name="dataSource" ref="dataSource"></property>
         </bean>
     
         <!--2 配置通知-->
         <tx:advice id="txadvice">
             <!--配置事务参数-->
             <tx:attributes>
                 <!--指定哪种规则的方法上面添加事务-->
                 <tx:method name="accountMoney" propagation="REQUIRED"/>
                 <!--<tx:method name="account*"/>-->
             </tx:attributes>
         </tx:advice>
     
         <!--3 配置切入点和切面-->
         <aop:config>
             <!--配置切入点-->
             <aop:pointcut id="pt" expression="execution(* com.spring5.service.UserService.*(..))"/>
             <!--配置切面-->
             <aop:advisor advice-ref="txadvice" pointcut-ref="pt"/>
         </aop:config>
     
     </beans>
     ```

***

##### 事务操作（完全注解声明式事务管理）

1. 创建配置类，使用配置类代替xml文件

   ```java
   @Configuration  //配置类
   @ComponentScan(basePackages = "com") //开启组件扫描
   @EnableTransactionManagement //开启事务
   public class TxConfig {
   
       //创建数据库连接池
       @Bean
       public DruidDataSource getDruidDataSource(){
           DruidDataSource dataSource = new DruidDataSource();
           dataSource.setDriverClassName("com.mysql.jdbc.Driver");
           dataSource.setUrl("jdbc:mysql:///user_db");
           dataSource.setUsername("root");
           dataSource.setPassword("10250511biubiu");
           return dataSource;
       }
   
       //创建JdbcTemplate对象
       @Bean
       public JdbcTemplate getJdbcTemplate(DataSource dataSource){
           //到IOC容器中根据类型找到dataSource
           JdbcTemplate jdbcTemplate = new JdbcTemplate();
           //注入dataSource
           jdbcTemplate.setDataSource(dataSource);
           return jdbcTemplate;
       }
   
       //创建事务管理器
       @Bean
       public DataSourceTransactionManager setDataSourceTransactionManager(DataSource dataSource){
           DataSourceTransactionManager transactionManager=new DataSourceTransactionManager();
           transactionManager.setDataSource(dataSource);
           return transactionManager;
   
       }
   
   }
   ```

2. 测试类：

   ```java
   @Test
   public void testAccount2(){
       ApplicationContext context =
               new AnnotationConfigApplicationContext(TxConfig.class);
       UserService userService=context.getBean("userService", UserService.class);
       userService.accountMoney();
   
   }
   ```



## 6.Spring5新特性

##### Spring5框架新功能

1. 整个Spring5框架的代码基于Java8，运行时兼容JDK9，许多不建议使用的类和方法在代码库中删除

2. Spring5.0框架自带了通用的日志封装

   * Spring5已经移除Log4jConfigListener，官方建议使用Log4j2
   * Spring5框架整合Log4j2

   第一步引入jar包

   ![image-20211008110733844](C:\Users\江流\AppData\Roaming\Typora\typora-user-images\image-20211008110733844.png)

   第二步 创建log4j2.xml配置文件

   ```java
   <?xml version="1.0" encoding="UTF-8"?>
   <!--日志级别以及优先级排序: OFF > FATAL > ERROR > WARN > INFO > DEBUG > TRACE > ALL -->
   <!--Configuration后面的status用于设置log4j2自身内部的信息输出，可以不设置，当设置成trace时，可以看到log4j2内部各种详细输出-->
   <configuration status="INFO">
       <!--先定义所有的appender-->
       <appenders>
           <!--输出日志信息到控制台-->
           <console name="Console" target="SYSTEM_OUT">
               <!--控制日志输出的格式-->
               <PatternLayout pattern="%d{yyyy-MM-dd HH:mm:ss.SSS} [%t] %-5level %logger{36} - %msg%n"/>
       </console>
       </appenders>
       <!--然后定义logger，只有定义了logger并引入的appender，appender才会生效-->
       <!--root：用于指定项目的根日志，如果没有单独指定Logger，则会使用root作为默认的日志输出-->
       <loggers>
           <root level="info">
               <appender-ref ref="Console"/>
           </root>
       </loggers>
   </configuration>
   ```

3. Spring5框架核心容器支持@Nullable注解

   (1) @Nullable注解可以使用在方法上面，属性上面，参数上面，表示方法返回可以为空，属性值可以为空，参数值可以为空

   (2) 注解用在方法上面，方法返回值可以为空

   ![image-20211012165555705](C:\Users\江流\AppData\Roaming\Typora\typora-user-images\image-20211012165555705.png)

   (3) 注解使用在方法参数里面，方法参数可以为空

   ![image-20211012165619276](C:\Users\江流\AppData\Roaming\Typora\typora-user-images\image-20211012165619276.png)

   (4) 注解使用在属性说明，属性值可以为空

   ![image-20211012170120905](C:\Users\江流\AppData\Roaming\Typora\typora-user-images\image-20211012170120905.png)

4. Spring5核心容器支持函数式风格GenericApplicationContext

   ```java
   //函数式风格创建对象，交给spring进行管理
   @Test
   public void testAccount3(){
      //1 创建GenericApplicationContext对象
       GenericApplicationContext context = new GenericApplicationContext();
       //2 调用context的方法对象注册
       context.refresh(); //清空内容
       context.registerBean("user1",User.class,() -> new User());
       //3 获取在spring注册对象
       //User user = (User)context.getBean("com.spring5.test.User");
       User user = (User)context.getBean("user1");
       System.out.println(user);
   
   }
   ```

5. Spring5支持整合JUnit5

   > JUnit4为了简化测试代码用注解的方式替代以下代码
   >
   > ```java
   > ApplicationContext context =
   >      new ClassPathXmlApplicationContext("bean2.xml");
   > UserService userService=context.getBean("userService", UserService.class);
   > ```

   （1）整合JUnit4

   第一步：引入Spring相关针对测试依赖

   ![image-20211013194352797](C:\Users\江流\AppData\Roaming\Typora\typora-user-images\image-20211013194352797.png)

   ![image-20211013200129933](C:\Users\江流\AppData\Roaming\Typora\typora-user-images\image-20211013200129933.png)

   第二步：创建测试类，使用注解方式完成

   ```java
   @RunWith(SpringJUnit4ClassRunner.class) //单元测试框架
   @ContextConfiguration("classpath:bean1.xml") //加载配置文件
   public class JTest4 {
       @Autowired
       private UserService userService;
   
       @Test
       public void test1(){
           userService.accountMoney();
       }
   }
   ```

   （2）Spring5整合JUnit5

   第一步：引入JUnit5的jar包

   ![image-20211013201220618](C:\Users\江流\AppData\Roaming\Typora\typora-user-images\image-20211013201220618.png)

   第二步：创建测试类，使用注解方式完成

   ```java
   @ExtendWith(SpringExtension.class)
   @ContextConfiguration("classpath:bean1.xml")
   public class JTest5 {
       @Autowired
       private UserService userService;
   
       @Test
       public void test1(){
           userService.accountMoney();
       }
   }
   ```

   （3）使用一个复合注解替代上面两个注解完成整合

   ```java
   @SpringJUnitConfig(locations = "classpath:bean1.xml")
   public class JTest5 {
       @Autowired
       private UserService userService;
   
       @Test
       public void test1(){
           userService.accountMoney();
       }
   }
   ```

##### SpringWebflux

1. SpringWebflux介绍：

   ![image-20211013202630000](C:\Users\江流\AppData\Roaming\Typora\typora-user-images\image-20211013202630000.png)

2. 响应式编程

   

3. Webflux执行流程和核心API

   

4. SpringWebflux（基于注解编程模型）

   

5. SpringWebflux（基于函数式编程模型）

