# Spring Boot Notes – Basics & Core Concepts

## 1. What is Spring?
- **Spring Framework** is a powerful, lightweight, and open-source framework for building Java applications.  
- It provides infrastructure support for developing **Java applications** with features like:  
  - **Dependency Injection (DI)** and **Inversion of Control (IoC)**  
  - **Aspect-Oriented Programming (AOP)**  
  - **Data Access Layer (JDBC, ORM integration)**  
  - **Transaction Management**  
  - **MVC Framework** for web applications  

### Key Features of Spring
- **Lightweight** – minimal overhead.  
- **Modular** – you can use only what you need.  
- **Loose Coupling** – achieved through Dependency Injection.  
- **Integration** – works with Hibernate, JPA, JDBC, JMS, and more.  
- **Testability** – makes unit testing and integration testing easier.  

---

## 2. What is Spring Boot?
- **Spring Boot** is an extension of the Spring Framework that simplifies application development.  
- It provides a **faster way to build production-ready applications** with minimal configuration.  
- Focuses on **convention over configuration** (sensible defaults).  

### Key Features of Spring Boot
1. **Auto-Configuration**  
   - Automatically configures beans and dependencies based on the project setup.  
   - Example: If `spring-boot-starter-web` is on the classpath, Spring Boot auto-configures a Tomcat server.  

2. **Starter Dependencies**  
   - Pre-defined dependency sets for common use cases.  
   - Example:  
     - `spring-boot-starter-web` → for REST APIs and web apps  
     - `spring-boot-starter-data-jpa` → for database and JPA  
     - `spring-boot-starter-security` → for authentication & authorization  

3. **Embedded Servers**  
   - No need to deploy WAR files on external servers like Tomcat/Jetty.  
   - Spring Boot ships with **embedded servers** (Tomcat, Jetty, Undertow).  

4. **Production-Ready Features**  
   - Built-in **metrics, health checks, logging, and monitoring** via Spring Boot Actuator.  

5. **Spring Initializr**  
   - A web tool to quickly generate Spring Boot projects with dependencies.  

---

## 3. Difference Between Spring and Spring Boot

| Feature                  | Spring Framework | Spring Boot |
|---------------------------|-----------------|-------------|
| Configuration             | Manual XML/Java config | Auto-configuration |
| Dependency Management     | Manual (add libraries individually) | Starter dependencies |
| Server Setup              | External server (Tomcat, etc.) | Embedded server included |
| Deployment                | WAR file deployment | Executable JAR |
| Learning Curve             | Steeper (more setup needed) | Easier (convention over config) |

---

## 4. Why Use Spring Boot?
- Faster development and setup.  
- Reduced boilerplate code.  
- Production-ready (Actuator, monitoring).  
- Easy integration with databases, security, cloud, and microservices.  
- Ideal for building **REST APIs, Microservices, Cloud Apps, and Enterprise Applications**.  

---
