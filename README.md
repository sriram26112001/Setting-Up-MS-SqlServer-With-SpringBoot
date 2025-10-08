# Setting-Up-MS Sql-Server-With-SpringBoot
This project demonstrates how to configure and connect Spring Boot with Microsoft SQL Server.It covers everything from establishing a database connection

## Features
- DataBase Connection using application.properties

🧱 Tech Stack

- Java 17+
- Spring Boot 3.x
- Spring Data JPA
- Microsoft SQL Server
- Lombok (for cleaner code)

## Properties 

```md
Properties

# ===============================
# SPRING DATASOURCE CONFIGURATION (SQL AUTH)
# ===============================
spring.datasource.url=jdbc:sqlserver://LAPTOP-XXXXXXX\\SQLEXPRESS:1433;databaseName=user;encrypt=true;trustServerCertificate=true
spring.datasource.username=sa
spring.datasource.password=5326
spring.datasource.driver-class-name=com.microsoft.sqlserver.jdbc.SQLServerDriver

# ===============================
# JPA / HIBERNATE CONFIGURATION
# ===============================
spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.SQLServerDialect

# ===============================
# SERVER CONFIGURATION
# ===============================
server.port=8080
```

## 🔐 Setting Up SQL Server Password

Follow these steps to enable SQL Server authentication and set the sa account password for your Spring Boot integration.
## 🧭 Steps
### 1. Open SQL Server Management Studio (SSMS)
  - Connect using Windows Authentication.
### 2. Enable SQL Server Authentication
  - Right-click your server name → Properties → Security.
  - Under Server Authentication, select SQL Server and Windows Authentication mode.
  - Click OK.
  - Restart the SQL Server.
### 3. Set or Reset *sa* Password
  - Expand Security → Logins.
  - Right-click sa → Properties.
  - Under General, enter your new password.
  - Under Status, ensure Login is enabled.
  - Click OK.
  - Restart SQL Server.

## Setting Up SQL Server Configuration Manager 
SQL Server Configuration Manager is used to manage SQL Server services, network protocols, and connectivity, which is required for Spring Boot applications to connect successfully.

### 1. Open SQL Server Configuration Manager
- Press Win + S → Search SQL Server Configuration Manager → Open it.
### 2. Enable TCP/IP
- Navigate to SQL Server Network Configuration → Protocols for MSSQLSERVER.
- Right-click TCP/IP → Enable.
- Right-click TCP/IP → Properties → IP Addresses:
- Make sure TCP Port = 1433 for all active IPs.
- Ensure Enabled = Yes for IP1, IP2… and IPAll.

### 3. Restart SQL Server Service
- Go to SQL Server Services → SQL Server (MSSQLSERVER).
- Right-click → Restart.

### 4. Verify Connectivity
- Use SSMS or sqlcmd to ensure SQL Server accepts connections over TCP/IP.
- This ensures Spring Boot can connect using JDBC.

## 🏗️ Create Entities and Run Application

After setting up SQL Server and Spring Boot configuration, you can create your **JPA entities** and start the application.

### 1. Create an Entity
Example `User` entity:

```java
package com.example.UserService.user;

import jakarta.persistence.*;
import lombok.*;

@Data
@Builder
@NoArgsConstructor
@AllArgsConstructor
@Entity
@Table(name = "users") // avoid reserved keyword
public class User {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Integer id;

    @Column(nullable = false)
    private String firstName;

    @Column(nullable = false)
    private String lastName;

    @Column(unique = true, nullable = false)
    private String email;

    @Column(nullable = false)
    private String password;
}
```

## 🏃‍♂️ Run the springBoot Application
