## spring是什么，或者说为什么使用spring?

1) 支持ioc控制反转，将对象创建交给容器管理。方便解耦
2) 支持aop面向切面编程，降低模块耦合度。封装公共模块，如事务、日志等等模块。
3) 对很多模块进行了集合和封装，也提过针对其他框架的支持，方便开发，增加效率。

# spring有哪些模块？

1) 核心模块有spring-core,beans,context,expression。主要提供了ioc依赖注入的支持
2) aop:aspects,aop,instrument提供面向切面编程的支持                   

3) web:web功能支持、mvc实现、websocket支持

4) data Access：提供了数据库访问支持、事务以及orm框架的支持

# spring 常用的注入方式有哪些?

1) setter注入 propertes

2) 构造函数注入 construct-arg
3) 基于注解的注入 @Component,Controller,Repository,service。描述依赖关系的注解则是@Resource,@Autowried

# spring bean线程安全吗？

当spring中bean默认为单例模式时，多个线程操作同一对象时，线程不安全的。

# spring bean作用域？

1) singleton单例
2) prototype每次获取新的实例
3) request(每次http请求产生一个新的bean)
4) session每一次新的session的http请求产生新的
5) websocket:每一次websocket会话产生新的bean

# spring 自动装配 bean 有哪些方式？

1) default/no 依靠ref属性指定对应bean
2) byName 按名字匹配
3) byType 按类型匹配
4) @AutoWried 先按byType,多种则按byName，为spring提供的注解.
5) @Resource 先按name。使用name属性指定bean


# 解释一下什么是控制反转ioc?

算是一种设计思想，普通实例对象都是new一个对象，如果类A中有成员变量类b，依赖于b；按照这种方式我们每次使用类a都要明确a的所有依赖关系，然后根据依赖关系一个个进行实例化，最后才能组装我们需要的对象a。这种方式比较复杂。spring就实现了由ioc容器来管理这种依赖关系,我们可以通过配置或者注解来说明这种依赖关系，然后在之后需要使用，直接引用即可。
DI依赖注入时ioc的一种实现方式。


# 解释下什么是aop？

aop也就是面向切面编程，我的理解是通过切入点的表达式去匹配方法执行过程中的某一个连接点，然后在方法执行之前或者之后去实现一些公共的逻辑，比如说事务和日志、权限这一类的功能).也就是减少了重复代码，降低模块之间的耦合度。公共校验一类的如果写在每一个方法中，重复太多切不易调整。
spring aop基于动态代理实现的，如果代理的对象实现了某个接口则使用JDK proxy,否则使用Cglib生成代理对象的子类来进行代理

# spring 事务实现方式有哪些？

编程式事务和声明式事务，编程式事务就是在代码块中使用事务管理器手动管理事务；声明式事务就是通过xml配置或者基于@Transactional注解来实现

# 说一下 spring 的事务隔离？

1) 默认使用数据库默认的隔离级别
2) 读未提交 读其他事务还未提交的数据
3) 读可提交 
4) 可重复读 首次读取一条记录时，就对该记录加锁。然后再读，都是同一条记录。但对insert无效，所以仍然会导致幻读。
5) 串行化


# springMVC运行流程？

1) http请求请求dispacherServlet
2) servlet调用HandlerMapping ，根据url查对应的controller，包括拦截器一起封装
3) 调用HandlerAdapter执行handler
4) 处理完请求后，返回一个modelAndView,model这里是数据模型，view就是视图。返回的是一个jsp路径。
5) servlet根据这个路径去找到实际的视图页面，并把数据模型传给这个视图，进行渲染。
6) 最后将这个页面返回给浏览器
