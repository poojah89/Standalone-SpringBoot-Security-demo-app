# Spring Boot JWT Security Demo

This project demonstrates how to secure a Spring Boot REST API using Spring Security and JWT (JSON Web Token).

The application was built step-by-step to understand the evolution from Basic Authentication to stateless JWT authentication.

---

# Project Overview

This application exposes three endpoints:

| Endpoint | Description | Access |
|--------|-------------|--------|
| `/public/ping` | Public endpoint for testing | No authentication |
| `/api/me` | Endpoint accessible by authenticated users | USER or ADMIN |
| `/api/admin` | Endpoint restricted to administrators | ADMIN only |

---

# Technologies Used

- Java 21
- Spring Boot
- Spring Security
- JWT (JSON Web Tokens)
- Maven

---

# Authentication Approaches Implemented

## 1. Basic Authentication (Initial Implementation)

The project initially used **HTTP Basic Authentication** to understand the fundamentals of Spring Security.

Key components:

- `SecurityFilterChain`
- `UserDetailsService`
- `AuthenticationManager`
- `@PreAuthorize` for role-based access

Basic authentication flow:

1. Client sends request with credentials
2. Spring Security intercepts request
3. `AuthenticationManager` validates credentials
4. `UserDetailsService` loads user
5. `SecurityContext` is populated
6. Authorization rules are applied

Limitations of Basic Auth:

- Credentials sent on every request
- Session-based authentication
- Not ideal for REST APIs
- Harder to scale in distributed systems

---

## 2. JWT Authentication (Current Implementation)

The application was upgraded to **JWT-based authentication**, which is stateless and more suitable for REST APIs.

JWT authentication flow:

1. Client sends login request
2. Server authenticates credentials
3. Server generates a JWT token
4. Client stores token
5. Client calls protected APIs with token
6. JwtAuthFilter validates the token
7. SecurityContext is populated
8. Controller executes if authorization rules pass

## Project Architecture
Request
↓
Tomcat
↓
SecurityFilterChain
↓
JwtAuthFilter
↓
JwtService (token validation)
↓
UserDetailsService
↓
SecurityContextHolder
↓
@PreAuthorize (role check)
↓
Controller
↓
Response
