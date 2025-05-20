---
home: true
heroImage: /logo.png
heroText: Sistema de Registro Universitario
tagline: Backend RESTful con Spring Boot · JWT · PostgreSQL · Redis · Swagger
actionText: Empezar →
actionLink: #estructura-del-proyecto
features:
  - title: 🔐 Autenticación & Seguridad
    details:
      - JWT con roles `ADMIN` / `USER`
      - Filtros de Spring Security
      - Protección de endpoints
  - title: 🎓 Gestión de Estudiantes
    details:
      - CRUD completo (Create, Read, Update, Delete lógico)
      - Validaciones con `@NotNull`, `@Email`, etc.
      - Caché con Redis
  - title: 📘 Gestión de Materias
    details:
      - CRUD materias
      - Asignación Docente ↔ Materia
      - Validaciones y manejo de errores
  - title: 📝 Inscripciones
    details:
      - CRUD de inscripciones por estudiante
      - Validaciones de negocio
---

# 📚 Sistema de Registro Universitario

## 📖 Descripción

Este proyecto es un **backend RESTful** construido con **Spring Boot 3** para gestionar un sistema universitario:

- 🔐 **Autenticación**: JWT, roles `ADMIN`/`USER`  
- 🎓 **Estudiantes**: CRUD con validaciones y caché  
- 📘 **Materias**: CRUD, asignación a docentes  
- 📝 **Inscripciones**: CRUD por estudiante  
- 🔄 **Cache**: Redis  
- 🐘 **Persistencia**: PostgreSQL  
- 🛡 **Manejo de excepciones**: `@RestControllerAdvice`  
- 📜 **Documentación**: Swagger / OpenAPI  

---

## 🏗 Estructura del proyecto

```text
src/
└── main/
    ├── java/
    │   └── com.universidad/
    │       ├── controller/
    │       │   ├── AuthController.java
    │       │   ├── UsuarioController.java
    │       │   ├── EstudianteController.java
    │       │   ├── MateriaController.java
    │       │   ├── DocenteController.java
    │       │   └── InscripcionController.java
    │       ├── dto/
    │       │   ├── AuthDTO.java
    │       │   ├── UsuarioDTO.java
    │       │   ├── EstudianteDTO.java
    │       │   ├── MateriaDTO.java
    │       │   └── InscripcionDTO.java
    │       ├── model/
    │       │   ├── Usuario.java
    │       │   ├── Rol.java
    │       │   ├── Estudiante.java
    │       │   ├── Materia.java
    │       │   ├── Docente.java
    │       │   └── Inscripcion.java
    │       ├── repository/
    │       ├── service/
    │       │   ├── I*Service.java
    │       │   └── impl/
    │       ├── security/
    │       └── validation/
    └── resources/
        ├── application.properties
        └── schema.sql


---

## ⚙️ Configuración

### 1. PostgreSQL

```properties
spring.datasource.url=jdbc:postgresql://localhost:5432/universidad
spring.datasource.username=postgres
spring.datasource.password=admin123
spring.jpa.hibernate.ddl-auto=validate
spring.jpa.show-sql=true
spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.PostgreSQLDialect

2. Redis Cache
spring.cache.type=redis
spring.redis.host=localhost
spring.redis.port=6379

En servicios:
@Cacheable("estudiantes")
public List<EstudianteDTO> listarEstudiantes() { … }

@CacheEvict(value="estudiantes", allEntries=true)
public EstudianteDTO crearEstudiante(…) { … }

3. JWT
app.jwtSecret=TU_SECRETO_LARGO_Y_COMPLEJO
app.jwtExpirationMs=86400000

4. Swagger / OpenAPI
springdoc.api-docs.enabled=true
springdoc.swagger-ui.enabled=true
springdoc.api-docs.path=/v3/api-docs
springdoc.swagger-ui.path=/swagger-ui.html

Acceso UI: http://localhost:8080/swagger-ui.html

🚀 Arranque
Levanta PostgreSQL y Redis.

Ajusta credenciales en application.properties.

Compila y ejecuta:

mvn clean install
java -jar target/mi-proyecto-spring-boot-0.0.1-SNAPSHOT.jar

