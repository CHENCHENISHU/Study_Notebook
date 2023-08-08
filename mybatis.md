# MyBatis环境搭建

pom.xml中引入MyBatis核心依赖

```xml
<?xml version="1.0" encoding="UTF-8"?>

<project xmlns="http://maven.apache.org/POM/4.0.0"     
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation=
         "http://maven.apache.org/POM/4.0.0 
          http://maven.apache.org/xsd/maven-4.0.0.xsd">

    <modelVersion>4.0.0</modelVersion>

    <!--项目配置-->
    <groupId>com.qf</groupId>
    <artifactId>hello-mybatis</artifactId>
    <version>1.0-SNAPSHOT</version>

    <!--依赖-->
    <dependencies>
        <!--MyBatis核心依赖-->
        <dependency>
            <groupId>org.mybatis</groupId>
            <artifactId>mybatis</artifactId>
            <version>3.4.6</version>
        </dependency>

        <!--MySql驱动依赖-->
      <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <version>8.0.21</version>
        </dependency>
      </dependencies>
</project>
```

## 创建MyBatis配置文件

> 在resources目录创建mybatis-config.xml

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
    "http://mybatis.org/dtd/mybatis-3-config.dtd">

<!--MyBatis配置-->
<configuration>
    <!--JDBC环境配置、选中默认环境-->
    <environments default="MySqlDB">
        <!--MySql数据库环境配置-->
        <environment id="MySqlDB">
            <!--事务管理-->
            <transactionManager type="JDBC"/>
            <!--连接池-->
       <dataSource type="org.apache.ibatis.datasource.pooled.PooledDataSourceFactory">
                <property name="driver" value="com.mysql.cj.jdbc.Driver"/>
                <!-- &转义& -->
                <property name="url" value="jdbc:mysql://localhost:3306/ssm?characterEncoding=utf8&useSSL=false&serverTimezone=Asia/Shanghai&rewriteBatchedStatements=true"/>
                <property name="username" value="root"/>
                <property name="password" value="123456"/>
            </dataSource>
        </environment>
    </environments>

    <!--Mapper注册-->
    <mappers>
        <!--注册Mapper文件的所在位置-->
        <mapper resource="xxxMapper.xml"/>
    </mappers>
</configuration>
```

注意：mapper.xml默认建议存放在resources中,路径不能以/开头



## MyBatis开发步骤

### 建表

```sql
create table t_users(
  id int primary key auto_increment,
  name varchar(50),
  password varchar(50),
  sex varchar(1),
  birthday datetime,
  registTime datetime
)default charset = utf8;
```

### 定义实体类

```java
public class User {
    private Integer id;
    private String name;
    private String password;
    private String sex;
      private Date birthday;
      private Date registTime;

    //无参构造（必备构造二选一）
    public User() {}

    //全参构造（必备构造二选一）
    public User(Integer id, String name, String password, String sex, Date birthday, Date registTime) {
        this.id = id;
        this.name = name;
        this.password = password;
        this.sex = sex;
          this.birthday = birthday;
          this.registTime = registTime;
    }

    //Getters And Setters
}
```

### 定义Mapper接口

> 创建Mapper包，然后创建UserMapper接口文件，并添加所需方法

```java
public interface UserDao {
    public User selectUserById(Integer id);
}
```

### 编写Mapper.xml

> 在resources目录中创建Mapper.xml文件

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
    "http://mybatis.org/dtd/mybatis-3-mapper.dtd">

<!--namespace = 所需实现的接口全限定名-->
<mapper namespace="com.qf.mybatis.mapper.UserDao">
    <!--id = 所需重写的接口抽象方法，resultType = 查询后所需返回的对象类型-->
    <select id="selectUserById" resultType="com.qf.mybatis.part1.basic.User">
        <!--#{arg0} = 方法的第一个形参-->
          SELECT * FROM t_users WHERE id = #{arg0}
    </select>
</mapper>
```

### 注册Mapper

> 将Mapper.xml注册到mybatis-config.xml中

