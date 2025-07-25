# Real Estate API

The **Real Estate API** is a RESTful service for managing real estate data, such as companies, housing units, promotions, and geographical populations. Built with Spring Boot, it follows a layered architecture to promote clean separation of concerns and maintainability.

## Technologies Used

- **Spring Boot**
- **Spring MVC**
- **Spring Data JPA**
- **H2
- **Swagger / OpenAPI**
- **Java 17+**

## Features

- CRUD operations for:
    - Companies
    - Promotions
    - Housing units
    - Populations
    - Real State
- Entity relationships (e.g. OneToMany, ManyToOne)
- Input validation using annotations
- Exception handling
- Swagger UI for testing and exploring the API

## Getting Started

### Prerequisites

- Java 17+
- Maven 3.6+
- (Optional) MySQL if not using H2

### How to Run the Project

1. Clone the Repository
```bash
git clone https://github.com/Yannx79/Real-State-API.git
cd real-estate-api
```

2. Configure the Database
```properties
# src/main/resources/application.properties

spring.datasource.url=jdbc:h2:mem:testdb
spring.datasource.driverClassName=org.h2.Driver
spring.datasource.username=sa
spring.datasource.password=

spring.jpa.database-platform=org.hibernate.dialect.H2Dialect
spring.h2.console.enabled=true
```

3. Run the Application
```bash
./mvnw spring-boot:run
```

### 4. Access the API

| Resource        | URL                                                   | Description                             |
|-----------------|-------------------------------------------------------|-----------------------------------------|
| **Swagger UI**  | [http://localhost:8080/swagger-ui/index.html](http://localhost:8080/swagger-ui/index.html) | Interactive API documentation           |
| **H2 Console**  | [http://localhost:8080/h2-console](http://localhost:8080/h2-console)                   | In-memory database console (for H2)     |
| **Base API URL**| `http://localhost:8080`                               | Base path for all REST endpoints        |

### 5. References DBML Code Block

```sql
Table PROMOCION {
  Codigo_Interno varchar [pk]
  Nombre varchar
}

Table INMOBILIARIA {
  Codigo_Interno varchar [pk]
  Codigo_Em varchar [fk]
  Importe decimal
}

Table VIVIENDA {
  ID_Vivienda varchar [pk]
  Superficie decimal
  Numero_Habitaciones integer
  Numero_Baños integer
  Plano_Vivienda text
  Foto text
  Precio decimal
  Terraza boolean
  Jardin_Privado boolean
  Piscina boolean
  Garaje boolean
  Codigo_Interno varchar [fk]
}

Table POBLACION {
  Codigo_Poblacion varchar [pk]
  Nombre varchar
  Planos text
  Codigo_Interno varchar [fk]
}

Table EMPRESA {
  Codigo_Em varchar [pk]
  Nombre varchar
  Tipo varchar
  Direccion varchar
  Telefono varchar
  Fax varchar
  Email varchar
}

Ref: PROMOCION.Codigo_Interno < VIVIENDA.Codigo_Interno
Ref: PROMOCION.Codigo_Interno < POBLACION.Codigo_Interno
Ref: EMPRESA.Codigo_Em < INMOBILIARIA.Codigo_Em
```