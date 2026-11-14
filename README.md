# Spring Ecosystem

A collection of Spring sample projects. It currently holds the `SpringSecurity` suite: Spring Boot demonstrations of authentication and authorization mechanisms, security configurations and best practices.

## 🚀 Quick Start

Each sample is a standalone Maven project. Build and run one (here `spring-security-filter-chain`):

```bash
cd SpringSecurity/spring-security-filter-chain

./buildMaven.sh          # or: mvn clean package
./runMaven.sh            # or: java -jar target/spring-security-filter-chain.jar
```

The app listens on `http://localhost:8080`. For default users, ports and per-module settings, see the [SpringSecurity README](SpringSecurity/README.md).

## ✨ Features

- **Spring Security demos** — filter chains, custom authentication, method security, JWT and OAuth 2.0
- **Modern stack** — Java 21, Spring Boot 3.5.7, Spring Security 6.x and Jakarta EE (migrated from `javax`)
- **Continuous integration** — one GitHub Actions workflow per `SpringSecurity` folder builds and tests every module that can run on a clean runner

## 📋 Prerequisites & Dependencies

- Java 21
- Maven 3.6+

| Technology | Version |
| ---------- | ------- |
| Java | 21 |
| Spring Boot | 3.5.7 |
| Spring Security | 6.x |
| Jakarta EE | 9+ (migrated from `javax`) |

Module-specific requirements (databases, Docker) are listed in the `SpringSecurity` README.

## ⚙️ Build & Configuration

Build and run each module from its own folder with `./buildMaven.sh` and `./runMaven.sh`. Settings live in each module's `src/main/resources/application.properties` (or `application.yml`). See the `SpringSecurity` README for the details.

### Deploy

Continuous integration runs in GitHub Actions. The workflows in `.github/workflows/` trigger on pushes and pull requests that touch their module's folder or the workflow file itself, and can also be started manually.

There is one workflow for each folder under `SpringSecurity/`:

| Workflow | What it builds |
| -------- | -------------- |
| `spring-security-component-based-security-ci.yml` | `component-based-security` |
| `spring-security-enable-method-security-ci.yml` | `enable-method-security` |
| `spring-security-filter-chain-ci.yml` | `spring-security-filter-chain` |
| `spring-security-java-jwt-based-security-ci.yml` | `java-jwt-based-security` |
| `spring-security-jwt-authentications-ci.yml` | `jwt-authentications/jwt-authentication1`, `3`, `4`, `5`, `7` |
| `spring-security-oauth-clients-ci.yml` | `spring-oauth-clients/springboot-oauth-client`, `springboot-oauth2-service` |
| `spring-security-web-login-ci.yml` | `spring-security-web-login` |

Each job runs `mvn -B -ntp test` on JDK 21 (Temurin). `jwt-authentication6` is excluded because its AppSuite dependencies can't be resolved on a clean runner.

## 📁 Project Layout

```
SpringEcosystem/
├── .github/
│   └── workflows/                  # CI: one workflow per SpringSecurity folder
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
cd SpringSecurity/<module>
mvn -B -ntp test
```

## 🛠️ Troubleshooting

| Issue | Fix |
| ----- | --- |
| Build fails on a Java version error | Use JDK 21 — `java -version` shows the current one |
| A module won't start because the port is taken | Stop the other process, or set `server.port` in the module's `application.properties` |

Module-specific problems, such as the `jwt-authentication6` dependency issue, are covered in the `SpringSecurity` README.

## 📚 References

### In this repository

This is an index README. It links the suite's README, which in turn indexes every module.

| Module | Link | Description |
| ------ | ---- | ----------- |
| `SpringSecurity` | [SpringSecurity/README.md](SpringSecurity/README.md) | Spring Security samples: filter chains, custom authentication, method security, JWT and OAuth 2.0 |

### External Documentation

| Link | Description |
| ---- | ----------- |
| [Spring Security Documentation](https://docs.spring.io/spring-security/reference/index.html) | Spring Security reference |
| [Spring Boot Documentation](https://docs.spring.io/spring-boot/docs/current/reference/html/) | Spring Boot reference |
| [Spring Authorization Server](https://docs.spring.io/spring-authorization-server/reference/) | Authorization server reference |
| [Jakarta EE Migration Guide](https://jakarta.ee/specifications/servlet/6.0/) | `javax` to `jakarta` migration |

## 📄 License

These are educational examples and demonstrations of Spring Security features.

## 👤 Author

- **Rohtash Lakra** — [@rslakra](https://github.com/rslakra)
