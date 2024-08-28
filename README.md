# BoilerPlate-HexagonalArchitecture
___
This project is a boilerplate for building applications in **Java** using **Spring Boot** with a structure based on **Hexagonal Architecture**, combined with **Vertical Slicing** and **Screaming Architecture** approaches. The purpose of this boilerplate is to provide a solid, scalable foundation for developing microservices with a clean, well-structured, and easy-to-maintain design.

## Table of Contents

- [Introduction](#introduction)
- [Hexagonal Architecture](#hexagonal-architecture)
- [Vertical Slicing](#vertical-slicing)
- [Screaming Architecture](#screaming-architecture)
- [Project Structure](#project-structure)
- [Getting Started](#getting-started)
- [Dependencies](#dependencies)
- [Usage](#usage)

## Introduction

This boilerplate uses an advanced software design approach that combines three key architectural patterns:

1. **Hexagonal Architecture**: To ensure framework independence and component decoupling.
2. **Vertical Slicing**: To split the project into vertical slices, facilitating separation of concerns.
3. **Screaming Architecture**: To make the architecture of the project clearly reflect its intentions and use cases.

## Hexagonal Architecture

### What is Hexagonal Architecture?

**Hexagonal Architecture** (also known as **Ports and Adapters Architecture**) is a software design pattern that promotes the decoupling of system components by separating the core business logic from the rest of the application. The architecture is divided into three main parts:

- **Domain Core**: Contains the business logic and domain entities. It has no external dependencies.
- **Ports**: Interfaces that define the operations the core needs from other systems or that other systems need from the core.
- **Adapters**: Implementations of ports that enable communication between the domain core and the outside world (e.g., APIs, databases, user interfaces).

## Vertical Slicing

### What is Vertical Slicing?

**Vertical Slicing** is a design approach that involves dividing the system into vertical slices that cover all layers of the application (e.g., controller, service, repository). Instead of dividing the code by horizontal layer (such as having separate folders for controllers, services, etc.), each slice represents a feature or functionality end-to-end.

## Screaming Architecture

### What is Screaming Architecture?

**Screaming Architecture** is a term coined by **Robert C. Martin (Uncle Bob)** that emphasizes that a system's architecture should "scream" about the system's purpose. In other words, the project's organization should immediately make it clear what the use cases and main functionalities of the system are.

## Project Structure

This project follows a structure that combines these three approaches to maximize the benefits:

```plaintext
/src
|-- /main
|   |-- /java
|   |   |-- /com
|   |   |   |-- /erikssonherlo
|   |   |   |   |-- /users-service                # Vertical Slice for 'users-service'
|   |   |   |   |   |-- /application              # Application Layer
|   |   |   |   |   |   |-- /usecases             # Use cases specific to 'users-service'
|   |   |   |   |   |   |   |-- RegisterUserUseCase.java
|   |   |   |   |   |   |   |-- LoginUserUseCase.java
|   |   |   |   |   |   |-- /dto                  # Data Transfer Objects
|   |   |   |   |   |   |   |-- UserDTO.java
|   |   |   |   |   |   |   |-- LoginRequestDTO.java
|   |   |   |   |   |   |-- /ports                # Ports (interfaces for input/output)
|   |   |   |   |   |   |   |-- RegisterUserInputPort.java
|   |   |   |   |   |   |   |-- LoginUserInputPort.java
|   |   |   |   |   |   |   |-- UserRepositoryPort.java
|   |   |   |   |   |-- /domain                       # Domain Layer
|   |   |   |   |   |   |-- /model                    # Domain Entities
|   |   |   |   |   |   |   |-- User.java
|   |   |   |   |   |-- /infrastructure               # Infrastructure Layer
|   |   |   |   |   |   |-- /adapter
|   |   |   |   |   |   |   |-- /input                # Input Adapters (Controllers, Filters)
|   |   |   |   |   |   |   |   |-- UserController.java
|   |   |   |   |   |   |   |   |-- JWTAuthenticationFilter.java
|   |   |   |   |   |   |   |-- /output               # Output Adapters (Persistence)
|   |   |   |   |   |   |   |   |-- UserJpaRepositoryAdapter.java
|   |   |   |   |   |   |-- /config                   # Configuration Classes
|   |   |   |   |   |   |   |-- SecurityConfig.java
|   |   |   |   |   |   |   |-- SwaggerConfiguration.java
|   |   |   |   |   |   |   |-- ApplicationConfiguration.java
|   |   |   |   |   |   |   |-- SchedulingConfiguration.java
|   |   |   |   |   |   |-- /cron                     # Cron Jobs and Scheduled Tasks
|   |   |   |   |   |   |   |-- ReservationScheduler.java
|   |   |   |   |   |   |-- /migrations               # Database Migrations (Flyway or Liquibase)
|   |   |   |   |   |   |   |-- V1__Create_Users_Table.sql
|   |   |   |   |   |-- /common                       # Common Utilities and Shared Services
|   |   |   |   |   |   |-- /security
|   |   |   |   |   |   |   |-- JWTService.java
|   |   |   |   |   |   |-- /exceptions               # Custom Exceptions
|   |   |   |   |   |   |   |-- UserNotFoundException.java
|   |-- /resources                                # Resources Directory
|   |   |-- /db
|   |   |   |-- /migrations                       # SQL Migration Files
|   |   |   |   |-- V1__Create_Users_Table.sql
|   |   |-- application.properties                # Spring Boot Application Properties
|   |   |-- application-dev.properties            # Development Configuration Properties
|   |   |-- application-prod.properties           # Production Configuration Properties
|-- /test
|   |-- /java
|   |   |-- /com
|   |   |   |-- /erikssonherlo
|   |   |   |   |-- /users-service
|   |   |   |   |   |-- /application
|   |   |   |   |   |   |-- /usecases             # Unit Tests for Use Cases
|   |   |   |   |   |   |   |-- RegisterUserUseCaseTest.java
|   |   |   |   |   |-- /infrastructure
|   |   |   |   |   |   |-- /adapter              # Integration Tests for Adapters
|   |   |   |   |   |   |   |-- UserControllerTest.java
|   |   |   |   |   |-- /common
```

## Getting Started

1. **Clone the repository:**

   ```bash
   git clone https://github.com/erikssonherlo/BoilerPlate-HexagonalArchitecture.git
   cd BoilerPlate-HexagonalArchitecture
   ```

2. **Build the project:**

   Make sure you have Maven and Java installed and properly configured.

   ```bash
   mvn clean install
   ```

3. **Run the project:**

   ```bash
   mvn spring-boot:run
   ```

## Dependencies

The project utilizes several Spring Boot dependencies and other libraries to facilitate modern and secure application development. Key dependencies include:

- **Spring Boot Starters**: Simplify the configuration of web applications, JPA, and security.
- **JSON Web Tokens (JWT)**: For secure token-based authentication and authorization.
- **JasperReports**: For generating reports in PDF format.
- **Flyway**: For database migration and versioning.
- **Lombok**: To reduce boilerplate code in Java.

## Usage

This boilerplate provides a solid foundation for developing microservices in Java using modern design principles. You can extend the functionality by adding new domain layers, use cases, and adapters following the hexagonal architecture structure. Ensure that you maintain a focus on separation of concerns and clarity of purpose in each module to fully leverage the benefits of this architecture.
