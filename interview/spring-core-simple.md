#### 1. What is Spring Framework?
Spring is an open-source Java framework that provides a comprehensive programming and configuration model for modern Java-based enterprise applications.
It supports features like dependency injection (DI), aspect-oriented programming (AOP), transaction management, and integration with other frameworks.

#### 2. What is Spring Core?
Spring Core is the central part of the Spring Framework responsible for providing the Inversion of Control (IoC) and Dependency Injection (DI) features.
It helps manage Java objects from creation to destruction, removing the need for manual instantiation.

#### 3.What is Dependency Injection (DI) in Spring?
Dependency Injection is a design pattern where the dependencies of an object are provided externally rather than creating them inside the class.
Example: Instead of new StudentService(), Spring injects the object via XML, annotations, or Java configuration.

#### 4. What are the types of Dependency Injection in Spring?
Constructor Injection – Dependencies are passed via constructor arguments.

Setter Injection – Dependencies are passed via setter methods.

Field Injection – Dependencies are injected directly into fields (via @Autowired).

#### 5.What is Inversion of Control (IoC)?
IoC is a principle where the control of creating and managing objects is transferred from the program to the Spring IoC container.
In other words, Spring creates and manages beans instead of the developer manually instantiating them.

#### 6.What is a Spring Bean?
A bean is a Java object that is managed by the Spring IoC container. Beans are created, configured, and destroyed by the container.

#### 7.What is the Spring IoC Container?

The IoC container is responsible for managing the lifecycle and configuration of application objects (beans).
Types:

BeanFactory – Basic container, lazy initialization.

ApplicationContext – Advanced container with additional features like event propagation and internationalization.

#### 8.Difference between BeanFactory and ApplicationContext?

| **BeanFactory**            | **ApplicationContext**          |
| -------------------------- | ------------------------------- |
| Basic container            | Advanced container              |
| Lazy loading               | Eager loading by default        |
| No built-in event handling | Supports events, messages, etc. |
| Slower in large apps       | Faster in large apps            |

#### 9.How do you define a bean in Spring?

XML configuration:

```typescript
<bean id="studentService" class="com.example.StudentService"/>
```

Annotation-based:
```typescript
@Component
public class StudentService {}
```

Java Config:
```typescript
@Bean
public StudentService studentService() {
    return new StudentService();
}
```
#### 10.What is the default scope of a Spring Bean?
Singleton – Only one instance is created and shared across the application context.

#### 11.What are the bean scopes in Spring?

singleton – One instance per Spring container.

prototype – New instance each time it’s requested.

request – One instance per HTTP request (web apps).

session – One instance per HTTP session.

application – One instance per ServletContext.

websocket – One instance per WebSocket.

#### 12.What are the different ways to configure Spring Beans?

XML-based configuration

Annotation-based configuration (@Component, @Autowired)

Java-based configuration (@Configuration, @Bean)

#### 13.What is Autowiring in Spring?
Autowiring allows Spring to automatically resolve and inject bean dependencies without explicit configuration.

Types:

no – No autowiring.

byName – Matches property name with bean ID.

byType – Matches by class type.

constructor – Uses constructor injection.

@Autowired – Annotation-based autowiring.

#### 14.Difference between @Component, @Service, @Repository, and @Controller?
All are specializations of @Component:

@Component – Generic bean.

@Service – Business logic layer bean.

@Repository – DAO layer bean (with exception translation).

@Controller – Web controller bean.

#### 15.What is @Configuration in Spring?

@Configuration indicates that the class contains bean definitions. Methods annotated with @Bean return objects that will be managed by Spring.

#### 16.What is @Bean annotation?
@Bean is used inside a @Configuration class to explicitly declare a bean and its configuration.

#### 17.What is @Autowired annotation?

@Autowired automatically injects a dependency into a bean’s property, constructor, or method.
It can be combined with @Qualifier to specify which bean to inject if multiple beans of the same type exist.

#### 18.What is the lifecycle of a Spring Bean?

Instantiation – Bean is created.

Populate properties – Dependencies injected.

BeanNameAware & BeanFactoryAware callbacks

Before Initialization – BeanPostProcessor methods.

Custom init-method

After Initialization – BeanPostProcessor post-init.

Usage – Bean is used in the app.

Destroy – DisposableBean or custom destroy-method.

#### 19.What is a BeanPostProcessor in Spring?

It allows custom modification of beans before and after initialization.
Example: Logging, modifying properties, creating proxies.

#### 20.What is the difference between @Qualifier and @Primary?
@Qualifier – Used with @Autowired to specify which bean to inject.

@Primary – Marks a bean as the default when multiple beans of the same type exist.

#### 21. What is the difference between ApplicationContext and WebApplicationContext?

ApplicationContext – Used in standalone applications.

WebApplicationContext – Specialized version for web apps, integrates with ServletContext.

#### 22.What is the role of @Lazy annotation?

@Lazy tells Spring to create a bean only when it is requested, instead of at startup (default eager initialization).

#### 23.What is the difference between eager and lazy initialization?
Eager – Beans are created during application startup.

Lazy – Beans are created only when first requested.

#### 24.What is @Scope annotation in Spring?
@Scope defines the scope of a Spring bean (singleton, prototype, request, session, etc.).

```typescript
@Scope("prototype")
@Component
public class MyBean {}
```
#### 25.What is Spring Expression Language (SpEL)?
SpEL is a powerful expression language that can be used in Spring to dynamically evaluate expressions at runtime.
```typescript
@Value("#{2 + 2}")
private int sum;

```
