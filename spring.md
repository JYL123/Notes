
## Spring and Spring Boot 

`Spring framework` is a java platform that provides comprehensive infrastructure support for developing java applications. Spring handles the infrastructure so you can focus on your application. Spring enables you to build applications from "plain old java objects" (POJOs) and to apply enterprise services non-invasively to POJO.

* Spring MVC: web layer 
* Spring Core: Business layer
* Spring Data: data & layer

### Spring basics
* Features of Spring Framework 
 * Dependency injection 
 * IoC container (Bean Factory & Application Contex) 
 * Autowiring 
 * Component scanning 

* @SpringBootApplication to the main class
* @Autowired: auto injection by spring framework; a field injection, a constructor injection, a setter injection
* @Component: lifecycle will be handled by spring; for class
* @Primary: injection priority 
* @Bean: injetction section we handed to spring framework to handle; for method

### Spring advantages
* Flexible architecture
* Loosely coupled design 
* Easy to unit test spring code
* Spring is modular (spring consists of features organized into about 20 modules)

### Spring Boot
* Spring boot framwork is an extension of spring framework, abd does not replace spring framework. Spring boot is focused on shortening the spring code length and providing the developer of runnign the spring application. Spring boot tries to make the use of Spring framework easier.
* Uses embedded Tomcat, Jetty or Undertow servers
* @postconstruct
* @predestroy
* @configuration: a bean, and how it is constructed
