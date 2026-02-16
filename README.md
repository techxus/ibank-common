# ibank-common

![Java](https://img.shields.io/badge/Java-17-blue) ![Spring
Boot](https://img.shields.io/badge/Spring%20Boot-3.x-brightgreen)
![Build](https://img.shields.io/badge/Build-Maven-orange)
![Architecture](https://img.shields.io/badge/Architecture-Microservices-purple)
![Status](https://img.shields.io/badge/Status-Active-success)

Shared platform libraries for **iBank Spring Boot microservices**.

This repository removes duplication across services by centralizing:

-   **Maven versions & plugins** → `ibank-parent`
-   **Shared DTOs, events, enums, and exceptions** → `ibank-model`
-   **Shared runtime dependencies and default configuration** →
    `ibank-starter`

------------------------------------------------------------------------

# Repository Structure

  -----------------------------------------------------------------------------
  Module              Packaging             Purpose           Used By
  ------------------- --------------------- ----------------- -----------------
  **ibank-parent**    `pom`                 Centralized       All services
                                            dependency &      
                                            plugin management 

  **ibank-model**     `jar`                 Shared DTOs,      All services
                                            events, enums,    
                                            exceptions        

  **ibank-starter**   `jar`                 Shared Spring     MVC services only
                                            Boot runtime      
                                            stack + defaults  
  -----------------------------------------------------------------------------

> **Gateway is reactive (WebFlux / Spring Cloud Gateway)** and must
> **NOT** depend on `ibank-starter`.

------------------------------------------------------------------------

# Architecture Overview

                    +----------------------+
                    |      API Gateway     |
                    |    (Reactive WebFlux)|
                    +----------+-----------+
                               |
            -----------------------------------------------
            |                |               |            |
    +---------------+ +---------------+ +---------------+ +---------------+
    | User Service  | | Account Serv. | | Txn Service   | | Notification   |
    | MVC + JPA     | | MVC + JPA     | | MVC + JPA     | | MVC + Kafka    |
    +-------+-------+ +-------+-------+ +-------+-------+ +-------+-------+
            |                 |                 |               |
            -----------------------------------------------------
                                  |
                        +-----------------------+
                        |      ibank-common     |
                        | parent / model / starter |
                        +-----------------------+

------------------------------------------------------------------------

# Build Locally

From the repository root:

``` bash
mvn -q clean install
```

Artifacts are installed to:

    ~/.m2/repository/com/ibank

Installed artifacts:

-   `ibank-parent`
-   `ibank-model`
-   `ibank-starter`

------------------------------------------------------------------------

# How Services Use These Modules

## Parent Configuration

``` xml
<parent>
  <groupId>com.ibank</groupId>
  <artifactId>ibank-parent</artifactId>
  <version>1.0.0</version>
</parent>
```

## Shared Dependencies

``` xml
<dependency>
  <groupId>com.ibank</groupId>
  <artifactId>ibank-starter</artifactId>
</dependency>

<dependency>
  <groupId>com.ibank</groupId>
  <artifactId>ibank-model</artifactId>
</dependency>
```

------------------------------------------------------------------------

# Observability Stack

-   **Spring Boot Actuator** --- Health checks and metrics\
-   **Micrometer + Prometheus** --- Metrics collection\
-   **OpenTelemetry (OTLP)** --- Distributed tracing\
-   **Splunk Java Logging** --- Centralized log export

------------------------------------------------------------------------

# Data & Caching

-   **Spring Data JPA** --- Database access\
-   **Flyway** --- Versioned schema migrations\
-   **PostgreSQL JDBC Driver** --- Database connectivity\
-   **Spring Cache + Redis** --- Distributed caching

------------------------------------------------------------------------

# Publishing Artifacts (GitHub Packages)

## Authenticate

``` bash
export GITHUB_TOKEN=YOUR_TOKEN
```

## Deploy

``` bash
mvn clean deploy
```

Artifacts will be published to:

    https://maven.pkg.github.com/<org>/ibank-common

------------------------------------------------------------------------

# Architectural Rules

## MVC Services

Must include:

-   `ibank-parent`
-   `ibank-model`
-   `ibank-starter`

## Reactive Gateway

Must include only:

-   `ibank-parent`
-   `ibank-model`

Must **NOT** include MVC, JPA, Redis, or Flyway dependencies.

------------------------------------------------------------------------

# Purpose

Provides a **production‑grade shared microservice foundation**:

-   Consistent builds across services\
-   Standardized domain contracts\
-   Unified observability integration\
-   Faster microservice development

------------------------------------------------------------------------

# License

**Internal --- iBank Platform**
