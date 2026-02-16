# ibank-starter

Reusable **Spring Boot starter** for all **MVC-based iBank microservices**.

This module standardizes:

- Runtime dependencies  
- Observability stack  
- Database & cache configuration  
- Default production settings  

➡ Ensures **consistent production behavior across services**.

---

## Overview

### Common Runtime Stack

| Area | Technology |
|------|------------|
| **Web** | Spring Boot MVC |
| **Observability** | Actuator + Micrometer + OpenTelemetry |
| **Logging** | Splunk Java logging |
| **Database** | JPA + PostgreSQL + Flyway |
| **Caching** | Redis + Spring Cache |

---

## Shared Default Configuration

Default configuration is provided in:

```
src/main/resources/application.yml
```

Includes sensible production defaults for:

- **Datasource / JPA / Flyway**
- **Redis caching**
- **Metrics & distributed tracing**
- **Health and readiness probes**

Each microservice should **override only what is unique**.

---

## Intentional Exclusions

| Not Included | Reason |
|-------------|--------|
| **Devtools** | Local-only dependency |
| **Tests** | Service-specific |
| **Kafka** | Not all services use messaging |
| **Security** | Added later via shared auto-configuration |
| **WebFlux** | Gateway is reactive and separate |

➡ Keeps the starter **minimal and reusable**.

---

## When to Add Code Here

Add functionality only if it is **shared infrastructure**, not business logic.

**Examples:**

- JWT authentication filter  
- Shared security configuration  
- Global exception handler  
- Tracing / logging interceptors  

➡ Rule: **If multiple services need it, it belongs here.**

---

## Dependency Reference

| Dependency | Purpose | Docs | Maven |
|------------|---------|------|-------|
| spring-boot-starter-web | REST MVC support | https://docs.spring.io/spring-boot/docs/current/reference/html/web.html | https://mvnrepository.com/artifact/org.springframework.boot/spring-boot-starter-web |
| spring-boot-starter-actuator | Health & metrics endpoints | https://docs.spring.io/spring-boot/docs/current/reference/html/actuator.html | https://mvnrepository.com/artifact/org.springframework.boot/spring-boot-starter-actuator |
| micrometer-registry-prometheus | Prometheus metrics export | https://micrometer.io/docs/registry/prometheus | https://mvnrepository.com/artifact/io.micrometer/micrometer-registry-prometheus |
| micrometer-tracing-bridge-otel | Micrometer → OpenTelemetry tracing bridge | https://micrometer.io/docs/tracing | https://mvnrepository.com/artifact/io.micrometer/micrometer-tracing-bridge-otel |
| opentelemetry-exporter-otlp | OTLP trace exporter | https://opentelemetry.io/docs/ | https://mvnrepository.com/artifact/io.opentelemetry/opentelemetry-exporter-otlp |
| splunk-library-javalogging | Structured logging to Splunk | https://github.com/splunk/splunk-library-javalogging | https://mvnrepository.com/artifact/com.splunk.logging/splunk-library-javalogging |
| spring-boot-starter-data-jpa | JPA database access | https://spring.io/projects/spring-data-jpa | https://mvnrepository.com/artifact/org.springframework.boot/spring-boot-starter-data-jpa |
| flyway-core | Database schema migrations | https://documentation.red-gate.com/flyway | https://mvnrepository.com/artifact/org.flywaydb/flyway-core |
| flyway-database-postgresql | PostgreSQL Flyway support | https://documentation.red-gate.com/flyway | https://mvnrepository.com/artifact/org.flywaydb/flyway-database-postgresql |
| postgresql | PostgreSQL JDBC driver | https://jdbc.postgresql.org/documentation/ | https://mvnrepository.com/artifact/org.postgresql/postgresql |
| spring-boot-starter-cache | Spring caching abstraction | https://docs.spring.io/spring-framework/reference/integration/cache.html | https://mvnrepository.com/artifact/org.springframework.boot/spring-boot-starter-cache |
| spring-boot-starter-data-redis | Redis integration | https://spring.io/projects/spring-data-redis | https://mvnrepository.com/artifact/org.springframework.boot/spring-boot-starter-data-redis |
| commons-pool2 | Redis connection pooling | https://commons.apache.org/proper/commons-pool/ | https://mvnrepository.com/artifact/org.apache.commons/commons-pool2 |

---

## License

Internal educational use for **Techxus / iBank training platform**.  
See the root **LICENSE** file for full terms.
