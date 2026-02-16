# ibank-model

Shared **pure Java domain library** used by all iBank microservices.

This module defines **stable service contracts** that allow
microservices to communicate **without tight coupling**.

---

## Purpose

Central place for:

- **DTOs** (request / response objects)
- **Events / messages** (Kafka, Axon, etc.)
- **Enums** (shared constants)
- **Exceptions** (standard error model)

➡ Ensures **consistent data structures across all services**.

---

## Design Principles

| Rule | Explanation |
|------|-------------|
| **No Spring dependencies** | Keeps contracts framework-independent |
| **No JPA entities** | Prevents persistence coupling |
| **Pure Java only** | Maximizes reuse across services |
| **Serializable objects** | Required for APIs and messaging |

---

## Typical Usage

```xml
<dependency>
  <groupId>com.ibank</groupId>
  <artifactId>ibank-model</artifactId>
  <version>1.0.0</version>
</dependency>
```

Used by:

- REST controllers  
- Kafka / Axon messaging  
- Shared error handling  

---

## What MUST NOT Be Added Here

❌ Business logic  
❌ Spring annotations  
❌ Database entities  
❌ Service-specific classes  

➡ This module must remain **contract-only**.

---

## Dependency Reference

| Dependency | Purpose | Docs | Maven |
|------------|---------|------|-------|
| Lombok (optional) | Reduce DTO boilerplate | https://projectlombok.org/ | https://mvnrepository.com/artifact/org.projectlombok/lombok |

---

## License

Internal educational use for **Techxus / iBank training platform**.  
See the root **LICENSE** file for full terms.