```xml
<!--Mapper文件注册位置-->
<mappers>
    <!--注册Mapper文件-->
    <mapper resource="mapper/UserDaoMapper.xml"/>
</mappers>
```

### 测试

```java
public class HelloMyBatis {

    @Test
    public void test1() throws IOException {
        //1.获得读取MyBatis配置文件的流对象
        InputStream is = Resources.getResourceAsStream("mybatis-config.xml");

        //2.构建SqlSession连接对象的工厂
        SqlSessionFactory factory = new SqlSessionFactoryBuilder().build(is);

        //3.通过工厂获得连接对象
        SqlSession sqlSession = factory.openSession();

        //4.通过连接对象获得接口实现类对象  
        UserDao userDao = sqlSession.getMapper(UserDao.class);

        //5.调用接口中的方法
        System.out.println(userDao.selectUserById(1));
    }
}
```

## 细节补充

### 解决mapper.xml存放在resources以外路径中的读取问题

> 在pom.xml文件最后追加< build >标签，以便可以将xml文件复制到classes中，并在程序运行时正确读取。

```xml
```xml
<build>
        <!-- 如果不添加此节点src/main/java目录下的所有配置文件都会被漏掉。 -->
        <resources>
            <resource>
                <directory>src/main/java</directory>
                <includes>
                    <include>**/*.xml</include>
                </includes>
            </resource>
            <resource>
                <directory>src/main/resources</directory>
                <includes>
                    <include>**/*.xml</include>
                    <include>**/*.properties</include>
                    <include>**/*.ini</include>
                </includes>
            </resource>
        </resources>
    </build>
```

### properties配置文件

> 对于mybatis-config.xml的核心配置中，如果存在需要频繁改动的数据内容，可以提取到properties中。

```
#jdbc.properties
jdbc.driver=com.mysql.jdbc.Driver
jdbc.url=jdbc:mysql://localhost:3306/example?useUnicode=true&characterEncpding=utf8
jdbc.username=root
jdbc.password=123456
```

> 修改mybatis-config.xml。

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">

<configuration>
    <!--添加properties配置文件路径(外部配置、动态替换)-->
    <properties resource="jdbc.properties" />

    <environments default="MySqlDB">
        <environment id="MySqlDB">
            <transactionManager type="JDBC"/>
            <dataSource type="POOLED">
                <!--使用$ + 占位符-->
                <property name="driver" value="${driver}"/>
                <property name="url" value="${url}"/>
                <property name="username" value="${username}"/>
                <property name="password" value="${password}"/>
            </dataSource>
        </environment>
    </environments>

    <mappers>
        <mapper resource="mapper/UserDaoMapper.xml" />
    </mappers>
</configuration>
```

### 类型别名（了解）

> 为实体类定义别名，提高书写效率。

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">

<configuration>
    <properties ... />

    <!--定义别名二选一-->
    <typeAliases>
        <!--定义类的别名-->
        <typeAlias type="com.qf.mybatis.mapper.User" alias="user" />

        <!--自动扫描包，将原类名作为别名-->
        <package name="com.qf.mybatis.part1.basic" />
    </typeAliases>

      ...
</configuration>
```

### 创建log4j配置文件

> 添加log4j依赖

```xml
<!-- log4j日志依赖 https://mvnrepository.com/artifact/log4j/log4j -->
<dependency>
        <groupId>log4j</groupId>
        <artifactId>log4j</artifactId>
        <version>1.2.17</version>
</dependency>
```

> 创建并配置log4j.properties

```
```xml
# Global logging configuration
log4j.rootLogger=DEBUG, stdout
# MyBatis logging configuration...
log4j.logger.org.mybatis.example.BlogMapper=TRACE
# Console output...
log4j.appender.stdout=org.apache.log4j.ConsoleAppender
log4j.appender.stdout.layout=org.apache.log4j.PatternLayout
log4j.appender.stdout.layout.ConversionPattern=%5p [%t] - %m%n
```

