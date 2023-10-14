

1. **What is Spring Boot, and how does it differ from the core Spring Framework?**
   - Spring Boot is an extension of the Spring Framework that simplifies the setup and development of Spring-based applications. It provides default configurations and eliminates the need for a lot of boilerplate code.

2. **What are the key advantages of using Spring Boot?**
   - Spring Boot offers advantages such as rapid development, auto-configuration, embedded servers, easy integration with databases, and a wide range of community-contributed libraries.   
          
3. **Explain the concept of Spring Boot Auto-Configuration.**
   - Spring Boot's auto-configuration automatically configures beans based on the project's dependencies and properties. It simplifies the configuration process by providing sensible defaults.

4. **What is the purpose of the `@SpringBootApplication` annotation?**
   - The `@SpringBootApplication` annotation is used to mark the main application class and enables auto-configuration, component scanning, and the setup of Spring Beans.

5. **What is the Embedded Container in Spring Boot, and why is it beneficial?**
   - Spring Boot includes embedded containers (e.g., Tomcat, Jetty) that allow you to run your application as a standalone JAR or WAR file without the need for an external application server.

## Spring Boot Configuration

6. **How do you configure application properties in Spring Boot?**
   - Application properties can be configured using the `application.properties` or `application.yml` files. Properties can also be defined programmatically using the `@ConfigurationProperties` annotation.

7. **Explain the purpose of Spring Boot Profiles.**
   - Spring Boot profiles allow you to define different configurations for different environments (e.g., development, production) and activate them using properties or command-line arguments.

8. **What is the purpose of the `application.properties` or `application.yml` file in Spring Boot?**
   - These files are used for external configuration of a Spring Boot application. They contain properties that can be easily customized for different environments.

9. **How can you access properties defined in `application.properties` or `application.yml`?**
   - Properties can be accessed using the `@Value` annotation or by using the `@ConfigurationProperties` annotation to bind properties to Java objects.

## Spring Boot Annotations and Components

10. **Explain the purpose of the `@RestController` annotation in Spring Boot.**
    - The `@RestController` annotation combines `@Controller` and `@ResponseBody`, making it easier to create RESTful web services that return JSON or XML responses.

11. **What is the role of the `@Service` annotation in Spring Boot?**
    - The `@Service` annotation is used to mark a class as a service component, typically containing business logic. It is automatically detected by component scanning.

12. **When should you use the `@Autowired` annotation in Spring Boot?**
    - The `@Autowired` annotation is used for automatic dependency injection, allowing Spring to automatically inject dependencies into beans.

13. **Explain the purpose of the `@ComponentScan` annotation in Spring Boot.**
    - The `@ComponentScan` annotation is used to specify the base package(s) for component scanning. Spring Boot scans these packages to discover and register beans.

## Spring Boot Data Access

14. **What is Spring Data JPA, and how does it simplify data access in Spring Boot?**
    - Spring Data JPA is a part of the Spring Data project that simplifies data access through the use of JPA (Java Persistence API). It provides repository interfaces and automatic CRUD methods.

15. **How do you create a custom query method in a Spring Data JPA repository?**
    - Custom query methods can be defined in a repository by following a specific naming convention (e.g., `findByPropertyName`). You can also use the `@Query` annotation for more complex queries.

16. **What is Spring Boot's support for NoSQL databases, and can you name some NoSQL databases compatible with Spring Boot?**
    - Spring Boot provides support for various NoSQL databases, including MongoDB, Redis, Cassandra, and Neo4j. It offers specialized modules for these databases.

1. **Is excluding package without using the basePackages filter is possible? How?**
    - Yes. It is possible to exclude package without using the basePackages filter by simply using the exclude attribute while using the @SpringBootApplication annotation.

2. **List out benefits of using the JavaConfig method?**
    - Following are the benefits of JavaConfig method
        - User can take benefit of object-oriented configuration.
        - Spring Boot configuration improves the efficiency of web-based application by eliminating complex XML configuration.
3. **Explain steps to deploy an application on virtual machine?**
    - Below are the steps to deploy application on virtual machine.
        - Install Java.
        - Install the Application Server.
        - Deploy the application war file.

