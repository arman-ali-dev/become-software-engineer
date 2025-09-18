# Data & Persistence Layer in Spring Boot

## 1. Spring Data JPA Basics
- **JPA (Java Persistence API)** → Standard for ORM (Object Relational Mapping).
- **Spring Data JPA** makes working with databases easier (no need to write long JDBC code).
- Provides ready-made repository interfaces to perform CRUD operations.


## 2. Entities and @Entity Annotation
- **Entity** → A Java class mapped to a database table.
- Mark class with `@Entity`.
- Use `@Id` for primary key.
- `@GeneratedValue` for auto-increment ID.


```java
import jakarta.persistence.*;

@Entity
public class User {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String name;
    private String email;
}
```

## 3. Repositories: CrudRepository, JpaRepository
- CrudRepository → Basic CRUD operations (save, findById, delete, etc.)
- JpaRepository → Extends CrudRepository + pagination + sorting features.

```java
import org.springframework.data.jpa.repository.JpaRepository;

public interface UserRepository extends JpaRepository<User, Long> {
}
```

## 4. Derived Query Methods
- Spring generates queries automatically by method names.
- Examples:
- findByName(String name)
- countByEmail(String email)
- deleteByName(String name)

```java
List<User> findByName(String name);
long countByEmail(String email);
void deleteByName(String name);
```

## 5. JPQL & Native Queries
- JPQL (Java Persistence Query Language) → Works with entity objects.
- Native Query → Direct SQL query.

```java
@Query("SELECT u FROM User u WHERE u.name = :name")   // JPQL
List<User> findUserByName(@Param("name") String name);

@Query(value = "SELECT * FROM user WHERE email=?1", nativeQuery = true)  // Native SQL
User findByEmail(String email);
```

## 6. Relationships (Entity Mapping)
- OneToOne → One entity related to exactly one other.
- OneToMany → One entity has a list of others.
- ManyToMany → Many entities connected to many.

```java
@Entity
public class Student {
    @Id
    @GeneratedValue
    private Long id;
    private String name;

    @OneToMany(mappedBy = "student")
    private List<Course> courses;
}
```

## 7. Hibernate with MySQL / PostgreSQL
- Hibernate is the ORM framework behind JPA.
- Configure database in application.properties:

```properties
spring.datasource.url=jdbc:mysql://localhost:3306/mydb
spring.datasource.username=root
spring.datasource.password=1234
spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
```

## 8. MongoDB with Spring Data Mongo
- Works with NoSQL databases.
- Use @Document instead of @Entity.
- Repository extends MongoRepository.

```java
import org.springframework.data.mongodb.core.mapping.Document;

@Document(collection = "users")
public class User {
    private String id;
    private String name;
    private String email;
}


public interface UserRepository extends MongoRepository<User, String> {
}
```

## Summary
- Spring Data JPA → Simplifies database interaction.
- Entities map Java objects to database tables.
- Repositories provide CRUD + custom queries.
- Relationships manage entity connections.
- Works with both SQL (MySQL/Postgres) and NoSQL (MongoDB) databases.
