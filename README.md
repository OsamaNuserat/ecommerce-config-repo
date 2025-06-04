
# ecommerce-config-repo

This repository contains centralized configuration files for all microservices in the **Ecommerce Microservices Architecture** using Spring Cloud Config.

---

## 🎯 Purpose

This repository acts as the **central configuration source** for all microservices in your architecture. The Spring Cloud Config Server will load and serve these configuration files to each microservice during startup.

---

## 📂 Structure

```
ecommerce-config-repo/
├── product-service.yml
├── order-service.yml
├── inventory-service.yml
├── payment-service.yml
├── discovery-server.yml
├── gateway-service.yml
```

Each file holds configuration properties like:

- `server.port`
- `spring.datasource` (DB config)
- `spring.application.name`
- `eureka.client.service-url`
- Any custom per-service properties

---

## 🛠 How to Use

### In Config Server (`application.yml`):
```yaml
spring:
  cloud:
    config:
      server:
        git:
          uri: https://github.com/YOUR_USERNAME/ecommerce-config-repo
```

> Replace `YOUR_USERNAME` with your actual GitHub username.

### In Client Services (`bootstrap.yml` or `application.yml`):
```yaml
spring:
  config:
    import: optional:configserver:http://localhost:8888
  application:
    name: product-service
```

> Make sure `name` matches the correct file name in this repo (e.g., `product-service.yml`).

---

## 🧾 Example: product-service.yml

```yaml
server:
  port: 8081

spring:
  application:
    name: product-service

  datasource:
    url: jdbc:mysql://localhost:3306/product_db
    username: root
    password: password

eureka:
  client:
    service-url:
      defaultZone: http://localhost:8761/eureka
```

---

## 📄 .gitignore

Add this to the `.gitignore` file:

```
# IDEs and OS
.idea/
.vscode/
.DS_Store

# Logs
*.log

# Build
target/
```

---

## 📘 Notes

- The `ecommerce-config-repo` is required by Spring Cloud Config Server to serve properties to each service.
- Each service loads its own configuration using the `spring.application.name` key.

---
