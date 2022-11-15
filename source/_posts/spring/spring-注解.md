---
title: spring 注解
categories: spring
comments: true
highlight_shrink: false
cover: /img/post/0c0f3f16880511ebb6edd017c2d2eca2.jpg
abbrlink: cb82
date: 2022-11-10 00:00:00
updated:
---

## spring 注解

### @Controller
用于标注控制层组件

### @Service
用于标注业务层组件

### @Repository
用于标注数据访问组件，即 DAO 组件

### @Component
泛指组件，当组件不好归类的时候，我们可以使用这个注解进行标注

### @Configuration
```java
@Configuration("name") // 表示这是一个配置信息类，可以给这个配置类也起一个名称
@ComponentScan("com.yylemon") // 类似于 xml 中的 <context:component-scan base-package="com.yylemon"/>
@PropertySource("classpath:jdbc.properties") // 加载 properties 文件，多文件要用数组格式，不允许使用通配符 *
public class Config {

    @Autowired // 自动注入，如果容器中有多个符合的 bean 时，需要进一步明确
    @Qualifier("Compent") // 进一步指明注入 bean 名称为 Compent 的 bean
    private Compent compent;

    @Bean("dataSource") // 第三方 bean，先创建方法，返回 bean 对象，加上 bean 注解，名字可加可不加
    public DataSource dataSource(){
        DruidDataSource ds = new DruidDataSource();
        ds.setDriverClassName("com.mysql.jdbc.Driver");
        ds.setUrl("jdbc://mysql://localhost:3306/database");
        ds.setUsername("root");
        ds.password("root");
        return ds;
    }   
}
```

### @Scope
```java
@Scope // 单例
@Scope("singleton") // 单例
@Scope("prototype") // 多例
```

### @PostConstruct
生命周期，构造方法后执行

### @PreDestroy
生命周期，彻底销毁前执行
销毁需要关闭容器或者注册钩子关闭
```java
// appletContext 需要使用父类
appletContext.registerShutdownHook(); // 注册钩子关闭
appletContext.close(); // close 关闭容器
```

### @Autowired
在默认情况下使用 @Autowired 注释进行自动注入时，Spring 容器中匹配的候选 Bean 数目必须有且仅有一个。
当找不到一个匹配的 Bean 时，Spring 容器将抛出 BeanCreationException 异常，并指出必须至少拥有一个匹配的 Bean。 
当不能确定 Spring 容器中一定拥有某个类的 Bean 时，可以在需要自动注入该类 Bean 的地方可以使用 @Autowired(required = false)，这等于告诉 Spring: 在找不到匹配 Bean 时也不报错。

### @Qualifier
配合 @Autowired 使用，当出现多个相同类型时，它可以缩小范围，指定注入对象的 id。

### @Value
使用它可以简单类型注入，或者读取配置文件里的值
```java
@Value("${name}")
```

### @ComponentScan
配合 @Configuration，注解会告知 Spring 扫描指定的包来初始化 Spring 容器

### @Import
导入配置类，跟 @ComponentScan 类似，但是它可以精准定位
```java
@Import({JdbcConfig.class}) // 数组形式
```

### @RunWith
spring 整合 junit
```java
//设置类运行器
@RunWith(SpringJUnit4ClassRunner.class)
//设置Spring环境对应的配置类
@ContextConfiguration(classes = SpringConfig.class)
public class UserServiceTest {
    @Autowired
    private UserService userService;

    @Test
    public void testFindById(){
        System.out.println(userService.findById(1));
    }
}
```

### @Aspect
```java
@Component
@Aspect
public class MyAdvice {
    //切入点表达式：
//    @Pointcut("execution(void com.itheima.dao.BookDao.update())")
//    @Pointcut("execution(void com.itheima.dao.impl.BookDaoImpl.update())")
//    @Pointcut("execution(* com.itheima.dao.impl.BookDaoImpl.update(*))")    //no
//    @Pointcut("execution(void com.*.*.*.update())")
//    @Pointcut("execution(* *..*(..))")
//    @Pointcut("execution(* *..*e(..))")
//    @Pointcut("execution(void com..*())")
//    @Pointcut("execution(* com.itheima.*.*Service.find*(..))")
    //执行com.itheima包下的任意包下的名称以Service结尾的类或接口中的save方法，参数任意，返回值任意
    @Pointcut("execution(* com.itheima.*.*Service.save(..))")
    private void pt(){}

    @Before("pt()")
    public void method(){
        System.out.println(System.currentTimeMillis());
    }
}
```
```java
@Configuration
@ComponentScan("com.itheima")
@EnableAspectJAutoProxy // 开启注解 aop
public class SpringConfig {
}
```
