# ibank-parent

Shared **Maven parent POM** for all iBank microservices.

This module guarantees **consistent builds, versions, and plugins**
across the entire platform.

---

# Responsibilities

- Defines **Spring Boot version**
- Defines **Java version**
- Centralizes **dependency versions**
- Centralizes **Maven plugin configuration**

Without this parent:

- Versions drift across services
- Builds become inconsistent
- Production bugs increase

➡ This module enforces **build stability across microservices**.

---

# Key Managed Dependencies

| Dependency | Why Used | Docs | Maven |
|------------|----------|------|-------|
| Spring Boot Parent | Controls dependency & plugin versions | https://docs.spring.io/spring-boot/docs/current/reference/html/ | https://mvnrepository.com/artifact/org.springframework.boot/spring-boot-starter-parent |
| Maven Compiler Plugin | Java compilation configuration | https://maven.apache.org/plugins/maven-compiler-plugin/ | https://mvnrepository.com/artifact/org.apache.maven.plugins/maven-compiler-plugin |
| Spring Boot Maven Plugin | Builds executable Boot JAR | https://docs.spring.io/spring-boot/docs/current/maven-plugin/reference/html/ | https://mvnrepository.com/artifact/org.springframework.boot/spring-boot-maven-plugin |
| Lombok | Compile-time code generation | https://projectlombok.org/ | https://mvnrepository.com/artifact/org.projectlombok/lombok |
| AWS MSK IAM Auth | Kafka IAM authentication | https://docs.aws.amazon.com/msk/latest/developerguide/iam-access-control.html | https://mvnrepository.com/artifact/software.amazon.msk/aws-msk-iam-auth |

---

# Who Uses This

**All microservices** must inherit:

```xml
<parent>
  <groupId>com.ibank</groupId>
  <artifactId>ibank-parent</artifactId>
  <version>1.0.0</version>
</parent>

```
# License

Internal educational use for **Techxus / iBank training platform**.  
See the `LICENSE` file for full terms.