4. **List out some of the Spring Boot Starters?**
    - Different Spring Boot Starters are as follows:
        - Security
        - Parent
        - web
        - Thymeleaf
        - Freemarker

5. **Describe the flow of HTTPS requests through the Spring Boot application.**
    - The flow of HTTPS requests through a Spring Boot application is as follows:
        - 1.The client (e.g., a web browser) initiates an HTTPS request to the server.
        - 2.The server’s SSL/TLS stack establishes a secure connection with the client.
        - 3.The client sends the request headers and body to the      server.
        - 4.The server decrypts the request headers and body.
        - 5.The server handles the request and generates a response.
        - 6.The server encrypts the response headers and body.
        - 7.The server sends the response back to the client.
        - 8.The client decrypts the response headers and body.

6. **Is it possible to change the port of the embedded Tomcat server in Spring Boot?**
    - Yes, it is possible to change the port of the embedded Tomcat server in a Spring Boot application.
    - A simple way is to set the server. port property in your application’s application.properties file. For example, to set the port to 8081, you would add the following property to your application.properties file:
    
          server.port=8081  

7. **What is the default port of Tomcat in spring boot?**
    - The default port of the embedded Tomcat server in Spring Boot is 8080.
    - You can change the default port by setting the **server. port** property in your application’s application.properties file.           

8. **Can we disable the default web server in the Spring Boot application?**
    - Yes, you can disable the default web server in the Spring Boot application.
    - To do this, you need to set the server.port property to -1 in your application’s application.properties file.    

9. **How to disable a specific auto-configuration class?**
    - To disable a specific auto-configuration class in a Spring Boot application, you can use the
    **@EnableAutoConfiguration** annotation with the exclude attribute. This allows you to exclude the auto-configuration class from being applied during the application startup process.
    - For example, the following code would exclude the

            org.springframework.boot.autoconfigure.security.servlet.SecurityAutoConfiguration class
                
            @SpringBootApplication
            @EnableAutoConfiguration(exclude = { SecurityAutoConfiguration.class }) 
            public class MyApplication { 
                public static void main(String[] args) 
                { 
                    SpringApplication.run(MyApplication.class, args); 
                } 
            }    

10. **Explain CORS in Spring Boot?**
    - CORS stands for Cross-Origin Resource Sharing is a mechanism implemented by browsers and helps users to authorize cross-domain requests. This mechanism serves as an alternative to less secure and less powerful hacks of the kinds of IFrame or JSONP.
11. **Explain different types of dependency injection?**
    - There are two types of dependency injection in Spring Boot. They are as follows:
      - **`Constructor based dependency injection:`** It is a technique in which one class object supplies the dependency of another object.
      - **`Setter-based dependency injection:`** It is a dependency injection in which the framework injects the primitive and string-based values using setter method.       

12. **What are the advantages of micro service?**
    - Following are the major advantages of micro service:
        - It makes development fast and easy.
        - Compatible with all container.
        - Reduce production time.
        - It's a lightweight model that supports a major business application.

13. **What is the default package in Spring Boot?**
    - A class without any package declaration is considered as a default package.

14. **Explain the difference between an embedded container and a WAR?**
     - The main difference between these two is:

        Embedded containers help you to run Spring Boot application as a JAR from the command prompt without setting up any web server, while to run a WAR you need first to set up Tomcat.

15. **Explain Spring MVC?**
    - It is a traditional web application framework which helps you to build a web application. This framework is similar to the framework of Struts.

16. **What is the use of `<set>` tag?**
    - This tag is used to write to inject java set using XML.

17. **What do you mean by aspect?**
    - It is a set of APIs which provides cross-cutting requirements.

18. **What is join point in Spring Boot?**
    - It is a program execution point like the handling of an exception or the execution of a method. In AOP, a join point is referred to as a method execution.

19. **How can you set active profile in Spring Boot?**
    - Follow the following methods to set an active profile in Spring Boot.
        - Pass this profile as an argument when you launch the Spring Boot application.
        - Set active the active profile in application.properties file.            
