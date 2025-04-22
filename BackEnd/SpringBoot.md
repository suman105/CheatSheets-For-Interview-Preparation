# Spring Boot Cheatsheet

## Spring Boot Basics

### Basic Spring Boot Application (Annotation-Based)

```java
// src/main/java/com/example/demo/DemoApplication.java
package com.example.demo;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

// Enables auto-configuration, component scanning, and configuration
@SpringBootApplication
@RestController
public class DemoApplication {

    public static void main(String[] args) {
        // Bootstrap Spring Boot application
        SpringApplication.run(DemoApplication.class, args);
    }

    // Simple REST endpoint
    @GetMapping("/hello")
    public String hello() {
        return "Hello, Spring Boot!";
    }
}

// Run: mvn spring-boot:run or ./gradlew bootRun
```

### Java-Based Configuration (Alternative)

```java
// src/main/java/com/example/demo/config/AppConfig.java
package com.example.demo.config;

import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.web.servlet.config.annotation.EnableWebMvc;
import org.springframework.web.servlet.config.annotation.WebMvcConfigurer;

@Configuration
@EnableWebMvc
public class AppConfig implements WebMvcConfigurer {

    @Bean
    public String welcomeMessage() {
        return "Hello, Spring Boot!";
    }
}
```

- **Spring Boot Overview**: A framework for building production-ready Java applications with minimal configuration, built on Spring Framework.
- **Key Features**:
  - Auto-configuration: Automatically configures beans based on dependencies.
  - Embedded servers: Tomcat, Jetty, or Undertow.
  - Starter dependencies: Pre-configured libraries (e.g., `spring-boot-starter-web`).
- **Approaches**:
  - **Annotation-Based**: Uses `@SpringBootApplication` for simplicity.
  - **Java-Based Config**: Explicit configuration, more control.
