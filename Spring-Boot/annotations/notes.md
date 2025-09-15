# Spring Boot Annotations (Must Know)

These annotations are the backbone of Spring Boot development.  
They make application configuration, API building, and property management easier.

## 1. `@SpringBootApplication`

### What it is
- Main entry-point annotation for a Spring Boot application.
- Combines three annotations:
  - `@Configuration` → allows bean definitions using `@Bean`.
  - `@EnableAutoConfiguration` → enables auto configuration based on classpath dependencies.
  - `@ComponentScan` → automatically scans for beans in the package and subpackages.
 
### Example
```java
@SpringBootApplication
public class MyApp {
    public static void main(String[] args) {
        SpringApplication.run(MyApp.class, args);
    }
}
```

### Notes

- Always placed on the main application class.
- You can limit scanning:

```java
@SpringBootApplication(scanBasePackages = {"com.example.service", "com.example.controller"})
```

## 2. @RestController vs @Controller
### @Controller

- Used in traditional MVC applications.
- Returns views (HTML/JSP/Thymeleaf).
- If you want to return JSON, you must also use @ResponseBody.

### @RestController

- Shortcut for @Controller + @ResponseBody.
- Used for REST APIs.
- Returns data (JSON/XML) directly in the response body.

```java
@Controller
public class HomeController {
    @GetMapping("/home")
    public String home() {
        return "home"; // returns view name (home.html)
    }
}

@RestController
public class ApiController {
    @GetMapping("/hello")
    public String hello() {
        return "Hello World"; // returns JSON/text directly
    }
}
```

## 3. @RequestMapping, @GetMapping, @PostMapping, etc.

### Purpose
- Maps HTTP requests to Java methods.

### Types

- @RequestMapping → general mapping (can define GET, POST, etc.).
- @GetMapping → handles HTTP GET requests.
- @PostMapping → handles HTTP POST requests.
- @PutMapping → handles HTTP PUT requests.
- @DeleteMapping → handles HTTP DELETE requests.
- @PatchMapping → handles HTTP PATCH requests.

```java
@RestController
@RequestMapping("/api")
public class UserController {

    @GetMapping("/users")
    public List<User> getAllUsers() { ... }

    @PostMapping("/users")
    public User createUser(@RequestBody User user) { ... }

    @PutMapping("/users/{id}")
    public User updateUser(@PathVariable Long id, @RequestBody User user) { ... }

    @DeleteMapping("/users/{id}")
    public void deleteUser(@PathVariable Long id) { ... }
}
```

### Extra Note
- You can also add produces and consumes for controlling request/response type.

## 4. @PathVariable and @RequestParam

### @PathVariable

- Extracts value from URI path.
- Used when the value is part of the URL.

```java
@GetMapping("/users/{id}")
public String getUser(@PathVariable int id) {
    return "User ID = " + id;
}
```

### @RequestParam

- Extracts value from query parameters.
- Used when values are passed like ?key=value.

```java
@GetMapping("/search")
public String search(@RequestParam String name) {
    return "Searching user with name = " + name;
}
```

### Default values
```java
@GetMapping("/search")
public String search(@RequestParam(defaultValue = "guest") String name) {
    return "Hello " + name;
}
```

## 5. @RequestBody and @ResponseBody

### @RequestBody

- Binds request body (JSON/XML) to a Java object.
- Used in POST/PUT methods.

```java
@PostMapping("/products")
public Product addProduct(@RequestBody Product product) {
    return product;
}
```

### @ResponseBody

- Converts the return value of a method into JSON/XML response.
- Already included in @RestController.

```java
@Controller
public class ProductController {
    @PostMapping("/products")
    @ResponseBody
    public Product addProduct(@RequestBody Product product) {
        return product;
    }
}
```

## 6. @ConfigurationProperties

### Purpose

- Maps values from application.properties or application.yml to a Java class.
- Helps in grouping related configuration.

### Example

#### application.properties

```properties
app.name=MySpringApp
app.version=1.0
```

```java
@Component
@ConfigurationProperties(prefix = "app")
public class AppConfig {
    private String name;
    private String version;

    // getters and setters
}
```

```java
@Autowired
private AppConfig appConfig;

System.out.println(appConfig.getName()); // MySpringApp
```

#### Extra
- Can also work with .yml:

```yaml
app:
  name: MySpringApp
  version: 1.0
```

- You can validate config with JSR-303 annotations:

```java
@Component
@ConfigurationProperties(prefix = "app")
@Validated
public class AppConfig {
    @NotNull
    private String name;
    ...
}
```

## Summary (Quick Look)
- @SpringBootApplication → main entry point (config + auto-config + scanning).
- @Controller → returns views, @RestController → returns JSON/XML.
- @GetMapping, @PostMapping, etc. → map HTTP methods to functions.
- @PathVariable → extract path data, @RequestParam → extract query params.
- @RequestBody → request JSON → Java object, @ResponseBody → Java object → JSON.
- @ConfigurationProperties → bind external config to Java class.
