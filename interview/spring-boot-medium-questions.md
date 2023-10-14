
1. **Explain the term ‘Spring Boot’?**
   - It is a Spring module that offers Rapid Application Development to Spring framework. Spring module is used to create an application based on Spring framework which requires to configure few Spring files.

2. **Mention some advantages of Spring Boot?**
   - Here are some major advantages of using spring-boot:
     - Helps you to create a stand-alone application, which can be started using java.jar.
     - It offers pinpointed‘started' POMs to Maven configuration.
     - Allows you to Embed Undertow, Tomcat, or Jetty directly.
     - Helps you to configure spring whenever possible automatically.

3. **How to create a Spring Boot application using Spring Initializer?**
   - It is a web tool provided by Spring on its official website. However, you can also create Spring Boot project by entering project details.

4. **Name the features of using Spring Boot?**
   - Features of using Spring Boot are:
     - Starter dependency
     - Auto-configuration
     - Spring initializer

5. **Explain different phases of RAD model?**
   - This is a frequently asked job interview. Various phases of RAD mode are:
     - Business Modeling: Based on the flow of information and distribution between various business channels, the product is designed.
     - Data Modeling : The information collected from business modeling is refined into a set of data objects that are significant for the business.
     - Application Generation: Automated tools are used for the construction of the software, to convert process and data models into prototypes.

6. **What is RAD model?**
      - RAD or Rapid Application Development process is an adoption of the waterfall model; it targets developing software in a short period. RAD follow the iterative

        SDLC RAD model has the following phases:

         - Business Modeling
         - Data Modeling
         - Process Modeling
         - Application Generation
         - Testing and Turnover

7. **What are the commands to run and stop Spring Boot executable jar file?**
   - You need to open cmd or shell window command and use

           java -jar
       Example

          $ java -jar myproject-0.0.1-SNAPSHOT.jar
        To stop use ctrl+C         
     
8. **How can you change JDK version in Spring Boot?**
   - To change the JDK version in Spring Boot, you can overwrite it by adding a java. version property

   tag as given:
 
        1.8

9. **What is the process that you need to follow to run Spring Boot application on the custom port?**
   - In order to run a Spring Boot application, you require to put server.port properties in application.properties. For example, server.port=8050     

10. **What is Spring Boot starter? How is it useful?**
    - Spring Boot has many starters. They are a set of convenient dependency descriptors. Starter allows you to include these descriptors in your pom.xml.

        For example, If you want to work with Spring MVC, you can include “spring–boot–starter–web” as a dependency in pom.xml.

11. **Can you use Spring Boot with applications which are not using Spring?**
    - No, it is not possible as Spring Boot is limited to Spring application only.

12. **What is the name of the configuration file which you can use in Spring Boot?**
    - The configuration file used in Spring Boot projects is called application.properties. It is an important file which allows you to override your default configurations.

13. **What is DevTools in Spring Boot?**
    - Spring Boot DevTools helps you to increase the productivity of the developer. So, you don't require to redeploy your application every time you make the changes. It allows the developer to reload changes without the need of restarting of the server.

14. **What are the important features of Reactjs?**
    - Important features of Reactjs are:
        - Web Development
        - Spring Application
        - Application occasions and listeners
        - Admin highlights
        - YAML Support
        - Type-safe Configuration
        - Externalized Configuration
        - Properties Files
        - Logging and Security

15. **What are the essential components of Spring Boot?**
    - The important components of Spring Boot are:
        - Spring Boot Starter
        - Spring Boot autoconfiguration
        - Spring Boot Actuator
        - Spring Boot CLI  

16. **How are properties defined? Where?**
    - You can define properties in the application.properties file exists in the classpath.

    Example: configure default DataSource bean

    database.host=localhost

17. **What is spring-boot-starter-parent?**
    - It is a special starter which makes Gradle or Maven dependency-management easy by adding jars to your classpath.

