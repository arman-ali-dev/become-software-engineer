# Dependency Injection & Bean Management

## 1. What is a Bean?
- A **bean** is just a Java object that is created, managed, and destroyed by the **Spring container**.
- Instead of creating objects manually using `new`, Spring creates and gives them to us when needed.

---

## 2. What is Dependency Injection (DI)?
- **Dependency**: If class A needs object of class B, then B is a dependency of A.
- **Dependency Injection**: Spring automatically provides (injects) required objects to a class instead of us creating them.
- Benefits:
  - Loose coupling (classes don’t depend tightly on each other).
  - Easier testing (we can replace real objects with mock objects).
  - Cleaner and more organized code.

Example:
```java
@Component
class Engine { }

@Component
class Car {
    private final Engine engine;

    @Autowired
    public Car(Engine engine) {
        this.engine = engine;
    }
}
```
Here, Spring injects Engine object into Car.

## 3. @Component, @Service, @Repository

These are stereotype ( Role, Purpose ) annotations used to tell Spring to create beans automatically.

- @Component: Generic annotation for any bean.
- @Service: Special type of component used for business logic classes.
- @Repository: Special type of component used for database/persistence classes.
    - Extra feature: it automatically converts database exceptions into Spring exceptions.
- Example:
```java
@Component
class Engine { }

@Service
class PaymentService { }

@Repository
class UserRepository { }
```

## 4. @Autowired and @Qualifier

- @Autowired: Tells Spring to inject dependency automatically.
    - Works with constructor, setter, or field.
    - Constructor injection is recommended (clean and testable).
- @Qualifier: Used when multiple beans of the same type exist and we need to specify which one to inject.
- Example:
```java
@Component("dieselEngine")
class DieselEngine { }

@Component("petrolEngine")
class PetrolEngine { }

@Component
class Car {
    private final Engine engine;

    @Autowired
    public Car(@Qualifier("dieselEngine") Engine engine) {
        this.engine = engine;
    }
}
```

## 5. @Configuration and @Bean
- @Configuration: Marks a class as a configuration class (like a replacement for XML config).
- @Bean: Used inside @Configuration to define beans manually.
- Example:
```java
@Configuration
class AppConfig {
    @Bean
    public Engine engine() {
        return new Engine();
    }

    @Bean
    public Car car(Engine engine) {
        return new Car(engine);
    }
}
```

## 6. Bean Scopes
Scope = lifetime of a bean (how many objects are created).

1. singleton (default) → Only one bean instance per Spring container.
2. prototype → New bean instance every time it is requested.
3. request (web apps) → One bean per HTTP request.
4. session (web apps) → One bean per HTTP session.

```java
@Component
@Scope("prototype")
class PrototypeBean { }
```

## 7. Bean Lifecycle
Steps from bean creation to destruction:

1. Spring creates the bean object.
2. Dependencies are injected.
3. If the bean implements Aware interfaces, Spring gives container info.
4. @PostConstruct method (if present) is called.
5. Bean is ready for use.
6. When container shuts down:
   - @PreDestroy method (if present) is called.
   - Bean is destroyed.
  
```java
@Component
class MyBean {
    @PostConstruct
    public void init() {
        System.out.println("Bean initialized");
    }

    @PreDestroy
    public void destroy() {
        System.out.println("Bean destroyed");
    }
}
```
