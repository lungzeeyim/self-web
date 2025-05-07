---
title: SpringBoot QA
tags:
- job
---

https://www.bilibili.com/opus/835823004023783475/?from=readlist

1. Spring Boot 开发 用 微服务 框架，
    - 简化 Spring 配置 和 部署。
1. SpringBoot 核心特性: 
    - 自动配置，自动起步依赖，自动化部署。
1. 什么是起步依赖（Starter Dependency）？
    - 起步依赖 是 一组 已经配置好 的 依赖关系，可以 简化项目 依赖管理。
1. Spring Boot如何处理版本冲突？
    - Spring Boot 用 依赖管理 处理 版本冲突
    - 依赖版本 来解决冲突。
1. Spring Boot如何加载外部配置文件？
    - Spring Boot使用 @PropertySource注解 
    - 或 application.properties/application.yml 加载外部配置文件。
1. Spring Boot中如何实现拦截器（Interceptor）？
    - 使用 实现 HandlerInterceptor接口 类 来 创建拦截器
1. Spring Boot中如何处理异常？
    - @ControllerAdvice注解 来处理异常
    - @ExceptionHandler注解 来处理异常
1. Spring Boot 如何 实现 Bean 的 作用域？
    - 可以使用 @Scope注解 来 指定 Bean的 作用域
    - 如singleton、prototype等
1. Spring Boot如何实现缓存？
    - Spring Boot 可以 通过 使用 @EnableCaching注解 来开启缓存，并 依赖缓存实现（如Ehcache、Redis）。
1. Spring Boot 如何 集成 持久化 框架（如Hibernate、MyBatis）？
    - Spring Boot可以 通过 使用 对应的 起步依赖 和 配置 来 集成 持久化框架。
1. Spring Boot如何处理跨域请求？
    - 可以使用 @CrossOrigin注解
        ```java
        @RestController
        @RequestMapping("/api")
        @CrossOrigin(origins = "http://localhost:8080") // 类级别
        public class MyController {
            
            @GetMapping("/items")
            @CrossOrigin(origins = "http://localhost:8080") // 方法级别(可覆盖类级别配置)
            public List<Item> getItems() {
                // ...
            }
        }
        ```
    - or 使用 Filter 方式 `public void doFilter(ServletRequest req, ServletResponse res, FilterChain chain) throws IOException, ServletException {}`
    - 在 application.yml 中
        ```java
        spring:
          mvc:
            cors:
              allowed-origins: "http://localhost:8080,https://example.com"
              allowed-methods: "GET,POST,PUT,DELETE"
              allowed-headers: "*"
              allow-credentials: true
              max-age: 3600
        ```
1. 如何在Spring Boot中 使用 定时任务？
    - 可以使用 @Scheduled注解 来创建定时任务。
1. Spring Boot 如何 实现 请求参数校验？
    - 可以使用 注解 校验框架（如Hibernate Validator）
    - 和相关注解（如@Valid）来实现请求参数校验。
1.  Spring Boot 实现 文件 上传？
    - 可以 使用 MultipartFile类 和
    - 注解 @RequestParam 来实现文件上传
1. Spring Boot 如何处理 表单提交？
    - 使用 @RequestBody注解 
    - 和 注解（如@PostMapping）来处理表单提交。
        ```java
        @PostMapping("/users")
        public ResponseEntity<User> createUser(@RequestBody User user) {
            // 处理接收到的user对象
            User savedUser = userService.save(user);
            return ResponseEntity.ok(savedUser);
        }
        ```
1. Spring Boot如何实现跨服务通信？
    - 使用 RestTemplate / Feign 来 实现 跨服务 通信。
1. Spring Boot如何实现安全认证和授权？
    - 可以使用 Spring Security 实现 安全认证 和 授权。
1. Spring Boot中的Bean生命周期是怎样的？
    - Bean 生命周期 包括
        - 实例化
        - 属性赋值
        - 初始化方法调用
        - 销毁方法调用。
1. 如何在Spring Boot中配置日志？
    - 可以使用日志框架（如Log4j2、Logback）
    - 和配置文件（如logback.xml）来配置日志。
