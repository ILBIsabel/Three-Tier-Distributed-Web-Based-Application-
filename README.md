# CNT 4714 Project 4 – Three-Tier Distributed Web Application

A full-stack enterprise web application built with Java Servlets, JSP, Apache Tomcat, and MySQL, demonstrating a distributed three-tier architecture for managing a suppliers/parts/jobs/shipments database system.

This project implements role-based authentication, JDBC database connectivity, server-side business logic, stored procedure execution, and multiple user-level applications running through a Tomcat servlet container.

---

# Architecture Overview

## Tier 1 – Presentation Layer (Client Browser)

The front-end interface consists of an authentication landing page and four JSP-based user applications.

### Front-End Pages
- `authentication.html` – login page used to authenticate all users
- `rootHome.jsp` – root-level SQL command interface
- `clientHome.jsp` – client-level SQL command interface
- `dataEntryHome.jsp` – form-based data entry application
- `accountantHome.jsp` – accountant report selection interface

### Features
- JSP-based interfaces
- Inline results display without requiring full browser refresh
- SQL command execution interface for root/client users
- Form-based insertion interface for data-entry users
- Radio-button report interface for accountant users

---

## Tier 2 – Application Logic Layer (Apache Tomcat Servlets)

The application logic is implemented using Java Servlets running inside Apache Tomcat.

### Servlets
- `AuthenticationServlet`
  - Validates credentials against `credentialsDB`
  - Redirects authenticated users to the correct JSP page

- `RootUserServlet`
  - Executes arbitrary SQL commands
  - Implements server-side business logic

- `ClientUserServlet`
  - Executes SQL queries with restricted database permissions

- `AddSupplierRecordServlet`
- `AddPartRecordServlet`
- `AddJobRecordServlet`
- `AddShipmentRecordServlet`
  - Handle form-based inserts using `PreparedStatement`

- `AccountantRPCServlet`
  - Executes MySQL stored procedures using `CallableStatement`

- `ResultSetToHTMLFormatterClass`
  - Utility class that formats JDBC `ResultSet` data into styled HTML tables

### Business Logic
The application implements server-side business logic directly inside the servlet layer (not through database triggers).

When a shipment is inserted or updated with a quantity greater than or equal to 100:
- Supplier status values are automatically incremented by 5
- Logic is processed inside the Java servlet layer

---

## Tier 3 – Persistence Layer (MySQL Database)

### Databases
- `project4`
  - suppliers
  - parts
  - jobs
  - shipments

- `credentialsDB`
  - usercredentials

### Database Features
- Referential integrity enforced through foreign key constraints
- Composite primary key on the shipments table
- Stored procedures used for accountant-level reporting
- Role-based MySQL user permissions

---

# Key Features

- Three-tier distributed enterprise architecture
- Role-based authentication system
- JSP + Servlet web application design
- JDBC connectivity using MySQL Connector/J
- PreparedStatement implementation for secure data-entry operations
- CallableStatement implementation for remote procedure calls (RPC)
- Separate database properties files for each user role
- Dynamic HTML result formatting using JDBC metadata
- MySQL privilege enforcement by user type
- Business logic implemented in Java servlets
- Styled execution results and error handling
- Foreign key and referential integrity enforcement

---

# Technologies Used

| Layer | Technology |
|---|---|
| Language | Java |
| Frontend | HTML, JSP, CSS |
| Backend | Java Servlets |
| Database | MySQL |
| JDBC Driver | MySQL Connector/J 9.6.0 |
| Web Container | Apache Tomcat 11 |
| API | Jakarta Servlet API |
| Build/Compile | javac |

---

# Project Structure

```text
Project-4/
│
├── authentication.html
├── errorpage.html
├── rootHome.jsp
├── clientHome.jsp
├── dataEntryHome.jsp
├── accountantHome.jsp
│
├── src/
│   ├── AuthenticationServlet.java
│   ├── RootUserServlet.java
│   ├── ClientUserServlet.java
│   ├── AddSupplierRecordServlet.java
│   ├── AddPartRecordServlet.java
│   ├── AddJobRecordServlet.java
│   ├── AddShipmentRecordServlet.java
│   ├── AccountantRPCServlet.java
│   └── ResultSetToHTMLFormatterClass.java
│
├── screenshots/
│   ├── root-user screenshots
│   ├── client-user screenshots
│   ├── dataentry screenshots
│   └── accountant screenshots
│
└── WEB-INF/
    ├── web.xml
    ├── classes/
    ├── conf/
    │   ├── root.properties
    │   ├── client.properties
    │   ├── dataentry.properties
    │   ├── accountant.properties
    │   └── systemapp.properties
    │
    └── lib/
        └── mysql-connector-j-9.6.0.jar
```

## Running the Application

# Database Setup
1. Run project4DBscript.sql
2. Run credentialsDBscript.sql
3. Run ClientCreationPermissionsScript.sql
# Deployment
1. Place the Project-4 folder inside Tomcat’s webapps directory
2. Compile the servlet files
3. Start Apache Tomcat
4. Open: http://localhost:8082/Project-4/

