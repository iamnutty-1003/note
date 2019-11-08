# 三、日志

## 4、日志使用

##### 2、指定配置

logging源码

logging>logback>base.xml中

~~~xml
<included>
	<include resource="org/springframework/boot/logging/logback/defaults.xml" />
	<property name="LOG_FILE" value="${LOG_FILE:-${LOG_PATH:-${LOG_TEMP:-${java.io.tmpdir:-/tmp}}}/spring.log}"/>
	<include resource="org/springframework/boot/logging/logback/console-appender.xml" />
	<include resource="org/springframework/boot/logging/logback/file-appender.xml" />
	<root level="INFO">
		<appender-ref ref="CONSOLE" />
		<appender-ref ref="FILE" />
	</root>
</included>
<!-- 配置了默认项 -->
~~~

添加自己的配置 直接加入logback-spring.xml或logback.xml

前者可以配置<dev> 等能被spring boot识别

# 四、Web开发

## 1、简介

## 2、SpringBoot对静态资源的映射规则

~~~java
        public void addResourceHandlers(ResourceHandlerRegistry registry) {
            if (!this.resourceProperties.isAddMappings()) {
                logger.debug("Default resource handling disabled");
            } else {
                Duration cachePeriod = this.resourceProperties.getCache().getPeriod();
                CacheControl cacheControl = this.resourceProperties.getCache().getCachecontrol().toHttpCacheControl();
                if (!registry.hasMappingForPattern("/webjars/**")) {
                    this.customizeResourceHandlerRegistration(registry.addResourceHandler(new String[]{"/webjars/**"}).addResourceLocations(new String[]{"classpath:/META-INF/resources/webjars/"}).setCachePeriod(this.getSeconds(cachePeriod)).setCacheControl(cacheControl));
                }

                String staticPathPattern = this.mvcProperties.getStaticPathPattern();
                if (!registry.hasMappingForPattern(staticPathPattern)) {
                    this.customizeResourceHandlerRegistration(registry.addResourceHandler(new String[]{staticPathPattern}).addResourceLocations(WebMvcAutoConfiguration.getResourceLocations(this.resourceProperties.getStaticLocations())).setCachePeriod(this.getSeconds(cachePeriod)).setCacheControl(cacheControl));
                }

            }
        }
~~~

### 1）webjars

![webjars](C:\Users\wangqi\Desktop\webjars.PNG)[webjars/**]

http://localhost:8080/webjars/jquery/3.4.1/jquery.js

### 2)"/**"访问当前的任何资源，静态资源的文件夹

~~~xml
"classpath:/META-INF/resources/", "classpath:/resources/",
"classpath:/static/", 
"classpath:/public/"
"/":当前项目的根路径
~~~

### 3)欢迎页静态资源文件夹下的所有index.html页面都被"/**"映射；

### 4)所有的**/favicon.ico都在静态资源文件夹下找

## 3、模板引擎

~~~java
public class ThymeleafProperties {
    private static final Charset DEFAULT_ENCODING;
    public static final String DEFAULT_PREFIX = "classpath:/templates/";
    public static final String DEFAULT_SUFFIX = ".html";
    private boolean checkTemplate = true;
    private boolean checkTemplateLocation = true;
    private String prefix = "classpath:/templates/";
    private String suffix = ".html";
    private String mode = "HTML";
~~~

只要我们把html文件放在templates下面就能被识别

### 语法规则

1)th:text 改变当前元素里的文本内容；

​	替换：任意html属性；来替换原生属性

~~~html
<div th:text="${hello}" th:id="">LSN</div>
~~~

2)表达式

${} 

#{} 获取国际化内容

@{}获取超链接地址

~~{}片段引用表达式

## 4、SpringMVC自动配置

### 29.1.1 Spring MVC Auto-configuration

Spring Boot provides auto-configuration for Spring MVC that works well with most applications.

以下是SpringBoot对SpringMVC的默认

- Inclusion of `ContentNegotiatingViewResolver` and `BeanNameViewResolver` beans.
  - 自动配置了ViewResolver(视图解析器：根据方法的返回值得到视图对象(view)，视图对象决定如何渲染(转发？重定向？))
  - 可以自己给容器中添加一个视图解析器
- Support for serving static resources, including support for WebJars (covered [later in this document](https://docs.spring.io/spring-boot/docs/current/reference/html/boot-features-developing-web-applications.html#boot-features-spring-mvc-static-content))).静态资源文件夹路径
- 自动注册了 `Converter`, `GenericConverter`, and `Formatter` beans.
  - `Converter`:转换器;public String hello(User user):类型转换使用Converter
  - `Formatter`格式化器;2019-09-24 ===Date;



- Support for `HttpMessageConverters` (covered [later in this document](https://docs.spring.io/spring-boot/docs/current/reference/html/boot-features-developing-web-applications.html#boot-features-spring-mvc-message-converters)).
  - `HttpMessageConverters`SpringMVC用来转换Http请求和响应的;User--Json
  - `HttpMessageConverters`是从容器中确定;获取所有的HttpMessageConverter。如果想要自己添加，只需要将自己的组件添加到容器中(@Bean @Component)
- Automatic registration of `MessageCodesResolver` (covered [later in this document](https://docs.spring.io/spring-boot/docs/current/reference/html/boot-features-developing-web-applications.html#boot-features-spring-message-codes)). 定义错误代码生成规则
- Static `index.html` support.
- Custom `Favicon` support (covered [later in this document](https://docs.spring.io/spring-boot/docs/current/reference/html/boot-features-developing-web-applications.html#boot-features-spring-mvc-favicon)).
- Automatic use of a `ConfigurableWebBindingInitializer` bean (covered [later in this document](https://docs.spring.io/spring-boot/docs/current/reference/html/boot-features-developing-web-applications.html#boot-features-spring-mvc-web-binding-initializer)).web数据自动绑定器
  - 我们可以自己配置` ConfigurableWebBindingInitializer`来替换默认的，只需要添加到容器

org.springframework.boot.autoconfigure. web 所有自动配置场景

If you want to keep Spring Boot MVC features and you want to add additional [MVC configuration](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/web.html#mvc) (interceptors, formatters, view controllers, and other features), you can add your own `@Configuration` class of type `WebMvcConfigurer` but **without** `@EnableWebMvc`. If you wish to provide custom instances of `RequestMappingHandlerMapping`, `RequestMappingHandlerAdapter`, or `ExceptionHandlerExceptionResolver`, you can declare a `WebMvcRegistrationsAdapter` instance to provide such components.

If you want to take complete control of Spring MVC, you can add your own `@Configuration` annotated with `@EnableWebMvc`.

### 2)扩展SpringMVC

```xml
    <mvc:view-controller path="/hello" view-name="success"/>
    <mvc:interceptors>
        <mvc:interceptor>
            <mvc:mapping path="/hello"/>
            <bean></bean>
        </mvc:interceptor>
    </mvc:interceptors>

```

~~编写一个配置类(@Configuration)，是WebMvcConfigurerAdapter类型；不能标注@EnableWebMvc~~

已经过时，直接实现WebMvcConfigurer接口就行  

原理：

​	1)WebMvcAutoConfiguration是SpringMVC的自动配置类

​	2)在做其他自动配置时会导入

## 5、如何修改SpringBoot的自动配置

模式：

### 	1)SpringBoot在自动配置很多组件的时候，优先配置用户自己配置的(@Bean @Component)，如果没有才自动配置；