1. Spring Boot 如何实现异步编程？
    - @Async
      - 标记 __方法__ 为异步执行。被标注的方法会在调用时立即返回
      - 实际执行会在单独的线程中进行
      - 优化用户体验（避免阻塞主线程）/ 实现后台任务处理
      - Spring 管理的 Bean 中使用（@Component, @Service 等）
      - 自调用（同一个类中的方法调用）@Async 方法不会异步执行？
      - @Transactional和@Async一起使用时，事务可能不会按预期工作
      - @Async 返回类型
        - void：不关心执行结果
        - CompletableFuture（推荐）：Java 8+更强大的异步处理 
            ```java
            @Async
            public CompletableFuture<String> fetchData() {
                return CompletableFuture.completedFuture("数据");
            }
            ```
    - 线程池来实现异步编程。
      - 自定义线程池
        - 实现AsyncConfigurer接口
        - 定义Bean `TaskExecutor`
          - 使用指定线程池: `@Bean(name = "taskExecutor")` 
    - 使用@Async的实际业务场景
      - 发送通知
      - 日志记录
      - 文件处理
      - 第三方API调用
      - 定时任务的后台处理(eg. 同步数据到其他系统)
1. Spring Boot 如何 集成 消息队列（如RabbitMQ）？
    - 可以 用 对应的 起步依赖
    - 配置来集成消息队列。
1. 如何在Spring Boot中实现RESTful API？
    - 可以使用 @RestController 注解 来实现RESTful API
    - 和相关注解
      - @GetMapping
      - @PostMapping
1. Spring Boot 如何实现WebSocket通信？
    - 可以使用注解（如@ServerEndpoint）
    - 和WebSocket相关的类（如Session）来实现WebSocket通信。
1. Spring Boot 如何实现 `连接池`？
    - 可以使用连接池技术（如HikariCP、Tomcat JDBC）来实现连接池。
1. Spring Boot 如何集成 缓存服务器（如Redis）？
    - 可以 用 对应的 起步依赖 和 配置 来集成 缓存服务器。
1. Spring Boot中如何 实现 数据库 事务管理？
    - 可以使用注解（如@Transactional）
    - 和事务管理器（如JpaTransactionManager）来实现数据库事务管理。
1. Spring Boot如何配置连接池？
    - 在Spring Boot中，可以使用配置文件（如application.properties/application.yml）来配置连接池的属性。
1. Spring Boot中如何实现RESTful接口版本控制？
    - 可以通过在 UR L或 请求头 中 添加 版本信息的 方式 来实现 RESTful接口版本控制。
1. Spring Boot如何实现热部署？
    - Spring Boot可以使用插件（如Spring Loaded、DevTools）来实现热部署。
1. Spring Boot如何实现请求重定向？
    - 在Spring Boot中，可以使用重定向视图（如RedirectView）
    - 或相关注解（如@ResponseStatus）来实现请求重定向。
1. Spring Boot如何配置跨域访问？
    - 可以通过配置类（如CorsConfiguration）
    - 或注解（如@CrossOrigin）来配置跨域访问。
1. Spring Boot 如何 实现 动态数据源 切换？
    - Spring Boot可以使用注解（如@Primary、@Qualifier、@ConfigurationProperties）
    - 和配置类（如DataSourceConfig）来实现动态数据源切换。
1. Spring Boot中如何使用AOP？
    - 可以使用自定义注解和切面类（如@Aspect）来实现AOP。
1. Spring Boot如何实现文件下载？
    - 在Spring Boot中，可以使用ResponseEntity
    - 和相关类（如InputStreamResource）来实现文件下载。
1. Spring Boot 如何 实现 分页查询？
    - 可以使用分页插件（如PageHelper、Spring Data JPA）来实现分页查询。
1. Spring Boot如何配置日志打印格式？
    - 在Spring Boot中，可以使用配置文件（如logback.xml）或配置类（如LoggingConfig）来配置日志打印格式。