- **Setup**:
  - Use Maven or Gradle with `spring-boot-starter-parent`.
  - Initialize via Spring Initializr (https://start.spring.io).
- **Best Practices**:
  - Use `@SpringBootApplication` for most projects.
  - Keep `main` class in root package for component scanning.
  - Avoid excessive custom configuration unless needed.

**Explanation**:
- `@SpringBootApplication` combines `@EnableAutoConfiguration`, `@ComponentScan`, and `@Configuration`.
- Java-based config is verbose but useful for fine-grained control or legacy systems.
- Spring Initializr simplifies dependency setup with pre-configured starters.
- Embedded servers eliminate external server setup, ideal for microservices.

---

## Dependency Injection

### Annotation-Based DI (Primary)

```java
// src/main/java/com/example/demo/service/UserService.java
package com.example.demo.service;

import org.springframework.stereotype.Service;

@Service // Marks as a Spring-managed bean
public class UserService {
    public String getUser() {
        return "User: Suman";
    }
}

// src/main/java/com/example/demo/controller/UserController.java
package com.example.demo.controller;

import com.example.demo.service.UserService;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class UserController {
    private final UserService userService;

    // Constructor injection (preferred)
    @Autowired
    public UserController(UserService userService) {
        this.userService = userService;
    }

    @GetMapping("/user")
    public String getUser() {
        return userService.getUser();
    }
}
```

### XML-Based DI (Legacy Alternative)

```xml
<!-- src/main/resources/applicationContext.xml -->
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
       http://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean id="userService" class="com.example.demo.service.UserService"/>
    <bean id="userController" class="com.example.demo.controller.UserController">
        <constructor-arg ref="userService"/>
    </bean>
</beans>
```

### Java-Based Config (Alternative)

```java
// src/main/java/com/example/demo/config/AppConfig.java
package com.example.demo.config;

import com.example.demo.service.UserService;
import com.example.demo.controller.UserController;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

@Configuration
public class AppConfig {
    @Bean
    public UserService userService() {
        return new UserService();
    }

    @Bean
    public UserController userController(UserService userService) {
        return new UserController(userService);
    }
}
```

- **Dependency Injection (DI)**: Spring’s core feature, manages bean dependencies.
- **Approaches**:
  - **Annotation-Based**: Uses `@Autowired`, `@Service`, `@RestController`, modern standard.
  - **XML-Based**: Legacy, verbose, used in older projects.
  - **Java-Based**: Explicit, avoids XML, more maintainable than XML.
- **Best Practices**:
  - Prefer constructor injection over field injection for testability.
  - Use `@Component`, `@Service`, `@Repository` for semantic clarity.
  - Minimize XML config; use annotations or Java config.

**Explanation**:
- Annotation-based DI is concise, leveraging auto-wiring and component scanning.
- XML config is outdated but found in legacy systems; avoid for new projects.
- Java config balances explicitness and flexibility, suitable for complex setups.
- Constructor injection ensures immutable dependencies and simplifies testing.

---

## REST APIs

### Basic REST Controller

```java
// src/main/java/com/example/demo/controller/UserController.java
package com.example.demo.controller;

import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.*;

import java.util.Arrays;
import java.util.List;

@RestController
@RequestMapping("/api/users")
public class UserController {

    // GET all users
    @GetMapping
    public List<String> getUsers() {
        return Arrays.asList("Suman", "Alice");
    }

    // GET user by ID
    @GetMapping("/{id}")
    public ResponseEntity<String> getUser(@PathVariable Long id) {
        return ResponseEntity.ok("User " + id);
    }

    // POST user
    @PostMapping
    public ResponseEntity<String> createUser(@RequestBody UserDTO user) {
        return ResponseEntity.status(201).body("Created: " + user.getName());
    }
}

// DTO for request body
class UserDTO {
    private String name;
    public String getName() { return name; }
    public void setName(String name) { this.name = name; }
}
```

### OpenAPI/Swagger Documentation

```java
// Add dependency: springdoc-openapi-starter-webmvc-ui
// src/main/java/com/example/demo/config/OpenApiConfig.java
package com.example.demo.config;

import io.swagger.v3.oas.models.OpenAPI;
import io.swagger.v3.oas.models.info.Info;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

@Configuration
public class OpenApiConfig {
    @Bean
    public OpenAPI customOpenAPI() {
        return new OpenAPI()
                .info(new Info()
                        .title("User API")
                        .version("1.0")
                        .description("API for managing users"));
    }
}

// Access: http://localhost:8080/swagger-ui.html
```

### JAX-RS Alternative (Less Common)

```java
// Requires dependency: spring-boot-starter-jersey
// src/main/java/com/example/demo/resource/UserResource.java
package com.example.demo.resource;

import jakarta.ws.rs.GET;
import jakarta.ws.rs.Path;
import jakarta.ws.rs.Produces;
import jakarta.ws.rs.core.MediaType;

import java.util.Arrays;
import java.util.List;

@Path("/api/users")
public class UserResource {
    @GET
    @Produces(MediaType.APPLICATION_JSON)
    public List<String> getUsers() {
        return Arrays.asList("Suman", "Alice");
    }
}
```

- **REST APIs**: Spring Boot’s primary use case, built with `@RestController`.
- **Approaches**:
  - **Spring MVC**: Standard, uses `@RestController`, `@GetMapping`, etc.
  - **OpenAPI**: Auto-generates API docs with `springdoc-openapi`.
  - **JAX-RS (Jersey)**: Alternative, uses Jakarta EE annotations.
- **Best Practices**:
  - Use `@RequestMapping` for consistent base paths.
  - Return `ResponseEntity` for flexible HTTP responses.
  - Document APIs with OpenAPI/Swagger for clarity.

**Explanation**:
- Spring MVC is intuitive, tightly integrated with Spring Boot.
- OpenAPI provides interactive API documentation, enhancing developer experience.
- JAX-RS is less common but aligns with Jakarta EE standards.
- Use DTOs to validate and structure request/response bodies.

---

## Data Access with Spring Data

### JPA with Hibernate (Primary)

```java
// src/main/java/com/example/demo/entity/User.java
package com.example.demo.entity;

import jakarta.persistence.Entity;
import jakarta.persistence.Id;

@Entity
public class User {
    @Id
    private Long id;
    private String name;
    private int age;

    // Getters and setters
    public Long getId() { return id; }
    public void setId(Long id) { this.id = id; }
    public String getName() { return name; }
    public void setName(String name) { this.name = name; }
    public int getAge() { return age; }
    public void setAge(int age) { this.age = age; }
}

// src/main/java/com/example/demo/repository/UserRepository.java
package com.example.demo.repository;

import com.example.demo.entity.User;
import org.springframework.data.jpa.repository.JpaRepository;

public interface UserRepository extends JpaRepository<User, Long> {
    // Custom query method
    User findByName(String name);
}

// src/main/java/com/example/demo/service/UserService.java
package com.example.demo.service;

import com.example.demo.entity.User;
import com.example.demo.repository.UserRepository;
import org.springframework.stereotype.Service;

@Service
public class UserService {
    private final UserRepository userRepository;

    public UserService(UserRepository userRepository) {
        this.userRepository = userRepository;
    }

    public User saveUser(User user) {
        return userRepository.save(user);
    }

    public User findByName(String name) {
        return userRepository.findByName(name);
    }
}

// application.properties
spring.datasource.url=jdbc:h2:mem:testdb
spring.datasource.driverClassName=org.h2.Driver
spring.jpa.hibernate.ddl-auto=update
```

### Spring Data MongoDB (NoSQL Alternative)

```java
// src/main/java/com/example/demo/document/User.java
package com.example.demo.document;

import org.springframework.data.annotation.Id;
import org.springframework.data.mongodb.core.mapping.Document;

@Document(collection = "users")
public class User {
    @Id
    private String id;
    private String name;
    private int age;

    // Getters and setters
}

// src/main/java/com/example/demo/repository/UserMongoRepository.java
package com.example.demo.repository;

import com.example.demo.document.User;
import org.springframework.data.mongodb.repository.MongoRepository;

public interface UserMongoRepository extends MongoRepository<User, String> {
    User findByName(String name);
}

// application.properties
spring.data.mongodb.uri=mongodb://localhost:27017/mydb
```

### JDBC Template (Raw SQL Alternative)

```java
// src/main/java/com/example/demo/service/UserJdbcService.java
package com.example.demo.service;

import org.springframework.jdbc.core.JdbcTemplate;
import org.springframework.stereotype.Service;

@Service
public class UserJdbcService {
    private final JdbcTemplate jdbcTemplate;

    public UserJdbcService(JdbcTemplate jdbcTemplate) {
        this.jdbcTemplate = jdbcTemplate;
    }

    public void saveUser(String name, int age) {
        jdbcTemplate.update("INSERT INTO users (name, age) VALUES (?, ?)", name, age);
    }

    public String findUserByName(String name) {
        return jdbcTemplate.queryForObject(
                "SELECT name FROM users WHERE name = ?", String.class, name);
    }
}
```

- **Data Access**:
  - **Spring Data JPA**: ORM with Hibernate, relational databases.
  - **Spring Data MongoDB**: NoSQL, document-based storage.
  - **JDBC Template**: Raw SQL, lightweight, high control.
- **Best Practices**:
  - Use JPA for complex relationships; MongoDB for flexible schemas.
  - Define repositories with clear interfaces.
  - Use `@Transactional` for database operations requiring atomicity.

**Explanation**:
- JPA simplifies CRUD with repositories, ideal for SQL databases.
- MongoDB suits unstructured data, leveraging Spring Data’s repository pattern.
- JDBC Template offers performance but requires manual query management.
- Configure datasources in `application.properties` for flexibility.

---

## Spring Security

### Basic Authentication

```java
// src/main/java/com/example/demo/config/SecurityConfig.java
package com.example.demo.config;

import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.security.config.annotation.web.builders.HttpSecurity;
import org.springframework.security.config.annotation.web.configuration.EnableWebSecurity;
import org.springframework.security.core.userdetails.User;
import org.springframework.security.core.userdetails.UserDetailsService;
import org.springframework.security.provisioning.InMemoryUserDetailsManager;
import org.springframework.security.web.SecurityFilterChain;

@Configuration
@EnableWebSecurity
public class SecurityConfig {

    @Bean
    public SecurityFilterChain securityFilterChain(HttpSecurity http) throws Exception {
        http
                .authorizeHttpRequests(auth -> auth
                        .requestMatchers("/public").permitAll()
                        .anyRequest().authenticated()
                )
                .formLogin(form -> form.permitAll())
                .logout(logout -> logout.permitAll());
        return http.build();
    }

    @Bean
    public UserDetailsService userDetailsService() {
        var user = User.withDefaultPasswordEncoder()
                .username("user")
                .password("password")
                .roles("USER")
                .build();
        return new InMemoryUserDetailsManager(user);
    }
}
```

### JWT-Based Authentication

```java
// src/main/java/com/example/demo/config/JwtSecurityConfig.java
package com.example.demo.config;

import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.security.config.annotation.web.builders.HttpSecurity;
import org.springframework.security.web.SecurityFilterChain;
import org.springframework.security.web.authentication.UsernamePasswordAuthenticationFilter;

@Configuration
public class JwtSecurityConfig {

    @Bean
    public SecurityFilterChain securityFilterChain(HttpSecurity http) throws Exception {
        http
                .csrf(csrf -> csrf.disable())
                .authorizeHttpRequests(auth -> auth
                        .requestMatchers("/api/login").permitAll()
                        .anyRequest().authenticated()
                )
                .addFilterBefore(jwtAuthenticationFilter(), UsernamePasswordAuthenticationFilter.class);
        return http.build();
    }

    @Bean
    public JwtAuthenticationFilter jwtAuthenticationFilter() {
        return new JwtAuthenticationFilter();
    }
}

// src/main/java/com/example/demo/security/JwtAuthenticationFilter.java
package com.example.demo.security;

import jakarta.servlet.FilterChain;
import jakarta.servlet.http.HttpServletRequest;
import jakarta.servlet.http.HttpServletResponse;
import org.springframework.security.core.context.SecurityContextHolder;
import org.springframework.web.filter.OncePerRequestFilter;

public class JwtAuthenticationFilter extends OncePerRequestFilter {
    @Override
    protected void doFilterInternal(HttpServletRequest request, HttpServletResponse response, FilterChain chain) {
        // Implement JWT validation logic
        chain.doFilter(request, response);
    }
}
```

- **Spring Security**: Secures applications with authentication and authorization.
- **Approaches**:
  - **Basic Auth**: Form-based, session-based, simple.
  - **JWT**: Stateless, token-based, ideal for APIs.
- **Best Practices**:
  - Use HTTPS to protect credentials.
  - Implement role-based access control (RBAC).
  - Store passwords with `BCryptPasswordEncoder`.

**Explanation**:
- Basic auth is quick for prototyping but stateful, less scalable.
- JWT is stateless, suitable for microservices and SPAs.
- Custom filters enable flexible authentication mechanisms.
- Secure APIs with CSRF disabled for stateless setups.

---

## Testing

### Unit Testing with JUnit and Mockito

```java
// src/test/java/com/example/demo/service/UserServiceTest.java
package com.example.demo.service;

import com.example.demo.repository.UserRepository;
import org.junit.jupiter.api.Test;
import org.mockito.InjectMocks;
import org.mockito.Mock;
import org.springframework.boot.test.context.SpringBootTest;

import static org.mockito.Mockito.when;
import static org.junit.jupiter.api.Assertions.assertEquals;

@SpringBootTest
public class UserServiceTest {

    @Mock
    private UserRepository userRepository;

    @InjectMocks
    private UserService userService;

    @Test
    public void testFindByName() {
        when(userRepository.findByName("Suman")).thenReturn(new User(1L, "Suman", 25));
        User user = userService.findByName("Suman");
        assertEquals("Suman", user.getName());
    }
}
```

### Integration Testing with TestRestTemplate

```java
// src/test/java/com/example/demo/controller/UserControllerTest.java
package com.example.demo.controller;

import org.junit.jupiter.api.Test;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.boot.test.web.client.TestRestTemplate;

import static org.junit.jupiter.api.Assertions.assertEquals;

@SpringBootTest(webEnvironment = SpringBootTest.WebEnvironment.RANDOM_PORT)
public class UserControllerTest {

    @Autowired
    private TestRestTemplate restTemplate;

    @Test
    public void testGetUsers() {
        String response = restTemplate.getForObject("/api/users", String.class);
        assertEquals("[\"Suman\",\"Alice\"]", response);
    }
}
```

- **Testing**:
  - **Unit**: Tests services with mocks (JUnit, Mockito).
  - **Integration**: Tests controllers with real server (TestRestTemplate).
- **Best Practices**:
  - Mock dependencies for unit tests to isolate logic.
  - Use `@SpringBootTest` for integration tests with real beans.
  - Test error cases and edge conditions.

**Explanation**:
- Unit tests focus on business logic, using mocks to avoid database calls.
- Integration tests verify API behavior, including HTTP responses.
- Spring Boot’s test annotations simplify setup.
- Use tools like AssertJ for fluent assertions.

---

## Microservices with Spring Cloud

### Service Registry with Eureka

```java
// src/main/java/com/example/demo/EurekaServerApplication.java
package com.example.demo;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.cloud.netflix.eureka.server.EnableEurekaServer;

@SpringBootApplication
@EnableEurekaServer
public class EurekaServerApplication {
    public static void main(String[] args) {
        SpringApplication.run(EurekaServerApplication.class, args);
    }
}

// application.yml
server:
  port: 8761
eureka:
  client:
    register-with-eureka: false
    fetch-registry: false
```

### Client Service

```java
// src/main/java/com/example/demo/UserServiceApplication.java
package com.example.demo;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.cloud.client.discovery.EnableDiscoveryClient;

@SpringBootApplication
@EnableDiscoveryClient
public class UserServiceApplication {
    public static void main(String[] args) {
        SpringApplication.run(UserServiceApplication.class, args);
    }
}

// application.yml
spring:
  application:
    name: user-service
eureka:
  client:
    service-url:
      defaultZone: http://localhost:8761/eureka/
```

- **Microservices**: Spring Cloud enhances Spring Boot for distributed systems.
- **Components**:
  - **Eureka**: Service discovery.
  - **Spring Cloud Config**: Centralized configuration.
  - **Spring Cloud Gateway**: API gateway.
- **Best Practices**:
  - Use Eureka for service discovery in dynamic environments.
  - Implement circuit breakers with Resilience4j.
  - Monitor with Actuator and Prometheus.

**Explanation**:
- Eureka enables services to find each other without hardcoding URLs.
- Spring Cloud Config centralizes configuration for scalability.
- Microservices increase complexity; ensure clear boundaries.
- Use Kubernetes for orchestration in production.

---

## Reactive Programming with WebFlux

### Reactive REST Controller

```java
// src/main/java/com/example/demo/controller/ReactiveUserController.java
package com.example.demo.controller;

import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;
import reactor.core.publisher.Flux;

@RestController
public class ReactiveUserController {
    @GetMapping("/reactive/users")
    public Flux<String> getUsers() {
        return Flux.just("Suman", "Alice");
    }
}
```

- **WebFlux**: Reactive, non-blocking alternative to Spring MVC.
- **Key Features**:
  - Uses Project Reactor (`Mono`, `Flux`).
  - Ideal for high-concurrency, low-latency apps.
- **Best Practices**:
  - Use WebFlux for I/O-heavy apps (e.g., streaming).
  - Avoid blocking calls in reactive pipelines.
  - Test with `WebTestClient`.

**Explanation**:
- WebFlux leverages reactive streams, improving resource efficiency.
- `Flux` handles multiple items, `Mono` for single items.
- Requires reactive repositories (e.g., Spring Data R2DBC).
- Use for specific use cases; Spring MVC suffices for most apps.

---

## Docker Integration

### Dockerfile

```dockerfile
FROM openjdk:17-jdk-slim
WORKDIR /app
COPY target/demo-0.0.1-SNAPSHOT.jar app.jar
EXPOSE 8080
ENTRYPOINT ["java", "-jar", "app.jar"]
```

### Docker Compose

```yaml
version: '3.8'
services:
  app:
    build: .
    ports:
      - "8080:8080"
    environment:
      - SPRING_DATASOURCE_URL=jdbc:postgresql://db:5432/mydb
  db:
    image: postgres:13
    environment:
      - POSTGRES_DB=mydb
      - POSTGRES_USER=user
      - POSTGRES_PASSWORD=pass
    ports:
      - "5432:5432"
```

- **Docker**: Containerizes Spring Boot apps for consistent deployment.
- **Best Practices**:
  - Use slim base images (e.g., `openjdk:17-jdk-slim`).
  - Externalize configuration with environment variables.
  - Use multi-stage builds for smaller images.

**Explanation**:
- Docker ensures portability across environments.
- Docker Compose simplifies multi-container setups (app + database).
- Optimize images with `.dockerignore` and slim JREs.
- Deploy with Kubernetes for scaling.

---

## Best Practices

- **Code**: Use package-by-feature (e.g., `com.example.user`), follow REST conventions.
- **Performance**: Cache with `@Cacheable`, use connection pooling.
- **Security**: Enable HTTPS, use Spring Security, validate inputs.
- **Testing**: Write unit and integration tests, mock dependencies.
- **Deployment**: Use Docker, CI/CD pipelines, monitor with Actuator.
- **Logging**: Use SLF4J with Logback, configure levels.

**Explanation**:
- Structured practices ensure maintainability and scalability.
- Security and testing prevent vulnerabilities and bugs.
- Monitoring and CI/CD improve production reliability.

---

## Common Spring Boot Annotations & Features

- **Annotations**:
  - `@SpringBootApplication`, `@RestController`, `@Service`, `@Repository`.
  - `@Autowired`, `@GetMapping`, `@PostMapping`, `@RequestBody`.
  - `@Transactional`, `@Cacheable`, `@EnableWebSecurity`.
- **Features**:
  - Actuator: Health checks, metrics (`/actuator/health`).
  - Profiles: Environment-specific configs (`application-dev.yml`).
  - DevTools: Auto-reload for development.

**Explanation**:
- Annotations simplify configuration and wiring.
- Actuator aids monitoring in production.
- Profiles enable flexible configuration management.

---

## Cheat Codes

```java
// Custom Actuator endpoint
@Endpoint(id = "custom")
public class CustomEndpoint {
    @ReadOperation
    public String custom() {
        return "Custom endpoint";
    }
}

// Log with SLF4J
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
Logger logger = LoggerFactory.getLogger(MyClass.class);
logger.info("Message");

// Profile-specific property
// application-dev.properties
spring.datasource.url=jdbc:h2:mem:devdb
```

**Explanation**:
- Custom endpoints extend Actuator for specific needs.
- SLF4J provides flexible logging with minimal overhead.
- Profiles streamline environment-specific configs.