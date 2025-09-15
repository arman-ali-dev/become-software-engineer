# REST API Development in Spring Boot

REST (Representational State Transfer) APIs allow applications to communicate over HTTP using JSON/XML.  
Spring Boot makes it easy to build RESTful services.

---

## 1. Building REST APIs with Spring Boot

- Use `@RestController` and mapping annotations (`@GetMapping`, `@PostMapping`, etc.).
- Data is usually exchanged in **JSON format**.
- Service layer (`@Service`) handles business logic.
- Repository layer (`@Repository`) interacts with database.

### Example
```java
@RestController
@RequestMapping("/api/users")
public class UserController {

    @GetMapping
    public List<User> getAllUsers() {
        // fetch users from DB
        return List.of(new User(1, "John"), new User(2, "Alice"));
    }

    @PostMapping
    public User createUser(@RequestBody User user) {
        // save user to DB
        return user;
    }
}
```

## 2. Returning JSON Response (Jackson)
- Spring Boot uses Jackson library internally to convert Java objects → JSON.
- No need for manual conversion.

```java
@RestController
public class ProductController {
    @GetMapping("/product")
    public Product getProduct() {
        return new Product(1, "Laptop", 50000);
    }
}
```


```output
{
  "id": 1,
  "name": "Laptop",
  "price": 50000
}
```

## 3. Handling Exceptions
- Local Exception Handling (inside method)

```java
@GetMapping("/user/{id}")
public User getUser(@PathVariable int id) {
    if (id <= 0) {
        throw new IllegalArgumentException("Invalid user ID");
    }
    return new User(id, "Demo");
}
```

- Global Exception Handling (@ControllerAdvice)
- Centralized place to handle exceptions for all controllers.
```java
@ControllerAdvice
public class GlobalExceptionHandler {

    @ExceptionHandler(IllegalArgumentException.class)
    public ResponseEntity<String> handleInvalidArgument(IllegalArgumentException ex) {
        return ResponseEntity.badRequest().body(ex.getMessage());
    }

    @ExceptionHandler(Exception.class)
    public ResponseEntity<String> handleGeneral(Exception ex) {
        return ResponseEntity.status(HttpStatus.INTERNAL_SERVER_ERROR)
                             .body("Something went wrong!");
    }
}
```

## 4. Versioning APIs
- APIs evolve over time. To avoid breaking old clients, we use API Versioning.

### Approaches
1. URI Versioning
- /api/v1/users, /api/v2/users

```java
@RestController
@RequestMapping("/api/v1/users")
public class UserV1Controller { ... }

@RestController
@RequestMapping("/api/v2/users")
public class UserV2Controller { ... }
```
2. Request Parameter Versioning
- /api/users?version=1

```java
@GetMapping(value = "/users", params = "version=1")
public String getUsersV1() { return "Users V1"; }

@GetMapping(value = "/users", params = "version=2")
public String getUsersV2() { return "Users V2"; }
```

3. Header-based Versioning
- Clients send custom header: X-API-VERSION: 1.

```java
@GetMapping(value = "/users", headers = "X-API-VERSION=1")
public String getUsersHeaderV1() { return "Users V1"; }
```

## 5. Pagination & Sorting with Spring Data
When dealing with large datasets, use pagination and sorting.

### Spring Data JPA provides:
- Pageable → handles page number & size.
- Page<T> → wrapper with total pages, size, etc.
- Sort → handles sorting by fields.
- Example
```java
public interface UserRepository extends JpaRepository<User, Integer> {
}
```

```java
@RestController
@RequestMapping("/api/users")
public class UserController {

    @Autowired
    private UserRepository userRepository;

    // Pagination + Sorting
    @GetMapping
    public Page<User> getUsers(
            @RequestParam int page,
            @RequestParam int size,
            @RequestParam String sortBy) {

        Pageable pageable = PageRequest.of(page, size, Sort.by(sortBy));
        return userRepository.findAll(pageable);
    }
}
```
```pgsql
GET /api/users?page=0&size=5&sortBy=name
```

- Response (sample JSON)
```java
{
  "content": [
    {"id": 1, "name": "Alice"},
    {"id": 2, "name": "Bob"}
  ],
  "totalPages": 10,
  "totalElements": 50,
  "size": 5,
  "number": 0
}
```

## Summary (Quick Look)
- Build REST APIs → @RestController, @GetMapping, @PostMapping, etc.
- JSON Response → handled automatically by Jackson.
- Exception Handling → local with try-catch, global with @ControllerAdvice.
- Versioning APIs → URI, Request Param, or Header-based.
- Pagination & Sorting → Spring Data JPA provides Pageable, Page, and Sort.