1. Spring Boot如何实现JWT（JSON Web Token）授权？
    - 注解（如@JwtToken）来实现JWT授权。
    - 令牌存储：客户端通常将 JWT 存储在 localStorage 或 cookie 中
    - 敏感操作：对于敏感操作，即使有有效 JWT 也应要求重新验证密码
    - 通常配合拦截器或 AOP 实现，基本流程：
      - 检查方法或类上是否有 @JwtToken 注解
      - 从 HTTP 请求头(通常是 Authorization 头)中获取 JWT
      - 验证 JWT 的签名和有效期
      - 检查 JWT 中的角色/权限是否符合注解要求
      ```java
      @JwtToken(
        roles = {"ADMIN"}  // 需要的角色
        permissions={"3"}  // 需要的权限
      )
      ```
1. Spring Boot 如何 实现 分布式系统的 `配置管理`
    - 集中式配置管理：
      - Spring Boot 可以通过 集中式的 配置管理工具（如Spring Cloud Config、Zookeeper等）来管理应用程序的配置。
      - 配置信息 存储在 配置服务器上，应用程序 可以动态获取 所需的配置信息，而无需重新部署。
    - 配置文件：
      - 支持 多种类型的 配置文件，如properties、yaml等
      - 配置文件中的 属性值 可以在应用程序中 通过 @Value注解 或 @ConfigurationProperties注解 进行注入使用。
    - 外部化配置：Spring Boot 支持 应用程序的 配置外部化，
      - 可以将配置信息存储在外部的属性源（如环境变量、系统属性、命令行参数、特定的配置文件等）中，
      - 使得配置可以在不同环境中灵活切换。
    - 动态刷新配置：
      - 可以通过Spring Cloud Config 或Actuator 的刷新功能，实现配置的动态刷新。
      - 当配置发生变化时，应用程序可以刷新配置，而无需重新启动应用程序。
    - 基于消息的配置：
      - Spring Boot可以与消息队列（如Kafka、RabbitMQ等）集成，
      - 将 配置信息 作为消息 进行传递。应用程序 可以订阅配置消息，并在 收到消息时 对配置进行更新。
    - Spring Cloud Config：
      - Spring Cloud Config 是Spring提供的分布式配置管理工具，它使用Git或其他后端存储来管理应用程序的配置文件
      - 并提供 RESTful API 供应用程序 获取配置信息。
1. 描述springboot核心实现原理？
    - Spring Boot的核心实现原理可以从以下几个方面来解释：
      - 自动配置（Auto Configuration）：Spring Boot利用条件化配置和约定优于配置的原则，通过扫描项目中的依赖、类等信息，自动配置应用程序的各个组件和特性。自动配置是Spring Boot的一大特点，它减少了开发人员的配置工作，提高了开发效率。
        - 起步依赖（Starter Dependency）：Spring Boot的起步依赖是预先定义好的一组已经配置好的依赖关系，可以简化项目的依赖管理。起步依赖中包含了常用的依赖，例如数据库驱动、web服务等，这样开发人员只需引入相应的起步依赖，即可获得所需功能的依赖。
        - 内嵌容器（Embedded Container）：Spring Boot通过内嵌容器（如Tomcat、Jetty）来运行应用程序，这样开发人员不再需要手动部署和配置外部容器。Spring Boot会自动根据项目的依赖和配置来选择合适的内嵌容器，并提供相应的默认配置。
        - 配置文件加载：Spring Boot支持多种类型的配置文件，如properties、yaml等。Spring Boot会在启动过程中自动加载并解析这些配置文件，然后将解析后的配置信息应用到应用程序中。
        - 条件化装配（Conditional Assembly）：Spring Boot可以根据条件自动装配bean。它通过@Conditional注解和Condition接口来判断是否满足某个条件，从而决定是否创建、注册某个bean。
        - 约定优于配置（Convention over Configuration）：Spring Boot遵循约定优于配置的原则，它通过默认的约定来减少代码的配置量。例如，Spring Boot会根据项目的结构和命名约定自动扫描组件，而不需要显式配置。
        - 总体来说，Spring Boot通过自动配置、起步依赖、内嵌容器、配置文件加载、条件化装配和约定优于配置等机制，简化了Spring应用程序的开发和部署过程，提高了开发效率和便利性。

