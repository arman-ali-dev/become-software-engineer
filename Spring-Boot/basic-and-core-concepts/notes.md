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


# Advantages of Spring Boot

Spring Boot simplifies Java application development by providing fast setup, less configuration, and production-ready features. The key advantages are:

---

## 1. Auto-Configuration
Spring Boot automatically configures your application based on the dependencies added to the project.

- If you add `spring-boot-starter-web` → it configures Tomcat, Spring MVC, and JSON support automatically.  
- If MySQL driver is present → it auto-configures a DataSource.  
- No need to write lengthy XML configuration.

Focus on **business logic**, not boilerplate setup.

---

## 2. Starter Dependencies
Spring Boot provides **starter packs** (predefined dependency sets) to reduce dependency management issues.

- `spring-boot-starter-web` → Web + Spring MVC + JSON + Tomcat  
- `spring-boot-starter-data-jpa` → Hibernate + JPA + Database Drivers  
- `spring-boot-starter-security` → Spring Security  

Add one dependency, and you get everything required for that feature.

---

## 3. Embedded Server
Spring Boot applications come with an **embedded server** (Tomcat/Jetty/Undertow).  

- No need to install and configure an external server.  
- Run apps directly using:  
  ```bash
  mvn spring-boot:run
  java -jar app.jar
  ```
- Easy deployment with Docker & Cloud.
- Deploy as a standalone application without WAR files.

### 4. Production-Ready Features
Spring Boot comes with features that make applications ready for production use:
- Spring Boot Actuator for health checks, metrics, and monitoring
- Built-in logging (SLF4J, Logback)
- Easy integration with cloud platforms (AWS, GCP, Azure)
- Profiles and environment-specific configurations

### Summary:

- Auto-Configuration → Reduces boilerplate code
- Starter Dependencies → Hassle-free dependency management
- Embedded Server → Run standalone apps easily
- Production-Ready Features → Monitoring, logging, deployment support

# Project Setup in Spring Boot
Spring Boot project setup can be done in multiple ways. The most common methods are:

## 1. Spring Initializr

- Spring Initializr is an online tool to quickly generate a Spring Boot project.
- Website: https://start.spring.io
- You can choose:
  - Project type → Maven or Gradle
  - Spring Boot version → Stable version (e.g., 3.x)
  - Project metadata → Group, Artifact, Name, Package, Java version
  - Dependencies → Like Spring Web, Spring Data JPA, Security, Lombok, etc.
- It generates a ready-to-run project (zip file). Just unzip, open in IDE (IntelliJ, Eclipse, VS Code), and start coding.
- Best way for beginners and professionals to quickly bootstrap a project.

## 2. Maven-based Setup
Maven is a build automation and dependency management tool.
- Project is defined using a pom.xml file.
- In pom.xml, you declare dependencies, plugins, and project information.
- Example pom.xml snippet for Spring Boot:
```xml
<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-data-jpa</artifactId>
    </dependency>
</dependencies>
```
- Maven downloads all required JARs automatically.
- mvn spring-boot:run → run project
- mvn clean install → build project

## 3. Gradle-based Setup
Gradle is another modern build tool (faster and more flexible than Maven).
- Project is defined using build.gradle file.
- Example build.gradle snippet:
```java
dependencies {
    implementation 'org.springframework.boot:spring-boot-starter-web'
    implementation 'org.springframework.boot:spring-boot-starter-data-jpa'
}
```
- Supports both Groovy and Kotlin DSL.
- Gradle builds are generally faster than Maven (uses incremental build + caching).
- ./gradlew bootRun → run project
- ./gradlew build → build project

## 4. Choosing Between Maven & Gradle
- Maven → Easier to learn, more widely used, strong convention, huge community support.
- Gradle → Faster, flexible, modern, preferred in large-scale projects.

### Summary:

- Spring Initializr → Quickest way to generate a Spring Boot project
- Maven → XML-based, widely used build tool
- Gradle → Modern, faster alternative to Maven

# application.properties vs application.yml
Spring Boot applications need a configuration file to define settings (like database URL, server port, logging level, etc.).
<br/>
<br/>
We can use either application.properties or application.yml. Both serve the same purpose, but their syntax and readability are different.

## 1. application.properties
- Key-Value format (simple, one line per property).
- Example:
```properties
server.port=8081
spring.datasource.url=jdbc:mysql://localhost:3306/mydb
spring.datasource.username=root
spring.datasource.password=1234
logging.level.org.springframework=DEBUG
```
- Easy for small projects.
- Gets messy when configuration grows large (repetition of keys).

## 2. application.yml
- Uses YAML (YAML Ain’t Markup Language) format → hierarchical and cleaner.
- Example:
```yaml
server:
  port: 8081

spring:
  datasource:
    url: jdbc:mysql://localhost:3306/mydb
    username: root
    password: 1234

logging:
  level:
    org.springframework: DEBUG
```
- More readable for nested configurations.
- Better for profiles (dev, test, prod).
- Indentation errors can cause issues.

## 3. When to Use What?
- Use application.properties if → project is small/simple.
- Use application.yml if → project is large, has multiple nested configs or environments.

### Summary:
- application.properties → Simple key-value, easy for small apps.
- application.yml → Hierarchical, clean, better for complex configs.
- Both supported by Spring Boot, but .properties wins if conflict occurs.

