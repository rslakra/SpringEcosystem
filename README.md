# Spring Ecosystem

A collection of Spring sample projects in three groups: plain Spring Framework configuration styles (`Spring`), Spring Boot services (`SpringBoot`), and Spring Security demonstrations (`SpringSecurity`).

## 🚀 Quick Start

Each sample is a standalone Maven project. Build and run one (here `spring-security-filter-chain`):

```bash
cd SpringSecurity/spring-security-filter-chain

./buildMaven.sh          # or: mvn clean package
./runMaven.sh            # or: java -jar target/spring-security-filter-chain.jar
```

The app listens on `http://localhost:8080`. For default users, ports and per-module settings, see the [SpringSecurity README](SpringSecurity/README.md). The `Spring` and `SpringBoot` READMEs cover their own projects.

## ✨ Features

- **Spring Framework** — the same Customer service configured with XML, Java, annotations and core concepts
- **Spring Boot services** — REST APIs, JPA, JSP and Thymeleaf views, JWT authentication, email, AOP and OAuth2 resource servers
- **Spring Security demos** — filter chains, custom authentication, method security, JWT and OAuth 2.0
- **Modern stack** — Java 21, Spring Boot 3.5.7, Spring Security 6.x and Jakarta EE (migrated from `javax`)
- **Continuous integration** — one GitHub Actions workflow per project folder

## 📋 Prerequisites & Dependencies

- Java 21
- Maven 3.6+ (Gradle 7+ for `SpringBoot/springboot-service`, which also builds with Gradle)

| Technology | Version |
| ---------- | ------- |
| Java | 21 |
| Spring Boot | 3.5.7 |
| Spring Security | 6.x |
| Jakarta EE | 9+ (migrated from `javax`) |

Module-specific requirements (databases, Docker) are listed in each group's README.

### Limits

Several projects (`SpringBoot/email-service`, `SpringBoot/jwt-authentication`, `SpringBoot/spring-aop-services/spring-aop-before-advice`, `SpringBoot/spring-aop-services/spring-aop-task-service` and `SpringSecurity/jwt-authentications/jwt-authentication6`) depend on `com.rslakra.appsuite:appsuite-core` and `appsuite-spring`. Those artifacts are not on Maven Central and the poms declare no repository for them, so the projects build only where the artifacts are already installed (for example in `~/.m2`). CI skips them; see **⚙️ Build & Configuration**.

## ⚙️ Build & Configuration

Build and run each module from its own folder with `./buildMaven.sh` and `./runMaven.sh` (the `Spring` projects use `./runMaven.sh` too). Settings live in each module's `src/main/resources/application.properties` (or `application.yml`). See each group's README for the details.

### Deploy

Continuous integration runs in GitHub Actions. The workflows in `.github/workflows/` trigger on pushes and pull requests that touch their folder or the workflow file itself, and can also be started manually. There is one workflow for each project folder:

| Workflow | What it builds |
| -------- | -------------- |
| `spring-annotation-ci.yml` | `Spring/spring-annotation` |
| `spring-core-ci.yml` | `Spring/spring-core` |
| `spring-java-ci.yml` | `Spring/spring-java` |
| `spring-xml-ci.yml` | `Spring/spring-xml` |
| `springboot-email-service-ci.yml` | `SpringBoot/email-service` (manual only, see below) |
| `springboot-example-ci.yml` | `SpringBoot/springboot-example` |
| `springboot-jwt-authentication-ci.yml` | `SpringBoot/jwt-authentication` (manual only, see below) |
| `spring-aop-services-ci.yml` | `SpringBoot/spring-aop-services/spring-aop-around-advice`, `spring-aop-service` |
| `spring-resource-servers-ci.yml` | `SpringBoot/spring-resource-servers/springboot-resource-server`, `springboot-resource-server-access` |
| `springboot-service-ci.yml` | `SpringBoot/springboot-service` |
| `springboot-service-jsp-ci.yml` | `SpringBoot/springboot-service-jsp` |
| `springsecurity-component-based-security-ci.yml` | `SpringSecurity/component-based-security` |
| `springsecurity-enable-method-security-ci.yml` | `SpringSecurity/enable-method-security` |
| `springsecurity-java-jwt-based-security-ci.yml` | `SpringSecurity/java-jwt-based-security` |
| `springsecurity-jwt-authentications-ci.yml` | `SpringSecurity/jwt-authentications/jwt-authentication1`, `3`, `4`, `5`, `7` |
| `springsecurity-spring-oauth-clients-ci.yml` | `SpringSecurity/spring-oauth-clients/springboot-oauth-client`, `springboot-oauth2-service` |
| `springsecurity-spring-security-filter-chain-ci.yml` | `SpringSecurity/spring-security-filter-chain` |
| `springsecurity-spring-security-web-login-ci.yml` | `SpringSecurity/spring-security-web-login` |