1. springboot常用注解有哪些？
  - @SpringBootApplication：
    - 标记主应用程序类，表示这是一个Spring Boot应用程序的入口点。
    - 它包含了
      - @ComponentScan
      - @EnableAutoConfiguration
      - @Configuration三个注解。
  - @RestController
    - 用于标记RESTful控制器 __类__，
    - @Controller 和 @ResponseBody 的组合注解
  - @RequestMapping：
    - HTTP请求路径 映射到 控制器 方法 或 类 上	
        ```java
        @RestController
        @RequestMapping("/api")  // 类级别：统一前缀
        public class UserController {
            
            @RequestMapping(value = "/users", method = RequestMethod.GET)  // 方法级别
            public List<User> getUsers() {
            return userService.getAllUsers();
            }
        }
        ```
  - @Autowired：
    - 用于标记需要自动注入的依赖对象。	
    - 自动装配 Bean 的依赖关系
    - 注入
      - 构造方法注入
      - Setter 方法注入
    - 装配
      - 多个同类型的 Bean，会抛出 NoUniqueBeanDefinitionException
      - 结合 @Qualifier 指定 Bean 名称
        ```java
        @Autowired
        @Qualifier("userRepositoryImpl")  // 指定具体实现类
        private UserRepository userRepository;
        ```
      - 使用 @Primary 标记优先注入的 Bean
        ```java
        @Repository
        @Primary
        public class JpaUserRepository implements UserRepository {}
        ```
    - 工作原理：
      - Spring 容器启动时，会扫描所有 @Component（或其派生注解如 @Service、@Repository）标记的类，创建 Bean 并管理其生命周期。@Autowired 通过以下步骤完成注入：
        - 查找匹配类型的 Bean。
        - 如果找到多个候选 Bean，按 @Qualifier 或 Bean 名称进一步筛选。
        - 通过反射或构造方法完成依赖注入。
      - 最佳实践：
        - 推荐构造方法注入：
        - 保证依赖不可变（final 字段），避免循环依赖问题。
      - 处理多实现类：
        - 使用 @Qualifier 或 @Primary 明确指定 Bean。
  - @Value：用于注入配置文件中的属性值。可直接将属性值注入到Java类中。
  - `@Component`：用于标记通用组件类，表示这个类是一个受Spring管理的组件Bean。
  - @Configuration：用于标记配置类，表示这个类是一个Bean配置类，包含配置信息的方法。
  - @EnableAutoConfiguration：
    - 用于启用自动配置功能
    - 根据当前的 classpath 里有哪些类、配置文件里的内容，自动配置 Spring 应用所需要的 Bean
  - @Conditional：
    - 只有当某个条件满足时，这个类/方法的 Bean 才会生效
		- OnProperty, OnClass, OnBean
  - @EnableCaching：
    - 开启 缓存功能。在 方法 或 类 上 使用。
    - 开启之后，从而 提高性能、减少 数据库 访问次数
      ```java
      @Service
      public class UserService {

          @Cacheable(value = "userCache", key = "#userId")
          public User getUserById(Long userId) {
        System.out.println("Fetching from DB...");
        return userRepository.findById(userId).orElse(null);
          }
      }
      ```
  - @Transactional：用于标记事务管理的方法或类。指示方法或类中的操作需要在事务中执行。
    - 用于 保证 数据库 操作 要么 全部成功，要么 全部失败 回滚（rollback），防止 出现 数据 不一致的情况。
    - 只能作用于 public 方法
    - 只在 Bean 上生效
      ```java
      @Transactional(
          propagation = Propagation.REQUIRED,  // propagation 事务延续 <- 有事务就加入，没有就创建
          isolation = Isolation.READ_COMMITTED, // 读 已提交
          rollbackFor = Exception.class,
          readOnly = true,
          timeout = 20
      )
      ```
  - @EnableScheduling：用于 定时 任务调 度功能。标记类或方法 