```

| 级别        | 描述                              |
| --------- | ------------------------------- |
| ALL LEVEL | 打开所有所有日志记录开关；最低等级的，用于打开所有日志记录   |
| DEBUG     | 输入调试信息；指出细粒度信息事件对调试应用程序是非常有帮助的  |
| INFO      | 输出提示信息；消息在粗粒度级别上突出强调应用程序的运行过程   |
| WARN      | 输出警告信息；表明会出现潜在错误的情形             |
| ERROR     | 输出错误信息；指出虽然发生错误事件，但仍然不影响系统的继续运行 |
| FATAL     | 输出致命错误；指出每个严重错误事件将导致应用程序的退出。    |
| OFF LEVEL | 关闭所有日志记录开关；最高等级的，用于关闭所有日志记录     |

## MyBatis的CRUD操作

### 查询

>  标签：< select id="" resultType="" >

#### 序号参数绑定

```java
public interface UserDao {
        //使用原生参数绑定
    public User selectUserByIdAndPwd(Integer id , String pwd);
}
```

```xml
<select id="selectUserByIdAndPwd" resultType="user">
    SELECT * FROM t_users
    WHERE id = #{arg0} AND password = #{arg1} <!--arg0 arg1 arg2 ...-->
</select>

<select id="selectUserByIdAndPwd" resultType="user">
    SELECT * FROM t_users
    WHERE id = #{param1} AND password = #{param2} <!--param1 param2 param3 ...-->
</select>

<select id="selectUserByIdAndPwd" resultType="user">
    SELECT * FROM t_users
    WHERE id = #{id} AND password = #{pwd} <!--param1 param2 param3 ...-->
</select>
```

#### 注解参数绑定【推荐】

```java
public interface UserDao {
    //使用MyBatis提供的@Param进行参数绑定
    public User selectUserByIdAndPwd(@Param("id") Integer id , @Param("pwd") String pwd);
}
```

```xml
<select id="selectUserByIdAndPwd" resultType="user">
    SELECT * FROM t_users
    WHERE id = #{id} AND password = #{pwd} <!-- 使用注解值 @Param("pwd") -->
</select>
```

#### Map参数绑定(了解)

```java
public interface UserDao {
    //添加Map进行参数绑定
		public User selectUserByIdAndPwd_map(Map values);
}
```

```java
Map values = new HashMap(); //测试类创建Map
values.put("myId",1); //自定义key，绑定参数
values.put("myPwd","123456");
User user = userDao.selectUserByIdAndPwd_map(values);
```

```xml
<select id="selectUserByIdAndPwd_map" resultType="user">
    SELECT * FROM t_users 
  	WHERE id = #{myId} AND password = #{myPwd} <!-- 通过key获得value -->
</select>
```

#### 对象参数绑定(重点)

```java
public interface UserDao {
    //使用对象属性进行参数绑定
    public User selectUserByUserInfo(User user);
}
```

```xml
<select id="selectUserByUserInfo" resultType="user">
    SELECT * FROM t_users
    WHERE id = #{id} AND password = #{password} <!-- #{id}取User对象的id属性值、#{password}同理 -->