Each job runs `mvn -B -ntp test` on JDK 21 (Temurin). The `Spring` projects have no tests yet, so their jobs compile the code and run Checkstyle.

The AppSuite-dependent projects can't be resolved on a clean runner:
- `springboot-email-service-ci.yml` and `springboot-jwt-authentication-ci.yml` run manually only. Re-enable their `push` and `pull_request` triggers (commented out in each file) once the artifacts are published.
- `spring-aop-services-ci.yml` leaves out `spring-aop-before-advice` and `spring-aop-task-service`.
- `jwt-authentication6` is excluded from `springsecurity-jwt-authentications-ci.yml`.

## 📁 Project Layout

```
SpringEcosystem/
├── .github/
│   └── workflows/                  # CI: one workflow per project folder
├── Spring/                         # Spring Framework configuration styles
│   ├── spring-annotation/
│   ├── spring-core/
│   ├── spring-java/
│   ├── spring-xml/
│   └── README.md                   # Index of the Spring projects
├── SpringBoot/                     # Spring Boot services
│   ├── email-service/
│   ├── jwt-authentication/
│   ├── spring-aop-services/
│   ├── spring-resource-servers/
│   ├── springboot-example/
│   ├── springboot-service/
│   ├── springboot-service-jsp/
│   ├── buildMaven.sh               # Builds every Maven project here
│   └── README.md                   # Index of the Spring Boot services
├── SpringSecurity/                 # Spring Security samples
│   ├── component-based-security/
│   ├── enable-method-security/
│   ├── java-jwt-based-security/
│   ├── jwt-authentications/
│   ├── spring-oauth-clients/
│   ├── spring-security-filter-chain/
│   ├── spring-security-web-login/
│   ├── DUPLICATE_ANALYSIS.md       # Analysis of duplicate JWT projects
│   └── README.md                   # Index of the Spring Security modules
├── .gitignore                      # The .gitignore file
└── README.md                       ← you are here
```

## 🧪 Testing

```bash
cd <group>/<module>
mvn -B -ntp test
```

## 🛠️ Troubleshooting

| Issue | Fix |
| ----- | --- |
| Build fails on a Java version error | Use JDK 21 — `java -version` shows the current one |
| A module won't start because the port is taken | Stop the other process, or set `server.port` in the module's `application.properties` |
| A build can't resolve `com.rslakra.appsuite:appsuite-core` or `appsuite-spring` | These are not on Maven Central. Install them first (they resolve locally from `~/.m2`), or publish them to a repository the pom declares |

Other module-specific problems are covered in each group's README.

## 📚 References

### In this repository

This is an index README. It links each group's README, which in turn indexes the modules in that group.

| Module | Link | Description |
| ------ | ---- | ----------- |
| `Spring` | [Spring/README.md](Spring/README.md) | Spring Framework applications using XML, Java, annotation and core configuration |
| `SpringBoot` | [SpringBoot/README.md](SpringBoot/README.md) | Spring Boot services: REST, JPA, JSP, JWT, email, AOP and resource servers |
| `SpringSecurity` | [SpringSecurity/README.md](SpringSecurity/README.md) | Spring Security samples: filter chains, custom authentication, method security, JWT and OAuth 2.0 |

### External Documentation

| Link | Description |
| ---- | ----------- |
| [Spring Security Documentation](https://docs.spring.io/spring-security/reference/index.html) | Spring Security reference |
| [Spring Boot Documentation](https://docs.spring.io/spring-boot/docs/current/reference/html/) | Spring Boot reference |
| [Spring Authorization Server](https://docs.spring.io/spring-authorization-server/reference/) | Authorization server reference |
| [Jakarta EE Migration Guide](https://jakarta.ee/specifications/servlet/6.0/) | `javax` to `jakarta` migration |

## 📄 License

These are educational examples and demonstrations of Spring, Spring Boot and Spring Security features.

## 👤 Author

- **Rohtash Lakra** — [@rslakra](https://github.com/rslakra)