18. **How to enable HTTP/2 supports in Spring Boot?**
    - User can enable HTTP/2 support by using server.http2.enabled configuration property.

19. **What is a Spring Boot Actuator?**
    - Spring Boot Actuator allows you to monitor and manage your application when you want to push it for the production. It helps you to control your application by using HTTP endpoints.

20. **What is the command to run Spring Boot application to custom port?**
    - In application.properties, add following property.

          server.port = 8181

21. **How can you access a value defined in the application? What is properties file in Spring Boot?**
    - Use the @Value annotation to access the properties which is defined in the application -properties file.

            @Value("${custom.value}")
            private String customVal;

22. **What is the primary difference between Spring and Spring Boot?**
    - Spring is a web application development framework based on Java. On the other hand Spring Boot is an extension of the spring framework which eliminated the boilerplate onfiguration
    required for setup a Spring application.

23. **Explain Spring Boot Admin?**
    - Spring Boot admin is a community project which helps you to manage and monitor your Spring Boot applications.

24. **How can you connect Spring Boot to the database using JPA?**
    - Spring Boot supports spring-boot-data-JPA start, which helps you to connect spring application with a relational database.

25. **Explain @RestController annotation in Spring Boot?**
    - The @RestController annotation helps you to add @ResponseBody and @Controller annotations to the class.

   You can also import org.springframework.web.bind.annotation package in your file.

26. **Define the term Spring Initializer?**
    - Spring initializer is a web application which can create an initial project structure for you.

27. **Explain Spring CLI?**
    - Spring CLI is used for writing in Groovy Spring Boot application, which helps you to concise code.

28. **Where can you define properties in Spring Boot application?**
    - You can define properties of Spring Boot into a file called application.properties. It helps you to create this file manually, or you can use Spring Initializer to create this file.

29. **What are embedded containers support by Spring?**
    - Spring Boot support the main three embedded containers:
    1) Tomcat
    2) Jetty
    3) Undertow.
    
    By default, it uses Tomcat as an embedded container.

30. **Explain thymeleaf in Spring Boot?**
    - Thymelaf is a server-side Java template engine for a webapplication. It helps you to bring elegant natural templates to your web application.     

31. **What are the Spring Boot properties?**
    - Spring Boot offers various properties which can be specified inside our project's application.properties file. It helps you to set values like a server-port number, database
    connection configuration, etc.

32. **What is the main difference between JPA and Hibernate?**
    - The main difference between both of them is that JPA is a specification/Interface, whereas
    Hibernate is only JPA implementations.

33. **What is a shutdown in the actuator?**
    - A shutdown is an endpoint that helps application to be shut down properly. This feature is not enabled by default.

    However, you can use it by setting command: management.endpoint.shutdown.enabled=true in
    your application.properties file.

34. **Is it possible to replace or override the Embedded Tomcat server in Spring Boot?**
    - Yes, it is possible to replace the Embedded Tomcat with any other servers by using the starter dependencies. For that, you can use spring-boot-starter-jetty or as a dependency for according you to your need.

35. **Can you disable the default web server in the Spring Boot application?**
    - Yes, we can disable the default web server by using application.properties to configure the web application type.

36. **How do you Add, Filter to an application?**
    - There are three methods to add filter to Spring Boot application:
        - By implementing Filter interface.
        - Using FilterRegistrationBean.
        - Using MVC controller.

37. **What are Spring Boot Starter Projects?**
    - Starters in Spring Boot are a set of convenient descriptors that are included in Spring Boot applications. It comes with a variety of Spring-related technology which makes the entire process of the application development much easier.

38. **What is @pathVariable?**
    - @PathVariable annotation helps you to extract information from the URI directly.   

39. **What is Swagger2?**
    - Swagger is used to describing the structure of APIs. Swagger 2 is an open-source service provided in Spring Boot which makes it easier for the machines to find out the structure of APIs like RESTful Web services.