</select>
```

#### 模糊查询

```java
public interface UserDao {
    public List<User> selectUsersByKeyword(@Param("keyword") String keyword);
}
```

```xml
<mapper namespace="com.qf.mybatis.part1.different.UserDao">
    <select id="selectUsersByKeyword" resultType="user">
        SELECT * FROM t_users 
  		WHERE name LIKE concat('%',#{keyword},'%') <!-- 拼接'%' -->
    </select>
</mapper>
```

#### 删除

> 标签：< delete id="" parameterType="" >

```xml
<delete id="deleteUser" parameterType="int">
    DELETE FROM t_users
    WHERE id = #{id} <!--只有一个参数时，#{任意书写}-->
</delete>
```

#### 添加

> 标签：< insert id="" parameterType="" >

```xml
<!--手动主键-->
<insert id="insertUser" parameterType="user">
    INSERT INTO t_users VALUES(#{id},#{name},#{password},#{sex},#{birthday},NULL);
</insert>

<!--自动主键-->
<insert id="insertUser" parameterType="user">
	<!-- 自动增长主键，以下两种方案均可 -->
    INSERT INTO t_users VALUES(#{id},#{name},#{password},#{sex},#{birthday},NULL);
	INSERT INTO t_users VALUES(NULL,#{name},#{password},#{sex},#{birthday},NULL);
</insert>
```

### 主键回填

> 标签：< selectKey id="" parameterType="" order="AFTER|BEFORE">

#### 通过last_insert_id()查询主键

```java
create table t_product(
  id int primary key auto_increment,
  name varchar(50)
)default charset = utf8;
```

```sql
class Product{
    private Integer id;
    private String name;
    //set+get ...
}
```

```xml
<mapper namespace="com.qf.mybatis.part1.basic.ProductDao">
    <insert id="insertProduct" parameterType="product">
        <selectKey keyProperty="id" resultType="int" order="AFTER"> <!-- 插入之后 -->
            SELECT LAST_INSERT_ID() <!-- 适用于整数类型自增主键 -->
        </selectKey>

        INSERT INTO t_product(id,name) VALUES(#{id},#{name})
    </insert>
</mapper>
```

## 通过uuid()查询主键

```sql
create table t_order(
  id varchar(32) primary key, # 字符型主键
  name varchar(50)
)default charset = utf8;
```

```java
class Order{
    private String id;
    private String name;
    //set+get ...
}
```

```xml
<mapper namespace="com.qf.mybatis.part1.basic.OrderDao">
    <insert id="insertOrder" parameterType="order">
        <selectKey keyProperty="id" resultType="String" order="BEFORE"><!-- 插入之前 -->
            SELECT REPLACE(UUID(),'-','') <!-- 适用于字符类型主键 -->
        </selectKey>

        INSERT INTO t_order(id,name) VALUES(#{id},#{name})
    </insert>
</mapper>
```

# MyBatis工具类

## 封装工具类

- Resource：用于获得读取配置文件的IO对象，耗费资源，建议通过IO一次性读取所有所需要的数据。

- SqlSessionFactory：SqlSession工厂类，内存占用多，耗费资源，建议每个应用只创建一个对象。
* SqlSession：相当于Connection，可控制事务，应为线程私有，不被多线程共享。
* 将获得连接、关闭连接、提交事务、回滚事务、获得接口实现类等方法进行封装。

```java
public class MyBatisUtils {

  	//获得SqlSession工厂
    private static SqlSessionFactory factory;

  	//创建ThreadLocal绑定当前线程中的SqlSession对象
    private static final ThreadLocal<SqlSession> tl = new ThreadLocal<SqlSession>();

    static {
        try {
            InputStream is = Resources.getResourceAsStream("mybatis-config.xml");
            factory = new SqlSessionFactoryBuilder().build(is);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    //获得连接（从tl中获得当前线程SqlSession）
    private static SqlSession openSession(){
        SqlSession session = tl.get();
        if(session == null){
            session = factory.openSession();
            tl.set(session);
        }
        return session;
    }

    //释放连接（释放当前线程中的SqlSession）
    private static void closeSession(){
        SqlSession session = tl.get();
        session.close();
        tl.remove();
    }

    //提交事务（提交当前线程中的SqlSession所管理的事务）
    public static void commit(){
        SqlSession session = openSession();
        session.commit();
        closeSession();
    }

    //回滚事务（回滚当前线程中的SqlSession所管理的事务）
    public static void rollback(){
        SqlSession session = openSession();
        session.rollback();
        closeSession();
    }

    //获得接口实现类对象
    public static <T extends Object> T getMapper(Class<T> clazz){
        SqlSession session = openSession();
        return session.getMapper(clazz);
    }
}
```

# 测试工具类

> 调用MyBatisUtils中的封装方法。

```java
@Test
    public void testUtils() {
        try {
            UserMapper userMapper = MyBatisUtils.getMapper(UserMapper.class);
            userMapper.deleteUser(15);
            MyBatisUtils.commit();
        } catch (Exception e) {
            MyBatisUtils.rollback();
            e.printStackTrace();
        }
    }
}
```
```

# ORM映射

## MyBatis自动ORM失效


