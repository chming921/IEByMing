# Spring

## **什么是Spring框架？**

Spring是一种**轻量级开发[框架](https://so.csdn.net/so/search?q=框架&spm=1001.2101.3001.7020)**，旨在**提高开发人员的开发效率**以及**系统的可维护性**。

目的：解决企业[应用开发](https://so.csdn.net/so/search?q=应用开发&spm=1001.2101.3001.7020)的复杂性

范围：任何Java应用

简单来说，Spring是一个**轻量级的[控制反转](https://so.csdn.net/so/search?q=控制反转&spm=1001.2101.3001.7020)**(IoC)和**面向切面(AOP)**的容器框架。

Spring官网列出的Spring的6个特性：核心技术，测试，数据访问，Web支持，继承，语言。

## **列举一些重要的Spring模块**

![img](https://img-blog.csdnimg.cn/20210426130529181.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwMjYyMzcy,size_16,color_FFFFFF,t_70)

Spring Core可以说Spring其他所有的功能都需要依赖该类库。主要**提供[IoC](https://so.csdn.net/so/search?q=IoC&spm=1001.2101.3001.7020)依赖注入功能**

Spring AOP: 提供**面向切面的编程**实现。

Spring JDBC: Java**数据库连接**。

Spring ORM: 用于支持Hibernate等ORM工具。

Spring Web:为**创建Web应用程序提供支持**。

Spring Test:提供了**对Junit测试的支持**。

## 请你说说Spring的核心是什么

**Core**是整个Spring框架的核心模块，其中Core是整个Spring框架的核心模块。Core模块提供了**IoC容器、AOP功能、数据绑定、类型转换**等一系列的基础功能，而这些功能以及其他**模块的功能**都是建立在**IoC和AOP**之上的，所以**IoC和AOP是Spring框架的核心**。

### @RestController和@Controller

**Controller 返回一个页面**

单独**使用@Controller不加@ResponseBody**的话一般都会**返回一个视图**，这个情况属于比较传统的Spring MVC的应用，对应于前后端不分离的情况。

![img](https://img-blog.csdnimg.cn/20210426130533855.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwMjYyMzcy,size_16,color_FFFFFF,t_70)

**RestController返回JSON或XML形式数据**

但**@RestController**只**返回对象**，对象数据直接**以JSON或XML形式写入HTTP响应**(Response)中，这种情况属于RESTFUL WEB服务，这也是目前日常开发所接触的最常用的情况(前后端分离)

**Controller+ResponseBody返回JSON或XML形式数据**

如果想在Spring4之前开发RESTFUL Web服务的话，只需要结合ResponseBody即可。

## @Transaction原理 Spring事务什么时候会失效？

**事务**的**原理**是**AOP**，底层**使用代理类实现**，**aop代理（dglib+jdk）**

1. 发生**自调用**，同一个类中的方法直接内部调用，会导致事务失效。
2. **本类**中**没有事务**的方法**调用**有**事务的方法**事务会失效。(注意是本类)

3. 方法不是public的（**@Transaction只能作用于public**，若**非要不是public**，可以**开启代理模式AspectJ代理模式**）
4. 数据库不支持事务
5. 没有被Spring管理；
6. 事务不会回滚，开发者在代码中手动try...catch了异常

## Spring事务相关

spring事务声明方式：

- **编程式**
- **声明式**：xml配置，注解@Transaction

**Spring管理事务的方式有几种？**

TransactionDefinition接口定义了五个表示隔离级别的常量

DEFAULT：使用数据库默认隔离级别，mysql rr可重复读，oracle rc 读已提交

READ_UNCOMMITTED:读未提交

READ_COMMITTED:读已提交

REPEATABLE-READ:可重复读

SERIALIZABLE:可重复读，可串行化

## 说一说你对Spring容器的了解

Spring主要提供了两种类型的容器：BeanFactory和ApplicationContext。

- **BeanFactory**：是**基础类型的IoC容器**，提供完整的IoC服务支持。如果没有特殊指定，默认采用**延迟初始化策略**。只有当客户端对象**需要访问**容器中的某个对象**的时候**，**才对该对象进行初始化以及依赖注入操作**。所以，相 对来说，容器启动初期速度较快，所需要的资源有限。对于**资源有限，并且功能要求不是很严格的场景**，BeanFactory是比较合适的IoC容器选择。
- **ApplicationContext**：它是在BeanFactory的基础上构建的，是相对比较高级的容器实现，除了拥有BeanFactory的所有支持，ApplicationContext还提供了其他高级特性，比如事件发布、国际化信息支持等。ApplicationContext所管理的对象，在**该类型容器启动之后，默认全部初始化并绑定完成**。所以，相对于BeanFactory来说，**ApplicationContext要求更多的系统资源**，同时，因为在**启动时就完成所有初始化**，容器**启动时间**较之BeanFactory也会**长一些**。在那些**系统资源充足，并且要求更多功能的场景中**，ApplicationContext类型的 容器是比较合适的选择。

## BeanFactory理解

BeanFactory是一个类工厂，与传统类工厂不同的是，BeanFactory是**类的通用工厂**，它可以**创建并管理各种类的对象**。

**BeanFactory**是Spring容器的顶层接口，Spring为BeanFactory提供了多种实现，最常用的是**XmlBeanFactory**。但它在Spring 3.2中已被废弃，建议使用**XmlBeanDefinitionReader**、**DefaultListableBeanFactory**替代。**BeanFactory**最主要的方法就是 **getBean**(String beanName)，该方法**从容器中返回特定名称的Bean。**

## @Autowired和@Resource注解区别

1. **@Autowired**是**Spring**提供的注解，**@Resource**是**JDK**提供的注解。

2. @Autowired是只能**按类型**注入，@Resource默认**按名称**注入，也支持**按类型**注入。

3. @Autowired按类型装配依赖对象，默认情况下它**要求依赖对象必须存在**，如果**允许null**值，可以设置它**required**属性为**false**，如果我们想**使用按名称装配**，可以**结合@Qualifier**注解一起使用。

   @Resource有两个中重要的属性：**name和type**。name属性指定byName，如果没有指定name属性，当注解标注在字段上，即默认取字段的名称作为bean名称寻找依赖对象，当注解标注在属性的setter方法上，即默认取属性名作为bean名称寻找依赖对象。需要注意的是，@Resource如果没有指定name属性，并且**按照默认的名称仍然找不到依赖对象时， @Resource注解会回退到按类型装配。但一旦指定了name属性，就只能按名称装配了。**

简单来说，byName就是变量名去匹配bean的id属性，而byType则是变量类型去匹配bean的class属性

```xml
<bean id="userService" class="com.test.UserServiceImpl">
</bean> 
```

```java
@Autowired
private UserService userService;
```

此处**byName**就是拿**变量名userService**去匹配IOC容器的iduserService，匹配成功；而**byType**就是拿**变量类型UserService**去**匹配IOC容器**的idcom.test.UserService.UserServiceImpl，因为UserServiceImpl是UserService实现，所以也匹配成功

接下来再分别讲讲@Autowired注解和@Resource注解的使用

@Autowird注解的使用
步骤：**@Autowird**默认的注入方式为**byType**，也就是根据类型匹配，当有**多个实现**时，则通过**byName**注入，也可以通过配合**@Qualifier**注解来**显式指定name值**，指明要使用哪个具体的实现类

举例：

首先有一个接口UserService和两个实现类UserServiceImpl1和UserServiceImpl2，并且这两个实现类已经加入到Spring的IOC容器中了

```java
@Service
public class UserServiceImpl1 implements UserService

@Service
public class UserServiceImpl2 implements UserService
通过@Autowired注入使用
```

```java
@Autowired
private UserService userService;
```

根据上面的步骤，可以很容易判断出，直接这么使用是会报错的
原因：首先通过byType注入，判断UserService类型有两个实现，无法确定具体是哪一个，于是通过byName方式，这里的变量名userService也无法匹配IOC容器中id（此处指的userServiceImpl1和userServiceImpl2），于是报错。

注意：通过注解注入到IOC容器的id值默认是其**类名首字母小写**

解决方案

方式一：

```java
// 方式一：改变变量名
@Autowired
private UserService userServiceImpl1;
```

方式二：

```java
// 方式二：配合@Qualifier注解来显式指定name值
@Autowired
@Qualifier(value = "userServiceImpl1")
private UserService userService;
```

**@Resource注解**的使用
步骤：@Resource**默认通过byName**注入，如果没有匹配则通过byType注入

举例：

```java
@Service
public class UserServiceImpl1 implements UserService

@Service
public class UserServiceImpl2 implements UserService

@Resource
private UserService userService;
```

首先通过byName匹配，变量名userService无法匹配IOC容器中任何一个id（这里指的userServiceImpl1和userServiceImpl2），于是通过byType匹配，发现类型UserService的实现类有两个，仍然无法确定，于是报错。

同时@Resource还有两个重要的属性：name和type，用来显式指定byName和byType方式注入

使用：对应4种情况

```java
// 1. 默认方式：byName
@Resource  
private UserService userDao; 
```

```java
// 2. 指定byName
@Resource(name="userService")  
private UserService userService; 
```

```java
// 3. 指定byType
@Resource(type=UserService.class)  
private UserService userService; 
```

```java
// 4. 指定byName和byType
@Resource(name="userService",type=UserService.class)  
private UserService userService; 
```

**既没指定name属性，也没指定type属性**：默认通过byName方式注入，如果byName匹配失败，则使用byType方式注入（也就是上面的那个例子）

**指定name属性**：通过byName方式注入，把变量名和IOC容器中的id去匹配，匹配失败则报错

**指定type属性**：通过byType方式注入，在IOC容器中匹配对应的类型，如果匹配不到或者匹配到多个则报错

**同时指定name属性和type属性**：在IOC容器中匹配，名字和类型同时匹配则成功，否则失败

## Spring中默认提供的单例是线程安全的吗？

不是。

Spring容器本身并没有提供Bean的线程安全策略。如果单例的Bean是一个**无状态的Bean**，即**线程中的操作不会对Bean的成员执行查询以外的操作，那么这个单例的Bean是线程安全的。**比如，Controller、Service、DAO这样的组件，通常都是**单例且线程安全的**。如果单例的Bean是一个**有状态的Bean**，则可以**采用ThreadLocal对状态数据做线程隔离，来保证线程安全。**

## **SpringIOC&AOP**

### **IoC**

IoC(控制反转)是一种设计思想，就是将**原本在程序中手动创建对象的控制权，交由Spring框架来管理**，**依赖注入**（Dependency Injection）是IOC的具体实现。

IoC容器是Spring用来**实现IoC的载体**，IoC容器实际上就是个**Map(key,value)**，Map中**存放的是各种对象**。

将对象之间的相互依赖关系交给IoC容器来管理，并由IoC容器完成出来对象的注入。降低了对象之间的耦合，当我们需要使用这个对象的时候直接从IOC中获取，获取方式有三种 **构造器注入  setter方法注入  注解注入**



Spring时代一般使用XML文件来配置Bean，后来开发人员觉得XML文件来配置不太友好，于是SpringBoot注解就慢慢流行起来了。

![img](https://img-blog.csdnimg.cn/20210426130552866.png)

![img](https://img-blog.csdnimg.cn/20210426130549113.png)

直接去工厂取，而不是去关联对象，因为可能一个类中会用多个对象，有工厂的话，那么只需要工厂一个类，而不是很多的类，减少耦合。

### **AOP**

AOP能够将**那些与业务无关，却为业务模块所共同调用的逻辑或责任**(例如事务管理、日志管理、权限控制)**封装起来**，便于减少系统的重复代码，降低模块间的耦合度，并有利于未来的可拓展性和可维护性。

原理：动态代理

一个工程如果依赖另一个工程给的接口，但是另一个工程的接口不稳定，经常变更协议，就可以使用一个代理，接口变更时，只需要修改代理，不需要一一修改业务代码。

#### 作用：

- **功能增强**：在原有功能加新功能
- **控制访问**：代理类不让你访问目标

#### AOP的术语：

- **连接点**（join point）：对应的是**具体被拦截的对象**，因为Spring只能支持方法，所以被拦截的对象往往就是指特定的方法，AOP将通过动态代理技术把它织入对应的流程中。
- **切点**（point cut）：有时候，我们的切面不单单应用于单个方法，也可能是多个类的不同方法，这时，可以通过正则式和指示器的规则去定义，从而适配连接点。切点就是提供这样一个功能的概念。
- **通知**（advice）：就是按照约定的流程下的方法，分为**前置通知**、**后置通知**、**环绕通知**、**事后返回通知**和**异常通知**，它会根据约定织入流程中。
- **目标对象**（target）：即被代理对象。
- **引入**（introduction）：是指引入新的类和其方法，增强现有Bean的功能。
- **织入**（weaving）：它是一个通过**动态代理**技术，为**原有服务对象生成代理对象**，然**后将**与**切点定义匹配**的**连接点拦截**，并按约定**将**各类**通知织入**约定**流程**的过程。
- **切面**（aspect）：是一个可以定义切点、各类通知和引入的内容，SpringAOP将通过它的信息来增强Bean的功能或者将对应的方法织入流程。

#### **应用场景：**

Spring AOP为IoC的使用提供了更多的便利，一方面，应用可以直接使用AOP的功能，设计应用的横切关注点，把跨越应用程序多个模块的功能抽象出来，并通过简单的AOP的使用，灵活地编制到模块中，比如可以**通过AOP实现应用程序中的日志功能**。另一方面，在Spring内部，一些支持模块也是通过Spring AOP来实现的，比如**事务处理**。从这两个角度就已经可以看到Spring AOP的核心地位了。

#### Spring AOP不能对哪些类进行增强？

1. Spring AOP只能对IoC容器中的Bean进行增强，对于不受容器管理的对象不能增强。
2. 由于CGLib采用动态创建子类的方式生成代理对象，所以不能对final修饰的类进行代理。

#### 动态代理

**JDK动态代理：**利用**反射机制生成代理类**，可以**动态指定代理类的目标类**，要求实现**invocationHandler**接口，**重写invoke方法**进行功能增强，还要求**目标类必须实现接口**，

**Cjlib动态代理：**利用ASM开源包，**把代理对象的Class文件加载进来**，**修改其字节码文件生成子类**，**子类重写目标类的方法**，**被final修饰不可以**，然后在**子类采用方法拦截技术拦截父类方法**调用，**织入逻辑**（定义拦截器实现MethodInterceptor接口）

Spring AOP是基于动态代理的，如果要代理的**对象**，**实现了某个接口**，那么Spring AOP会**使用JDK Proxy**,去**创建代理对象**，而对于没有实现接口的对象(有些类单类，不去实现接口)，就无法使用JDK Proxy去进行代理，这时候Spring AOP会使用Cglib，这时候Spring AOP会使用Cglib生成一个被代理对象的子类来作为代理，如下图所示：

![img](https://img-blog.csdnimg.cn/2021042613060643.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwMjYyMzcy,size_16,color_FFFFFF,t_70)

```java
//动态代理代码
//Rent.java 即抽象角色
public interface Rent {
    public void rent();
}

//Host.java 即真实角色
//房东 真实角色
public class Host implements Rent {

    @Override
    public void rent() {
        System.out.println("房东要出租房子");
    }
}

//ProxyInvocationHandler. java 即代理角色
public class ProxyInvocationHandler implements InvocationHandler {
    private Rent rent;

    public void setRent(Rent rent) {
        this.rent = rent;
    }
    //生成代理类，重点是第二个参数，获取要代理的抽象角色!之前都是一个角色，现在可以代理一类角色
    public Object getProxy(){
        return Proxy.newProxyInstance(this.getClass().getClassLoader(), rent.getClass().getInterfaces(),this);
    }
    //proxy:代理类method：代理类的调用处理程序的方法对象
    //处理代理实例上的方法调用并返回结果
    @Override
    public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
        seeHouse();
        Object result=method.invoke(rent,args);
        fare();
        return result;
    }
    public void seeHouse(){
        System.out.println("带房客看房");
    }
    public void fare(){
        System.out.println("收中介费");
    }
}

//Client.java
public class Client {
    public static void main(String[] args) {
        //真实角色
        Host host=new Host();
        //代理实例调用处理程序
        ProxyInvocationHandler pih=new ProxyInvocationHandler();
        pih.setRent(host);//把真实角色放进去！
        Rent proxy = (Rent) pih.getProxy();
        proxy.rent();
    }
}
```

就相当于一个类不能满足要求了，另外开一个类去获得该类的方法，然后自己在添加方法。

这个是动态代理，没有专门写一个类来扩展，是需要的时候我们另开一个类代理，因此我们就会有一个Proxy.newProxyInstance方法来获得当前需要被代理的类，然后被代理后就在invoke中加入要另外添加的东西。

当然也可以使用AspectJ,任何对象都可以使用，基于字节码操作，编译时增强；但是Spring AOP只能用作Spring Beans上，基于代理(Proxy)，运行时增强。

方式一：使用Spring的API接口

方式二：自定义来实现AOP

方式三：使用注解实现

```java
//AspectJ代码

```

**代理模式：**

**静态代理模式**的好处：

- 可以使真实觉得的操作更加纯粹!不用关注一些公共的业务
- 公共也就是交给代理角色！实现了业务的分工！
- 公共业务发生扩展的时候，方便集中管理。

缺点:

- **一个真实角色**就会**产生一个代理角色**；**代码量会翻倍**~开发效率会变低~

动态代理的好处：

- 可以使真实角色的**操作更加纯粹!**不用关注一些公共的业务
- 公共也就是**交给代理角色**！实现了业务的分工！
- 公共业务发生扩展的时候，方便**集中管理**。
- 一个**动态代理类**就是**一个接口**，一般就是**对应的一类业务**
- 一个动态代理类**可以代理多个类**，只要是**实现**了**同一个接口**即可。

#### 既然有没有接口都可以用CGLIB，为什么Spring还要使用JDK动态代理？

在**性能**方面，**CGLib**创建的**代理对象**比**JDK动态代理**创建的**代理对象高很多**。但是，CGLib在创建代理对象时所**花费的时间**比JDK动态代理**多很多**。所以，对于**单例的对象**因为**无需频繁创建代理对象**，采用**CGLib动态代理**比较合适。反之，对于**多例的对象因为需要频繁的创建代理对象**，则**JDK动态代理**更合适。

## Servlet生命周期

加载阶段、初始化阶段、请求处理、销毁阶段

init(), service(), destory()

### **Spring bean**

**spring是如何管理Bean的**

Spring通过IoC容器来管理Bean，我们可以通过XML配置或者注解配置，来指导IoC容器对Bean的管理。因为注解配置比XML配置方便很多，所以现在大多时候会使用注解配置的方式。

1. @**ComponentScan**用于声明扫描策略，通过它的声明，容器就知道要扫描哪些包下带有声明的类，也可以知道哪些特定的类是被排除在外的。
2. @**Component**、@**Repository**、@**Service**、@**Controller**用于声明Bean，它们的作用一样，但是语义不同。@Component用于声明通用的Bean，@Repository用于声明DAO层的Bean，@Service用于声明业务层的Bean，@Controller用于声明视图层的控制器Bean，被这些注解声明的类就可以被容器扫描并创建。
3. @**Autowired**、@**Qualifier**用于注入Bean，即告诉容器应该为当前属性注入哪个Bean。其中，@Autowired是按照Bean的类型进行匹配的，如果这个属性的类型具有多个Bean，就可以通过@Qualifier指定Bean的名称，以消除歧义。
4. @**Scope**用于声明Bean的作用域，默认情况下Bean是单例的，即在整个容器中这个类型只有一个实例。可以通过@Scope注解指定prototype值将其声明为多例的，也可以将Bean声明为session级作用域、request级作用域等等，但最常用的还是默认的单例模式。
5. @**PostConstruct**、@**PreDestroy**用于声明Bean的生命周期。其中，被@PostConstruct修饰的方法将在Bean实例化后被调用，@PreDestroy修饰的方法将在容器销毁前被调用。

**Spring中的bean的作用域有那些?**

Bean的含义：被Spring IOC容器初始化、装配、管理的对象。那么对于Spring托管的单例ServiceBean，如何保证安全？Spring的单例是基于BeanFatory也就是Spring容器的，单例Bean在此容器内只有一个，Java的单例是基于JVM，每个JVM中内只有一个实例。

默认情况下，Bean在Spring容器中是单例的，我们可以通过@Scope注解修改Bean的作用域。该注解有如下5个取值，它们代表了Bean的5种不同类型的作用域：

|        类型        |                             说明                             |
| :----------------: | :----------------------------------------------------------: |
|   **singleton**    |     在spring容器中仅存在一个实例，即Bean以单例的形式存在     |
|   **prototype**    |    每次调用getBean()时，都会执行new操作，返回一个新的实例    |
|    **request**     | 每个HTTP请求都会创建一个新的实例，该bean仅在当前HTTP request内有效 |
|    **session**     | 每一次HTTP请求都会产生一个新的bean,该bean仅在当前HTTP session内有效 |
| **Global-session** | 全局session作用域，仅仅在基于portlet的web应用中才有意义，Spring5已经没有了。 |

**Spring中的单例bean的线程安全了解吗？**

单例bean存在线程问题，主要是因为当多个线程操作同一个对象的时候，对这个对象的非静态成员变量的写操作会存在线程安全问题。

  常见的两种解决方法：

  1.在Bean对象中尽量避免定义可变的成员变量(不太现实)。

  2.在类中定义一个**ThreadLocal**成员变量，将需要的**可变成员变量保存在ThreadLocal**中。

**@Component和@Bean的区别是什么？**

1.作用对象不同：**@Component注解作用于类**，而**@Bean注解作用于方法**,因为这个方法**返回的就是new** 类。

[2.@Component](mailto:2.@Component)通常是通过类路径扫描来自动装配到Spring容器中(会调用ComponentScan注解去扫描路径)。@Bean告诉了Spring这是某个类的示例，当我们需要用它的时候就给我。

3.当我们要引用第三方库的类时，我们只能用@Bean。

**将一个类声明为Spring的bean的注解有那些？**

我们一般使用@Autowired注解自动装配bean，要想把类标识成@Autowired能自动装配的bean，采用以下注解实现：

  @Component:通用的注解，可标注任意类为Spring组件。如果一个Bean不知道属于哪个层，可以使用@Component注解标注。

  @Repository:对应持久层即Dao层，主要有用于数据库的操作。

  @Service：对应服务层，主要涉及一些复杂的逻辑，需要用到Dao层。

  @Controller:对应Spring MVC控制层，主要用户接受用户请求并调用Service层返回数据给前端页面。

**Spring中的bean生命周期？**

从**创建Spring IOC容器开始**，直到**最终spring IOC容器销毁Bean为止**

1.通过构造器创建bean实例(无参数构造)

2.为bean的属性设置值和对其他bean引用(调用set方法)

![init-method-" initMethod"  <bean  destroy-method-"destor Method" >  <property name="oname" value =  </bean> ](C:/Users/chm/Desktop/Java学习/面经.assets/clip_image001.png)

![Applicationcontext applicationcontext =  new  applicationcontext . getBean(  Orders orders =  classpathxmlApplicationcontext(C:/Users/chm/Desktop/Java学习/面经.assets/clip_image002.png);  s: " orders"  configLocation:  "bean4.xml ](面经.assets/clip_image002.png)

3.调用bean的初始化的方法(需要进行配置)

![img](C:/Users/chm/Desktop/Java学习/面经.assets/clip_image003.png)

![public void initMethod(C:/Users/chm/Desktop/Java学习/面经.assets/clip_image004.png){  System . out. println( ) ; ](面经.assets/clip_image004.png)

4.bean可以使用了(对象获取到了)

5.当容器关闭时，调用bean的销毁的方法

![img](C:/Users/chm/Desktop/Java学习/面经.assets/clip_image005.png)

![public void  System . out. println(C:/Users/chm/Desktop/Java学习/面经.assets/clip_image006.png ) ; ](面经.assets/clip_image006.png)

3.演示bean生命周期

![1 ． 执 行 无 参 数 造 创 建 bean 实 例  2 ． 调 用 set 方 法 设 置 属 性 值  3 ． 执 行 初 始 化 方 法  4 ． 获 取 创 建 bean 实 例 对 象  com.chm.spring5.collect10ntype.bean.Ordersö)3891771e  5 ． 执 行 销 毁 的 方 法 ](C:/Users/chm/Desktop/Java学习/面经.assets/clip_image007.png)

![img](https://img-blog.csdnimg.cn/20210426130634981.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwMjYyMzcy,size_16,color_FFFFFF,t_70)

 总结下来，只有**4个**。

1. 实例化

2. 属性赋值

3. 初始化

4. 使用

5. 销毁

实例化属性赋值->初始化->销毁

实例->设置属性->aware->BeanPostProcessor->initialzingBean->init-method->BeanPostProcessor->使用->destory->destort-method

首先根据配置文件利用**反射创建Bean实例**，然后为**bean实例设置属性**，如果Bean**实现了*.Aware接口，调用相应的方法**，然后**执行BeanPostProcessor的初始化前置处理方法**，如果**实现了InitializingBean接口，执行afterPropertiesSet**然后**执行init-method属性执行指定的方法**，再**执行BeanPostProcessor的初始化后置处理方法**，然后**使用Bean**，**执行DisposableBean的destroy方法**，最后执行destroy-method属性指定的方法。

**1.实例化bean对象**

Bean容器找到配置文件中Spring Bean的定义

Bean容器利用java Reflection API**创建一个Bean的实例**

**2.设置对象属性**

如果涉及一些属性值，利用**set()方法设置一些属性值**

**3.检查Aware相关接口并设置相关依赖**

如果Bean实现了BeanNameAware接口，调用setBeanName()方法，传入Bean的名字

如果Bean实现了BeanClassLoaderAware接口，调用setBeanClassLoader()方法，传入ClassLoader对象的实例。

如果实现了其他*.Aware接口，就调用相应的方法。

**4.BeanPostProcessor前置处理**

如果有和加载这个Bean的Spring容器相关的BeanPostProcessor对象，执行postProcessBeforeInitialization()方法。

**5.包含init-method属性，执行指定方法**

如果Bean在配置文件中的定义包含init-method属性，执行指定的方法。

**6.BeanPostProcessor后置处理**

如果有和加载这个Bean的Spring容器相关的BeanPostProcessor对象，执行postProcessAfterInitialization()方法。

**7.执行destroy**

当要销毁Bean的时候，如果Bean实现了DisposableBean接口，执行destroy()方法。

当要销毁Bean的时候，如果Bean在配置文件中的定义包含destroy-method属性，执行指定的方法。

**Bean的注入方式：**

**setter**方法注入：

![img](https://img-blog.csdnimg.cn/20210426130648388.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwMjYyMzcy,size_16,color_FFFFFF,t_70)

通过setter方法，可以更改相应的对象属性。所以，当前对象只要为其依赖对象所对应的属性添加setter方法，就可以通过setter方法将相应的依赖对象设置到被注入对象中。可以在对象构造完成后再注入。

2.**构造器注入**：

构造器可以用三个方式：1.参数名称 2.参数下标 3.参数类型

就是被注入对象可以在它的构造方法中声明依赖对象的参数列表，让外部知道它需要哪些依赖对象。然后，IoC Service Provider会检查被注入的对象的构造方法，取得它所需要的依赖对象列表，进而为其注入相应的对象。构造方法注入方式比较直观，对象被构造完成后，即进入就绪状态，可以马上使用。

```java
//在Student类中增加以下构造方法：

public Student(String no, String name, String gender) {
    this.no = no;
    this.name = name;
    this.gender = gender;
}
```

```xml
//配置中增加以下配置：
<bean id="s3" class="com.etc.entity.Student" >
    <constructor-arg index="0" value="2015001002"/>
    <constructor-arg index="1" value="李四"/>
    <constructor-arg index="2" value="男"/>
</bean>
//注意：index=0的注入到第一个参数，index=1的注入到第二个参数，Spring 3推荐使用该方法。

//或者：

<bean id="s4" class="com.etc.entity.Student" >
    <constructor-arg name="name" value="李四"/>
    <constructor-arg name="no" value="2015001002"/>
    <constructor-arg name="gender" value="男"/>
</bean>
//直接指定参数名称，Spring 4推荐使用该方式。

<bean id="s5" class="com.etc.entity.Student" >
    <constructor-arg  type="java.lang.String" value="2015001002"/>
    <constructor-arg  type="java.lang.String" value="李四"/>
    <constructor-arg  type="java.lang.String" value="男"/>
</bean>
```

3.**接口注入**

被注入对象如果想要IoC Service Provider为其注入依赖对象，就必须实现某个接口。这个接口提供一个方法，用来为其注入依赖对象。IoC Service Provider最终通过这些接口来了解应该为被注入对象注入什么依赖对象。相对于前两种依赖注入方式，接口注入比较死板和烦琐。

```java
public class ClassA {
  private InterfaceB clzB;
  public void doSomething() {
    Ojbect obj = Class.forName(Config.BImplementation).newInstance();
    clzB = (InterfaceB)obj;
    clzB.doIt(); 
  }
……
}
```

解释一下上述的代码部分，ClassA依赖于InterfaceB的实现，我们如何获得InterfaceB的实现实例呢？传统的方法是在代码中创建 InterfaceB实现类的实例，并将赋予clzB.这样一来，ClassA在编译期即依赖于InterfaceB的实现。为了将调用者与实现者在编译期分离，于是有了上面的代码。我们根据预先在配置文件中设定的实现类的类名(Config.BImplementation),动态加载实现类，并通过InterfaceB强制转型后为ClassA所用，这就是接口注入的一个最原始的雏形。

3.**静态工厂**注入：

我们编写一个静态的工厂方法，这个工厂方法会返回一个我们需要的值，然后在配置文件中，我们指定使用这个工厂方法创建bean。注意是静态方法！

```java
//编写factory类：
package com.Kevin.factorybean;
/**
 * 编写工厂类测试静态工厂方法注入
 * @author Kevin
 *
 */
public class CarFactory {
  public static Car createCar(){
    Car car = new Car();
    car.setBrand("Lamborghini");
    return car;
  }
}

//编写配置文件：
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xmlns:context="http://www.springframework.org/schema/context" xsi:schemaLocation="
    http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
    http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context.xsd"> <!-- bean definitions here -->
  <!-- 配置对象 -->
  <bean id="car" class="com.Kevin.factorybean.Car" factory-method="createCar"></bean>  
</beans>
```

4.**实例工厂**注入

实例工厂与静态工厂，不同的是，**静态工厂**调用工厂方法**不需要先创建工厂类的对象**，因为静态方法**可以直接通过类调用**，所以在上面的配置文件中，并不会声明工厂类的bean。但是，**实例工厂，需要一个实例对象**，才能调用它的工程方法。

```java
//编写工厂类：
package com.Kevin.factorybean;
/**
 * 编写工厂类测试非静态工厂方法注入
 * @author Kevin
 *
 */
public class BookFactory {
  public Book buyBook(){
    Book book = new Book();
    book.setName("Think in Java");
    return book;
  }
}

//配置文件编写：
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xmlns:context="http://www.springframework.org/schema/context" xsi:schemaLocation="
    http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
    http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context.xsd"> <!-- bean definitions here -->
 
  <!-- 配置对象 -->
  <bean id="bookFactory" class="com.Kevin.factorybean.BookFactory"></bean>
  <bean id="book" factory-bean="bookFactory" factory-method="buyBook"></bean>
  </beans>
```

**Bean的扫描加载过程**

![img](面经.assets/2021042613070656.png)

如何从一个配置文件到一个对象：

![img](https://img-blog.csdnimg.cn/20210426130709738.png)

bean定义对象：定义bean的一些属性，比如作用域，是否懒加载等。

从xml文件到最后的bean拿来应用放在哪里，bean放在IOC容器(是一个概念)中，实际上用数据结构存储，用的Map存储。

![img](https://img-blog.csdnimg.cn/2021042613071315.png)

既然是一个容器，那么肯定有一个入口，所有Spring容器有一个根接口。**BeanFactory**

![img](https://img-blog.csdnimg.cn/20210426130716628.png)

![img](https://img-blog.csdnimg.cn/20210426130719732.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwMjYyMzcy,size_16,color_FFFFFF,t_70)

![img](https://img-blog.csdnimg.cn/20210426130722680.png)

选择入口和容器都有了，那么就该放对象了，放对象的操作。

![img](https://img-blog.csdnimg.cn/20210426130728562.png)

因此在容器中就会有一个beanDefination，给容器添加元素。

![img](https://img-blog.csdnimg.cn/2021042613073752.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwMjYyMzcy,size_16,color_FFFFFF,t_70)

有不同类型进行定义Bean，因此其中会有一个统一接口BeanDefinitionReader去解析成统一规格给BeanDefinition。

![img](https://img-blog.csdnimg.cn/20210426130742354.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwMjYyMzcy,size_16,color_FFFFFF,t_70)

那么从BeanDefinition直接到实例化,直接到到了吗？肯定不会这么简单啊。进一步再回忆Spring是什么？

![img](https://img-blog.csdnimg.cn/20210426130745546.png)

我需要单独都写一个框架吗？肯定不是啊。因此Spring底层肯定满足**扩展性、扩展性、扩展性**

![img](https://img-blog.csdnimg.cn/20210426130748969.png)

因此从BeanDefinition无论是new还是反射，都不会到实例化的。

为什么要使用反射？反射性能不是低吗？ 反射只是成十万对象的时候才会出现性能瓶颈，几十个、几百个不印象的是不会成为性能问题。因为反射足够的灵活！！我们想要new一个实例出来，必须要知道这个类。我们在配置文件中写好了类吗？我们在配置文件中是写好了类的完全限定名，我们知道这个限定名，是无法直接获取class对象和字节码文件的。

![img](https://img-blog.csdnimg.cn/20210426130753298.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwMjYyMzcy,size_16,color_FFFFFF,t_70)

Xml读到BeanDefinition去的是${jdbc.url}还是实际的值。正确答案是带参数占位符的${jdbc.url}，因此我们要想实例化，肯定要去把这个替换掉成为我们想要的实际值。所以在BeanDefinition到实例化肯定还有过程。

在进行反射之前，肯定要换成真实变量，所以就要开始慢慢引入把占位符的东西换成我们真实需要的东西。

![img](https://img-blog.csdnimg.cn/202104261307590.png)

这个PostProcessor就是将占位符、空配符换成我们真实的属性。这两个是**不同阶段的操作**，因此要分成BeanFactory和Bean。

![img](https://img-blog.csdnimg.cn/20210426130804209.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwMjYyMzcy,size_16,color_FFFFFF,t_70)

BeanDefinition读过来后，我们要进行实例化了，要修改工厂中的某些对象，将那些占位符的修改成真实值。因此经过BeanFactoryPostProcessor将BeanDefinition中一些具有占位符的属性换成我们真实的值。

![img](https://img-blog.csdnimg.cn/20210426130807663.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwMjYyMzcy,size_16,color_FFFFFF,t_70)

BeanFactoryPostProcessor可以修改bean的definition参数，上图是自己建立的一个类，然后去实现BeanFactoryPostProcessor接口。

Spring一开始出来的时候，是写xml,后来注解可以用了，我们把注解集成到Spring生态中去。

通过BeanFactoryPostProcessor修改完后，我们就可以通过反射对类进行实例化。

![img](https://img-blog.csdnimg.cn/20210426130811386.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwMjYyMzcy,size_16,color_FFFFFF,t_70)

这样创建的对象是不完整的，创建对象是真正包括两块的：

![img](https://img-blog.csdnimg.cn/20210426130818929.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwMjYyMzcy,size_16,color_FFFFFF,t_70)

那么回到IOC容器中，我们在实例化后，还有一系列的初始化操作，调用aware接口的方法。Bean的生命周期操作。

![img](https://img-blog.csdnimg.cn/20210426130822184.png)

![img](https://img-blog.csdnimg.cn/20210426130825790.png)

例子解释aware，一个类先是用name，get\set

![img](https://img-blog.csdnimg.cn/20210426130832582.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwMjYyMzcy,size_16,color_FFFFFF,t_70)

现在又增加一个属性beanName，也有set/get

![img](https://img-blog.csdnimg.cn/20210426130836612.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwMjYyMzcy,size_16,color_FFFFFF,t_70)

beanName我是后来又加的，意味着我们又增加set方法吗？实则不需要，我们只用实现BeanNameAware即可(有别名之类的，因此要统一名字)，然后会让我强行重写set方法。这里实际上就是在**注入**了

![img](https://img-blog.csdnimg.cn/20210426130839885.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwMjYyMzcy,size_16,color_FFFFFF,t_70)

实现了aware接口我们就去拿容器的对象了。

跟直接set有什么区别：

直接set的前提是你要有对象，在容器里面怎么调用这个set。

所以容器里的aware帮你去set，之后得到对象后直接get即可。  在这里我们已经把bean对象搞定了，但是为了Spring大生态，这里Bean对象还要经过加工才可以。调试源码的例子：

populateBean 是给注入普通属性

initializeBean 是注入Aware接口的属性

![img](https://img-blog.csdnimg.cn/20210426130848347.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwMjYyMzcy,size_16,color_FFFFFF,t_70)

![img](https://img-blog.csdnimg.cn/20210426130855676.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwMjYyMzcy,size_16,color_FFFFFF,t_70)

![img](https://img-blog.csdnimg.cn/20210426130900433.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwMjYyMzcy,size_16,color_FFFFFF,t_70)

如果去掉setBeanName的复制，那么下面就是这样的注入属性了

![img](https://img-blog.csdnimg.cn/20210426130905820.png)

这个就会变为空了。

![img](https://img-blog.csdnimg.cn/20210426130910312.png)

Before,after都是AOP织入进去的。

![img](https://img-blog.csdnimg.cn/20210426130913685.png)

中间就是自己自定义的方法，bean配置中有一个init-method

![img](https://img-blog.csdnimg.cn/20210426130917497.png)

加载Bean的时候可以执行自己定义的方法一次。

Before与After 用的AOP，AOP基于动态代理，动态代理两种方式解决，jdk,cglib： 有接口用jdk，没接口用cglib。

![img](https://img-blog.csdnimg.cn/20210426130922756.png)

然后获取真正的Bean对象

![img](https://img-blog.csdnimg.cn/20210426130927365.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwMjYyMzcy,size_16,color_FFFFFF,t_70)

总结下来：生命周期包括：实例化，初始化，销毁

看懂**refresh**的十三个方法就把Spring源码搞懂了。

![img](https://img-blog.csdnimg.cn/20210426130932939.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwMjYyMzcy,size_16,color_FFFFFF,t_70)

1. 准备容器，prepareRefresh，设置启动时间之类的，初始化资源之类，跟Bean无关的。
2. obtainBeanFactory,如果存在就毁掉，重新重建，里面开始加载beanDefinition(beanDefinitionMap和beanDefinitionNames)，loadBeanDefinitions一直套娃,一直在重载。
3. 得到BeanDefinition后，就开始用BeanFactoryPostProcessors。一直给我们BeanDefinition设置属性值
4. invokeBeanFactoryPostProcessor()调用这个PostProcessor，容器中全部没有类，全靠反射搞类。
5. 实例化这边这么多步骤，要不要做准备工作呢？before,after 要进行postprocessor准备工作还要准备监听器，广播器。registerBeanPostProcessors 做准备工作，等到后面before或after才开始执行
6. finishBeanFactoryInitialization开始实例化了。里面也是set,add。也是设置属性。最后一行，preInstantiate,默认单例，容器里有且只有一个对象，在每次创建前先要去获取，再看有没有，源码里有doXXX是实际干活的方法，看见什么代码，意味着Bean创建成功。一路搞构造器，新建实例。
7. 填充属性，是填充我们自己set的内容，比如姓名=zhangsan
8. invokeAwareMethods，将aware接口的beanName赋值，但是applicitioncontext没有赋值
9. applicationcontext是在before完成的
10. nitMethod方法
11. AfterMethod
12. 继续循环。直到新注册的bean搞完。

## spring怎么解决循环依赖的

首先，需要明确的是spring对循环依赖的处理有三种情况：

1. **构造器的循环依赖**：这种依赖spring是处理不了的，直接抛出BeanCurrentlylnCreationException异常。
2. **单例模式下的setter**循环依赖：通过“**三级缓存**”处理循环依赖。
3. **非单例循环依赖**：无法处理。

接下来，我们具体看看spring是如何处理第二种循环依赖的。

Spring单例对象的初始化大略分为三步：

1. createBeanInstance：实例化，其实也就是调用对象的构造方法实例化对象；
2. populateBean：填充属性，这一步主要是多bean的依赖属性进行填充；
3. initializeBean：调用spring xml中的init 方法。

从上面讲述的单例bean初始化步骤我们可以知道，循环依赖主要发生在第一步、第二步。也就是构造器循环依赖和field循环依赖。 Spring为了解决单例的循环依赖问题，使用了三级缓存。

“A的某个field或者setter依赖了B的实例对象，同时B的某个field或者setter依赖了A的实例对象”这种循环依赖的情况。A首先完成了初始化的第一步，并且将自己提前曝光到singletonFactories中，此时进行初始化的第二步，发现自己依赖对象B，此时就尝试去get(B)，发现B还没有被create，所以走create流程，B在初始化第一步的时候发现自己依赖了对象A，于是尝试get(A)，尝试一级缓存singletonObjects(肯定没有，因为A还没初始化完全)，尝试二级缓存earlySingletonObjects（也没有），尝试三级缓存singletonFactories，由于A通过ObjectFactory将自己提前曝光了，所以B能够通过ObjectFactory.getObject拿到A对象(虽然A还没有初始化完全，但是总比没有好呀)，B拿到A对象后顺利完成了初始化阶段1、2、3，完全初始化之后将自己放入到一级缓存singletonObjects中。此时返回A中，A此时能拿到B的对象顺利完成自己的初始化阶段2、3，最终A也完成了初始化，进去了一级缓存singletonObjects中，而且更加幸运的是，由于B拿到了A的对象引用，所以B现在hold住的A对象完成了初始化。

## **Spring事务**

 Spring事务的本事其实就是数据库对事务的支持，没有数据库的事务支持，spring是无法提供事务功能的。对于纯JDBC操作数据库，想要用到事务，可以按照这几步：

1.获得连接

2.开启事务

3.执行JDBC

4.提交事务/回滚事务

5.关闭连接

Spring的事务是帮我们做了第2步和第4步，是利用动态代理方法。



#### **Sprig管理事务的方式有几种？**

 1.编程式事务，在代码中硬编码。(不推荐使用)

 2.声明式事务，在配置文件中配置(推荐使用)



#### **声明式事务分为以下两种：**

1.基于XML的声明式事务

2.基于注解的声明式事务



#### **Spring事务的隔离级别有哪几种？**

TransactionDefinition接口中定义了五个表示隔离级别的常量(sql是4个+一个默认)：

1. Default:使用后端数据库默认的隔离级别，Mysql默认采用的是可重复读。Sqlsever默认采用的是读已提交。

2. 与sql的四个事务一样：读未提交、读已提交、可重复读、串行化。



#### **Spring事务中有哪几种事务传播行为？**

[(20条消息) 看完就明白_spring事务的7种传播行为_gnixlee的博客-CSDN博客_事务传播行为](https://blog.csdn.net/weixin_39625809/article/details/80707695)

![这里写图片描述](https://img-blog.csdn.net/20170420212829825?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvc29vbmZseQ==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

**1、PROPAGATION_REQUIRED**

如果存在一个事务，则支持当前事务。如果没有事务则开启一个新的事务。 
可以把事务想像成一个胶囊，在这个场景下方法B用的是方法A产生的胶囊（事务）。 
![这里写图片描述](https://img-blog.csdn.net/20170420213050220?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvc29vbmZseQ==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

举例有两个方法：

```java
@Transactional(propagation = Propagation.REQUIRED)
public void methodA() {
	 methodB();
	// do something
}

@Transactional(propagation = Propagation.REQUIRED)
public void methodB() {
    // do something
}
```

单独调用methodB方法时，因为当前上下文不存在事务，所以会开启一个新的事务。 
调用methodA方法时，因为当前上下文不存在事务，所以会开启一个新的事务。当执行到methodB时，methodB发现当前上下文有事务，因此就加入到当前事务中来。

**2、PROPAGATION_SUPPORTS**

如果存在一个事务，支持当前事务。如果没有事务，则非事务的执行。但是对于事务同步的事务管理器，PROPAGATION_SUPPORTS与不使用事务有少许不同。 
举例有两个方法：

```java
@Transactional(propagation = Propagation.REQUIRED)
public void methodA() {
 	methodB();
// do something
}

// 事务属性为SUPPORTS
@Transactional(propagation = Propagation.SUPPORTS)
public void methodB() {
    // do something
}
```

单纯的调用methodB时，methodB方法是非事务的执行的。当调用methdA时,methodB则加入了methodA的事务中,事务地执行。

**3、PROPAGATION_MANDATORY**

如果已经存在一个事务，支持当前事务。如果没有一个活动的事务，则抛出异常。

```java
@Transactional(propagation = Propagation.REQUIRED)
public void methodA() {
 methodB();
// do something
}

// 事务属性为MANDATORY
@Transactional(propagation = Propagation.MANDATORY)
public void methodB() {
    // do something
}
```

当单独调用methodB时，因为当前没有一个活动的事务，则会抛出异常throw new IllegalTransactionStateException(“Transaction propagation ‘mandatory’ but no existing transaction found”);当调用methodA时，methodB则加入到methodA的事务中，事务地执行。

**4、PROPAGATION_REQUIRES_NEW**

![这里写图片描述](https://img-blog.csdn.net/20170420213308563?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvc29vbmZseQ==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

使用PROPAGATION_REQUIRES_NEW,需要使用 JtaTransactionManager作为事务管理器。 
它会开启一个新的事务。如果一个事务已经存在，则先将这个存在的事务挂起。

```java
@Transactional(propagation = Propagation.REQUIRED)
public void methodA() {
	doSomeThingA();
	methodB();
	doSomeThingB();
	// do something else
}

// 事务属性为REQUIRES_NEW
@Transactional(propagation = Propagation.REQUIRES_NEW)
public void methodB() {
    // do something
}
```

当调用

```css
main{  
	methodA();
} 
```

相当于调用

```php
main(){
    TransactionManager tm = null;
    try{
        //获得一个JTA事务管理器
        tm = getTransactionManager();
        tm.begin();//开启一个新的事务
        Transaction ts1 = tm.getTransaction();
        doSomeThing();
        tm.suspend();//挂起当前事务
        try{
            tm.begin();//重新开启第二个事务
            Transaction ts2 = tm.getTransaction();
            methodB();
            ts2.commit();//提交第二个事务
        } Catch(RunTimeException ex) {
            ts2.rollback();//回滚第二个事务
        } finally {
            //释放资源
        }
        //methodB执行完后，恢复第一个事务
        tm.resume(ts1);
        doSomeThingB();
        ts1.commit();//提交第一个事务
    } catch(RunTimeException ex) {
        ts1.rollback();//回滚第一个事务
    } finally {
        //释放资源
    }
}
```

在这里，我把ts1称为外层事务，ts2称为内层事务。从上面的代码可以看出，ts2与ts1是两个独立的事务，互不相干。Ts2是否成功并不依赖于 ts1。如果methodA方法在调用methodB方法后的doSomeThingB方法失败了，而methodB方法所做的结果依然被提交。而除了 methodB之外的其它代码导致的结果却被回滚了

**5、PROPAGATION_NOT_SUPPORTED**

PROPAGATION_NOT_SUPPORTED 总是非事务地执行，并挂起任何存在的事务。使用PROPAGATION_NOT_SUPPORTED,也需要使用JtaTransactionManager作为事务管理器。 

![这里写图片描述](https://img-blog.csdn.net/20170420213400079?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvc29vbmZseQ==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

**6、PROPAGATION_NEVER**

总是非事务地执行，如果存在一个活动事务，则抛出异常。

**7、PROPAGATION_NESTED**

![这里写图片描述](https://img-blog.csdn.net/20170420213432872?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvc29vbmZseQ==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast) 
如果一个活动的事务存在，则运行在一个嵌套的事务中。 如果没有活动事务, 则按TransactionDefinition.PROPAGATION_REQUIRED 属性执行。 
这是一个嵌套事务,使用JDBC 3.0驱动时,仅仅支持DataSourceTransactionManager作为事务管理器。 
需要JDBC 驱动的java.sql.Savepoint类。使用PROPAGATION_NESTED，还需要把PlatformTransactionManager的nestedTransactionAllowed属性设为true(属性值默认为false)。

这里关键是嵌套执行。

```java
@Transactional(propagation = Propagation.REQUIRED)
methodA(){
  doSomeThingA();
  methodB();
  doSomeThingB();
}

@Transactional(propagation = Propagation.NEWSTED)
methodB(){
  ……
}
```

如果单独调用methodB方法，则按REQUIRED属性执行。如果调用methodA方法，相当于下面的效果：

```java
main(){
    Connection con = null;
    Savepoint savepoint = null;
    try{
        con = getConnection();
        con.setAutoCommit(false);
        doSomeThingA();
        savepoint = con2.setSavepoint();
        try{
            methodB();
        } catch(RuntimeException ex) {
            con.rollback(savepoint);
        } finally {
            //释放资源
        }
        doSomeThingB();
        con.commit();
    } catch(RuntimeException ex) {
        con.rollback();
    } finally {
        //释放资源
    }
}
```

当methodB方法调用之前，调用setSavepoint方法，保存当前的状态到savepoint。如果methodB方法调用失败，则恢复到之前保存的状态。但是需要注意的是，这时的事务并没有进行提交，如果后续的代码(doSomeThingB()方法)调用失败，则回滚包括methodB方法的所有操作。嵌套事务一个非常重要的概念就是内层事务依赖于外层事务。外层事务失败时，会回滚内层事务所做的动作。而内层事务操作失败并不会引起外层事务的回滚。

**PROPAGATION_NESTED 与PROPAGATION_REQUIRES_NEW的区别:**

它们非常类似,都像一个嵌套事务，如果不存在一个活动的事务，**都会开启一个新的事务**。 
使用 PROPAGATION_REQUIRES_NEW时，内层事务与外层事务就像两个独立的事务一样，一旦内层事务进行了提交后，外层事务不能对其进行回滚。两个事务互不影响。两个事务不是一个真正的嵌套事务。同时它需要JTA事务管理器的支持。

使用PROPAGATION_NESTED时，外层事务的回滚可以引起内层事务的回滚。而内层事务的异常并不会导致外层事务的回滚，它是一个真正的嵌套事务。DataSourceTransactionManager使用savepoint支持PROPAGATION_NESTED时，需要JDBC 3.0以上驱动及1.4以上的JDK版本支持。其它的JTATrasactionManager实现可能有不同的支持方式。

PROPAGATION_REQUIRES_NEW 启动一个新的, 不依赖于环境的 “内部” 事务. 这个事务将被完全 commited 或 rolled back 而不依赖于外部事务, 它拥有自己的隔离范围, 自己的锁, 等等. 当内部事务开始执行时, 外部事务将被挂起, 内务事务结束时, 外部事务将继续执行。

另一方面, PROPAGATION_NESTED 开始一个 “嵌套的” 事务, 它是已经存在事务的一个真正的子事务. 潜套事务开始执行时, 它将取得一个 savepoint. 如果这个嵌套事务失败, 我们将回滚到此 savepoint. 潜套事务是外部事务的一部分, 只有外部事务结束后它才会被提交。

由此可见, PROPAGATION_REQUIRES_NEW 和 PROPAGATION_NESTED 的最大区别在于, PROPAGATION_REQUIRES_NEW 完全是一个新的事务, 而 PROPAGATION_NESTED 则是外部事务的子事务, 如果外部事务 commit, 嵌套事务也会被 commit, 这个规则同样适用于 roll back.

#### Spring的事务如何配置，常用注解有哪些？

事务的打开、回滚和提交是由事务管理器来完成的，我们使用不同的数据库访问框架，就要使用与之对应的事务管理器。在Spring Boot中，当你添加了数据库访问框架的起步依赖时，它就会进行自动配置，即自动实例化正确的事务管理器。

对于声明式事务，是使用@Transactional进行标注的。这个注解可以标注在类或者方法上。

- 当它标注在类上时，代表这个类所有公共（public）非静态的方法都将启用事务功能。
- 当它标注在方法上时，代表这个方法将启用事务功能。

另外，在@Transactional注解上，我们可以使用isolation属性声明事务的隔离级别，使用propagation属性声明事务的传播机制。

**@Transactional(rollbackFor=Exception.class)注解了解吗？**

![img](https://img-blog.csdnimg.cn/20210426131020751.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwMjYyMzcy,size_16,color_FFFFFF,t_70)

怎么实现：

1.配置文件开启注解驱动，在相关的类和方法上通过注解@Transactional标识。

2.spring在启动的时候会去解析生成相关的bean,这时候会查看拥有相关注解的类和方法，并且为这些类和方法生成代理，并根据@Transaction的相关参数进行相关配置注入，这样就在代理中我们把相关的事务处理掉了(开启正常提交事务，异常回滚事务)。

3.真正的数据库的事务和回滚是通过binlog或者redo log实现的。

# **Spring MVC**

### **MVC介绍**

谈到[SpringMVC](https://so.csdn.net/so/search?q=SpringMVC&spm=1001.2101.3001.7020),我们不得不提一下之前**Model1**和**Model2**这两个没有SpringMVC时代。

**Model1(视图层+模型层):**

整个web项目都是用JSP写的，只有少量的JavaBean去和数据库打交道。这个模式下Jsp即使控制层又是表现层。显而易见，这个模式存在很多问题。①前端后端依赖严重，难以进行测试并开发效率低。②控制逻辑和表现逻辑是混杂一起，导致代码复用率低。

![img](https://img-blog.csdnimg.cn/20210426130941664.png)

**Model2:**

整个是由Javabean(Model)+JSP(View)+Servlet(Controller)。这种开发模式就是早期的JavaWeb MVC，但是用这种模式开发不可避免地会重复造轮子，这会大大降低程序的可维护性和复用性。

![img](https://img-blog.csdnimg.cn/2021042613094560.png)

MVC是一种设计模式，在这种模式下软件被分为三层，即Model（模型）、View（视图）、Controller（控制器）。Model代表的是数据，View代表的是用户界面，Controller代表的是数据的处理逻辑，它是Model和View这两层的桥梁。将软件分层的好处是，可以将对象之间的耦合度降低，便于代码的维护。

### DAO层是做什么的

DAO是Data Access Object的缩写，即数据访问对象，在项目中它通常作为独立的一层，专门用于访问数据库。这一层的具体实现技术有很多，常用的有Spring JDBC、Hibernate、JPA、MyBatis等，在Spring框架下无论采用哪一种技术访问数据库，它的编程模式都是统一的。

Spring MVC一般把后端项目分成Service层（处理业务）、Dao层（数据库操作）、Entity层（实体类）、Controller（控制层，返回数据给前台页面）。

### 介绍一下Spring MVC的执行流程

请求来到dispatcherServlet，调用HandlerMapping，解析得到Handler，再由HandlerAdapter根据Handler调用处理器处理请求返回modeview

1. 客户端（浏览器）发送请求，直接请求到DispatcherServlet
2. DispatcherServlet根据请求信息调用HandlerMapping，解析请求对应的Handler。
3. 解析得到对应的Handler（也就是我们平时说的Controller控制器后），开始由HandlerAdapter适配器处理
4. HandlerAdapter会根据Handler来调用真正的处理器来处理请求，并处理相应的业务逻辑
5. 处理器处理完业务后，会返回一个ModelAndView对象，Model是返回的数据对象，View是个逻辑上的View。
6. ViewResolver会根据逻辑View查找实际的View。
7. DispatcherServlet会把返回的Model传给View（视图渲染）。
8. 把View返回给请求者。

![image-20220608205825005](C:/Users/chm/Desktop/Java学习/面经.assets/image-20220608205825005.png)

![img](https://img-blog.csdnimg.cn/20210426130953563.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwMjYyMzcy,size_16,color_FFFFFF,t_70)

处理器中包含映射器和适配器。映射器是寻找Handler，返给前端控制器，然后再给适配器与Hanlder处理器弄。

### 说一说你知道的Spring MVC注解

**@RequestMapping：**

作用：该注解的作用就是用来处理请求地址映射的，也就是说将其中的处理器方法映射到url路径上。

属性：

- method：是让你指定请求的method的类型，比如常用的有get和post。
- value：是指请求的实际地址，如果是多个地址就用{}来指定就可以啦。
- produces：指定返回的内容类型，当request请求头中的Accept类型中包含指定的类型才可以返回的。
- consumes：指定处理请求的提交内容类型，比如一些json、html、text等的类型。
- headers：指定request中必须包含那些的headed值时，它才会用该方法处理请求的。
- params：指定request中一定要有的参数值，它才会使用该方法处理请求。

**@RequestParam：**

作用：是将请求参数绑定到你的控制器的方法参数上，是Spring MVC中的接收普通参数的注解。

属性：

- value是请求参数中的名称。
- required是请求参数是否必须提供参数，它的默认是true，意思是表示必须提供。

**@RequestBody：**

作用：如果作用在方法上，就表示该方法的返回结果是直接按写入的Http responsebody中（一般在异步获取数据时使用的注解）。

属性：required，是否必须有请求体。它的默认值是true，在使用该注解时，值得注意的当为true时get的请求方式是报错的，如果你取值为false的话，get的请求是null。

**@PathVaribale：**

作用：该注解是用于绑定url中的占位符，但是注意，spring3.0以后，url才开始支持占位符的，它是Spring MVC支持的rest风格url的一个重要的标志。

### 介绍一下Spring MVC的拦截器

拦截器会对处理器进行拦截，这样通过拦截器就可以增强处理器的功能。Spring MVC中，所有的拦截器都需要实现HandlerInterceptor接口，该接口包含如下三个方法：preHandle()、postHandle()、afterCompletion()。

![img](https://uploadfiles.nowcoder.com/images/20220224/4107856_1645694469544/31C010B3F63CB1CC1ADC5481E9E77BDB)



通过上图可以看出，Spring MVC拦截器的执行流程如下：

- 执行preHandle方法，它会返回一个布尔值。如果为false，则结束所有流程，如果为true，则执行下一步。
- 执行处理器逻辑，它包含控制器的功能。
- 执行postHandle方法。
- 执行视图解析和视图渲染。
- 执行afterCompletion方法。

Spring MVC拦截器的开发步骤如下：

1. 开发拦截器：

   实现handlerInterceptor接口，从三个方法中选择合适的方法，实现拦截时要执行的具体业务逻辑。

   ```java
   public class MyInterceptor implements HandlerInterceptor{
   
           /*preHandle 方法：会在控制器(controller)前执行，返回值表示是否中断后续执行，当返回值为true时表示继续向下执行，为false时会中断后续所有操作；*/
   	@Override
   	public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler)
   			throws Exception {
   		// TODO Auto-generated method stub
   		
   		System.out.println("preHandle---------------->运行了");
   		// 返回值为false的时候不运行下面两个方法
   		return true;
   	}
   
   	/*postHandle 方法：会在控制器方法调用之后，且解析视图之前执行。可以通过此方法对请求域中的模型和视图做出进一步的修改；*/
   	@Override
   	public void postHandle(HttpServletRequest request, HttpServletResponse response, Object handler,
   			ModelAndView modelAndView) throws Exception {
   		// TODO Auto-generated method stub
   		System.out.println("postHandle---------------->运行了");
   	}
   
           /*afterCompletion 方法：会在整个请求完成，即视图渲染结束之后执行。可以通过此方法实现一些资源清理、记录日志信息等工作。*/
   	@Override
   	public void afterCompletion(HttpServletRequest request, HttpServletResponse response, Object handler, Exception ex)
   			throws Exception {
   		// TODO Auto-generated method stub
   		System.out.println("afterCompletion---------------->运行了");
   	}
   }
   ```

   

2. 注册拦截器：

   定义配置类，并让它实现WebMvcConfigurer接口，在接口的addInterceptors方法中，注册拦截器，并定义该拦截器匹配哪些请求路径。

   ```java
   @Configuratio
   public class MyWebMvcConfig implements WebMvcConfigurer{
   	/**
   	 * 拦截器配置
   	 */
   	@Override
   	public void addInterceptors(InterceptorRegistry registry) {
   		// TODO Auto-generated method stub
   		registry.addInterceptor(new MyInterceptor())
   		// 拦截路劲
   		.addPathPatterns("/**")
   		// 排除路径
   		.excludePathPatterns("/excludeInterceptor");
   	}
   	
   }
   ```

### 怎么去做请求拦截？

如果是对Controller拦截，则可以使用Spring MVC的拦截器。

如果是对所有的请求（如访问静态资源的请求）进行拦截，则可以使用Filter。

如果是对除了Controller之外的其他Bean的请求进行拦截，则可以使用Spring AOP。

### **MVC流程，@RequestMapping的注解具体怎么实现的？**

  1.Spring扫描所有的Bean

  2.遍历这些bean，依次判断是否是处理器，并检测其HandlerMethod

  3.遍历Handler中的所有方法，找出其中被@RequestMapping注解标记的方法。

  4.获取方法method上的@RequestMapping实例

  5.检查方法所属的类有没有@RequestMapping注解

  6.将类和方法的RequestMapping结合

  7.当请求到达时，去UrlMap中找匹配的Url，以及获取对应mapping实例，然后去handerMethods中获取匹配HandlerMethod实例。

  8.将RequestMappingInfo实例以及处理方法注册到缓存中。

### **MVC自动装配流程**

![img](https://img-blog.csdnimg.cn/20210426131007375.png)

### **Spring框架中用到了那些设计模式？**

1. 简单工厂：由一个工厂类根据传入的参数，动态决定应该创建哪一个产品类

​		体现：BeanFactory根据传入唯一标识符获取Bean对象  getBean

2. 工厂方法：实现了factoryBean接口，重写getObject()方法，spring再调用getBean()方法时，返回getObject()方法返回的bean
3. 单例模式：保证一个类仅有一个实例，并提供一个访问它的全局访问点
4. 适配器模式：spring定义了一个适配器接口，使得每一种controller都有一种适配器实现类，让适配器代替controller执行相应方法
5. 动态代理模式：aop使用动态代理产生代理类
6. 观察者模式：监听器
7. 策略者模式：resource接口

## BeanFactory和ApplicationContext有什么区别

ApplicationContext，它是容器启动时，一次性创建了所有的Bean、占空间，继承MessageSource，因此支持国际化。

BeanFactory采用的是延迟加载形式注入Bean的，使用才实例化。

## **Spring、SpringMVC、SpringBoot、SpringCloud的联系与区别**

Spring:一个轻量级的控制反转和面向切面的容器。

SpringMVC: MVC 框架提供了模型-视图-控制的体系结构和可以用来开发灵活、松散耦合的 web 应用程序的组件

SpringBoot: 它基于Spring4.0设计，不仅继承了Spring框架原有的优秀特性，而且还通过**简化配置来进一步简化了Spring应用的整个搭建和开发过程**。另外SpringBoot通过集成大量的框架使得依赖包的版本冲突，以及引用的不稳定性等问题得到了很好的解决。

SpringCloud: 它利用Spring Boot的开发便利性巧妙地简化了分布式系统基础设施的开发，如服务发现注册、配置中心、消息总线、负载均衡、断路器、数据监控等，都可以用Spring Boot的开发风格做到一键启动和部署。

联系与区别：Spring提供IOC和AOP的容器，并具有强大的扩展功能；Springmvc在上面拓展了WEB开发，基于Servlet的一个MVC框架，通过XML配置，统一开发前端视图和后端逻辑；SpringBoot专注于微服务方面的接口开发，和前端解耦，同时也解决了Spring配置非常复杂，各种XML、Servlet处理起来比较繁琐，默认优于配置，简化了SpringMVC的配置流程；SpringCould更关注全局微服务的整合和管理，相当于管理多个springBoot框架的单体微服务。

## **SpringCloud微服务治理**

![img](https://img-blog.csdnimg.cn/20210426131033794.png)

![img](https://img-blog.csdnimg.cn/20210426131038256.png)

![img](https://img-blog.csdnimg.cn/20210426131043820.png)

![img](https://img-blog.csdnimg.cn/20210426131049319.png)

有了微服务，那么我们就需要去管理他们，然后就会有很大一堆方法了。

![img](https://img-blog.csdnimg.cn/20210426131053855.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwMjYyMzcy,size_16,color_FFFFFF,t_70)

**网关**就是整个整体的守门人；**日志采集，追踪工具，服务注册发现**都是用来**采集信息**的；然后需要**监控平台**来展现这些采集的信息，并进行监控和分析。最后根据分析的结果采取**治理策略**，有的服务快撑不住了要限流，有的服务坏了要熔断，并且还能够及时的调整这些服务的配置。

![img](https://img-blog.csdnimg.cn/20210426131058314.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwMjYyMzcy,size_16,color_FFFFFF,t_70)

# SpringBoot

## 说说你对Spring Boot的理解

从本质上来说，Spring Boot就是Spring，它做了那些没有它你自己也会去做的Spring Bean配置。Spring Boot使用“习惯优于配置”的理念让你的项目快速地运行起来，使用Spring Boot很容易创建一个能独立运行、准生产级别、基于Spring框架的项目，使用Spring Boot你可以不用或者只需要很少的Spring配置。

Spring Boot本身并不提供Spring的核心功能，而是作为Spring的脚手架框架，以达到快速构建项目、预置三方配置、开箱即用的目的。Spring Boot有如下的优点：

- 可以快速构建项目；
- 可以对主流开发框架的无配置集成；
- 项目可独立运行，无需外部依赖Servlet容器；
- 提供运行时的应用监控；
- 可以极大地提高开发、部署效率；
- 可以与云计算天然集成。

## Spring Boot Starter有什么用？（Spring Boot项目是如何导入包的？）

Spring Boot通过提供众多起步依赖（Starter）降低项目依赖的复杂度。起步依赖本质上是一个Maven项目对象模型（Project Object Model, POM），定义了对其他库的传递依赖，这些东西加在一起即支持某项功能。很多起步依赖的命名都暗示了它们提供的某种或某类功能。

举例来说，你打算把这个阅读列表应用程序做成一个Web应用程序。与其向项目的构建文件里添加一堆单独的库依赖，还不如声明这是一个Web应用程序来得简单。你只要添加Spring Boot的Web起步依赖就好了。

## Spring Boot的启动流程

Spring Boot项目创建完成会默认生成一个名为 *Application 的入口类，我们是通过该类的main方法启动Spring Boot项目的。在main方法中，通过SpringApplication的静态方法，即run方法进行SpringApplication类的实例化操作，然后再针对实例化对象调用另外一个run方法来完成整个项目的初始化和启动。

SpringApplication调用的run方法的大致流程，如下图：

![img](https://uploadfiles.nowcoder.com/images/20220224/4107856_1645694256551/4ECC3AECD1D8D2B62421E2D3453DC465)

其中，SpringApplication在run方法中重点做了以下操作：

- 获取监听器和参数配置；
- 打印Banner信息；
- 创建并初始化容器；
- 监听器发送通知。

## **springBoot核心注解，自动装配原理**

springboot会自动将一些配置类的bean注册进IOC容器

**核心注解**

说到springboot的核心注解，肯定是@springBootApplication注解当之无愧了。这个注解里面有三个注解，我一个一个说：

**1.@springbootConfiguration**

用来代替 applicationContext.xml配置文件，所有这个配置文件里面能做到的事情都可以通过这个注解所在类来进行注册。

**2.@ComponentScan**

用来代替配置文件中的 component-scan 配置，开启组件扫描，即自动扫描包路径下的 @Component 注解进行注册 bean 实例到 context 中。

**3.@EnableAutoConfiguration**

用来提供自动配置

@EnableAutoConfiguration里面包含了@Import({AutoConfigurationImportSelector.class})，其中的AutoConfigurationImportSelector类的selectImports() 方法从MATA-INF/spring.factories文件中                                                  //找到EnableAutoConfiguration配置，再去加载各种自动配置

加载注册的各种AutoConfiguration类，当某个AutoConfiguration类满足其注解@Conditional指定的生效条件（Starters提供的依赖、配置或Spring容器中是否存在某个Bean等）时，实例化该AutoConfiguration类中定义的Bean（组件等），并注入Spring容器，就可以完成依赖框架的自动配置。

**自动装配**

![img](https://img-blog.csdnimg.cn/20210426131103531.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwMjYyMzcy,size_16,color_FFFFFF,t_70)

![img](https://img-blog.csdnimg.cn/20210426131108616.png)

## Springboot注解

**@SpringBootApplication**注解：

在Spring Boot入口类中，唯一的一个注解就是@SpringBootApplication。它是Spring Boot项目的核心注解，用于开启自动配置，准确说是通过该注解内组合的@EnableAutoConfiguration开启了自动配置。

**@EnableAutoConfiguration**注解：

@EnableAutoConfiguration的主要功能是启动Spring应用程序上下文时进行自动配置，它会尝试猜测并配置项目可能需要的Bean。自动配置通常是基于项目classpath中引入的类和已定义的Bean来实现的。在此过程中，被自动配置的组件来自项目自身和项目依赖的jar包中。

**@Import**注解：

**@EnableAutoConfiguration**的关键功能是通过@Import注解导入的ImportSelector来完成的。从源代码得知@Import(AutoConfigurationImportSelector.class)是@EnableAutoConfiguration注解的组成部分，也是自动配置功能的核心实现者。

**@Conditional**注解：

@Conditional注解是由Spring 4.0版本引入的新特性，可根据是否满足指定的条件来决定是否进行Bean的实例化及装配，比如，设定当类路径下包含某个jar包的时候才会对注解的类进行实例化操作。总之，就是根据一些特定条件来控制Bean实例化的行为。

@Conditional衍生注解：

在Spring Boot的autoconfigure项目中提供了各类基于@Conditional注解的衍生注解，它们适用不同的场景并提供了不同的功能。通过阅读这些注解的源码，你会发现它们其实都组合了@Conditional注解，不同之处是它们在注解中指定的条件（Condition）不同。

- @ConditionalOnBean：在容器中有指定Bean的条件下。
- @ConditionalOnClass：在classpath类路径下有指定类的条件下。
- @ConditionalOnCloudPlatform：当指定的云平台处于active状态时。
- @ConditionalOnExpression：基于SpEL表达式的条件判断。
- @ConditionalOnJava：基于JVM版本作为判断条件。
- @ConditionalOnJndi：在JNDI存在的条件下查找指定的位置。
- @ConditionalOnMissingBean：当容器里没有指定Bean的条件时。
- @ConditionalOnMissingClass：当类路径下没有指定类的条件时。
- @ConditionalOnNotWebApplication：在项目不是一个Web项目的条件下。
- @ConditionalOnProperty：在指定的属性有指定值的条件下。
- @ConditionalOnResource：类路径是否有指定的值。
- @ConditionalOnSingleCandidate：当指定的Bean在容器中只有一个或者有多个但是指定了首选的Bean时。
- @ConditionalOnWebApplication：在项目是一个Web项目的条件下。