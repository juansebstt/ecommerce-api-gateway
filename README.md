# E-commerce API Gateway

## Overview

The **E-commerce API Gateway** is a microservice built using Spring Boot that acts as a single entry point for client requests to multiple backend services, such as the authentication service and the payment service. It improves the architecture by managing routing, JWT-based authentication, request forwarding, and load balancing, ensuring a seamless interaction between the client and internal services.

## Features

- **Centralized Routing**: Handles client requests and forwards them to the appropriate microservices (Auth-Service, Payment-Service, etc.).
- **JWT Authentication**: Verifies JSON Web Tokens (JWT) for secure communication.
- **Load Balancing**: Distributes incoming traffic to improve scalability and performance.
- **Fault Tolerance**: Implements resilience patterns to ensure reliability.
- **Monitoring and Logging**: Centralized logging and monitoring for requests, errors, and system health.

## Technologies Used

- **Java 17**
- **Spring Boot**
- **Spring Cloud Gateway** - For routing and load balancing.
- **Spring Security** - For authentication and authorization.
- **JWT** - For secure user authentication.
- **Maven** - Dependency management and build tool.
- **Docker** - Containerization for easy deployment.
- **PostgreSQL** - Used for backend services (though not directly connected to the gateway).

## Prerequisites

Before running this service, ensure you have the following installed:

- **Java 17**
- **Maven** (for building the project)
- **Docker**
- Microservices:
   - [Auth Service](https://github.com/juansebstt/ecommerce-auth-service) - Manages user registration, login, and JWT authentication. 
  - [Payment Service](https://github.com/juansebstt/ecommerce-payment-service) - Handles Stripe payments and transaction processing.

## Installation

1. Clone the repository:

    ```bash
    git clone https://github.com/juansebstt/ecommerce-api-gateway
    ```

2. Navigate to the project directory:

    ```bash
    cd ecommerce-api-gateway
    ```

3. Build the project using Maven:

    ```bash
    mvn clean install
    ```

4. Run the project:

    ```bash
    mvn spring-boot:run
    ```


## Configuration

The API Gateway uses a configuration file to manage routing, security, and other properties. Here are the key configuration options from `application.yaml`:

```yaml
yaml
server:
  port: 8080

spring:
  cloud:
    gateway:
      routes:
        - id: auth-service
          uri: http://localhost:8081
          predicates:
            - Path=/auth/**
        - id: payment-service
          uri: http://localhost:8082
          predicates:
            - Path=/payment/**
  security:
    oauth2:
      resourceserver:
        jwt:
          issuer-uri: https://issuer-url.com/

```

- Replace the `uri` values with the actual URLs where your services are hosted.
- Configure JWT issuer URI for security.

## Usage

Once the gateway is running, you can access the backend services through the following routes:

- `http://localhost:8080/auth/**` - For authentication-related requests (handled by Auth Service).
- `http://localhost:8080/payment/**` - For payment-related requests (handled by Payment Service).

## Contributing

Feel free to submit pull requests or open issues if you find bugs or want to contribute to the project.