40. **What are different environments for enterprise application development?**
    - Dev
    - QA
    - Stage
    - Production
41. **What are the major differences between RequestMapping and GetMapping?**
    - RequestMapping can be used with GET, POST, PUT, and many other request methods using the method attribute on the annotation. Whereas GetMapping is only an extension of RequestMapping, which helps you to improve clarity on requests.

42. **How can you define properties in Spring Boot?**
    - You can define properties in Spring Boot with the help of the application.properties file which exists in a classpath of the application as follows.

43. **How to create a Spring Boot project using Maven?**
    - Use any of the following methods to create a project.
        - Spring Initializr
        - Spring Boot CLI
        - Spring Starter Project Wizard

44. **What is the use of profiles in Spring Boot?**
    - Profiles are used to separate various parts of your spring application configuration and make it only available in certain environments.

45. **How to change tomcat HTTP port?**
    - To change the tomcat HTTP port, you have to change default HTTP property in application.properties file.

46. **What is LiveReload in Spring Boot?**
    - LiveReload is a spring-boot-devtools module that includes LiveReload server to trigger a browser refresh when a resource is changed. LiveReload server extensions are available freeware for Firefox, Chrome,and Safari.             

47. **What are the major benefits of spring Externalized Configuration?**
    - Externalized Configuration helps to work with the same code in different environments.Developers can use YAML files, properties files, command-line arguments, and environment variables to externalize configuration.
48. **What do you mean by hot-swapping in Spring Boot?**
    - It is a way to reload the changes without restarting Tomcat, or Jetty server. Eclipse and Many other IDEs support bytecode hot swapping. If you make any changes that don’t affect the method signature, it should reload without side effect.
49. **Explain Auto-Configuration in Spring Boot?**
    - Auto-configuration is used to configure Spring application automatically based on dependencies of classpath parameter. It makes development faster and easier.
50. **What is the meaning of Aspect-Oriented Programming (AOP)?**
    - Aspect-Oriented Programming supplements Object-Oriented Programming that aims to increase modularity. AOP breaks program logic into various parts, which are called concerns.
51. **How to enable logging in Spring Boot?**
    - In order to enable debug logging, you can specify --debug while starting the application from the command prompt.
52. **Explain overriding default properties in Spring Boot application?**
    - Spring Boot has lots of properties that can be easily overridden by specifying them in application.properties.
53. **Explain Docker in Spring Boot?**
    - It is a tool designed to create, deploy, and run a project by using containers.
54. **Define ELK stack?**
    - The ELK Stack is made of three open-source products: 1. Elasticsearch, 2. Logstash, and 3. Kibana.
      - **Elasticsearch:** It is a NoSQL database which is based on the open-source search engine
     called Lucene.
      - **Logstash:** It is a data processing pipeline tool which accepts inputs from sources, performs different transformations, and exports the data to targets.
      - **Kibana:** Kibana helps users to visualize data with graphs and chart in Elasticsearch.   

55. **How to handle exception in Spring Boot?**
    - Spring Boot provides a very useful way to handle exceptions using @ControllerAdvice annotation.

56. **Explain caching ?**
    - Caching is a memory are that temporary stores frequently accessed data that is otherwise expensive to get or compute.

57. **What is Cross-Site Request Forgery attack?**
    - Cross-Site Request Forgery attack or one-click attack is an attack that forces other users to execute malicious commands on the application. CSRF attack specifically targets state-changing requests.

58. **Define apache freemarker?**
    - Freemarker is a Java-based template used to generate plain text, emails, HTML file, etc.
59. **What is mean by spring batch?**
    - Spring Boot Batch provides code reusability which is important when working with large numbers of records, including transaction management, logging, skipping, job processing statistics, and job restarts.
60. **Explain Apache Kafka?**
    - Apache Kafka is an open-source messaging platform. LinkedIn develops it. Apache Kafka enables the user to build distributed applications and handle real-time data feeds. Kafka is suitable for both offline and online messaging.




