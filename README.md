# RevWorkforce - HRM Management System

RevWorkforce is a modern, full-stack Human Resource Management (HRM) system designed for streamlined employee data management, leave tracking, and performance reviews.

## 🏗️ Tech Stack

- **Backend**: Java 17, Spring Boot 3.2.3, Spring Security (JWT), Spring Data JPA, MySQL 8
- **Frontend**: Angular 16, Angular Material, SCSS, Chart.js
- **Architecture**: REST API with JWT Authentication, Role-Based Access Control (RBAC)

---

## 📋 Prerequisites

Ensure you have the following installed on your system:

1. **Java 17 JDK** (e.g., Microsoft OpenJDK 17)
2. **Apache Maven 3.6+**
3. **MySQL Server 8.0+**
4. **Node.js 18+** & **npm**
5. **Angular CLI** (`npm install -g @angular/cli`)

---

## 🚀 Setup Instructions

### 1. Database Configuration

1. Log in to your MySQL terminal or client.
2. Initialize the database and seed data using the provided script:
   ```bash
   mysql -u root -p < schema.sql
   ```
   *This creates the `revworkforce_db` and inserts default departments, designations, leave types, and the initial Admin user.*

### 2. Backend Setup (`/backend`)

1. Open `backend/src/main/resources/application.properties`.
2. Update the MySQL credentials:
   ```properties
   spring.datasource.username=root
   spring.datasource.password=YOUR_MYSQL_PASSWORD_HERE
   ```
3. Run the backend application:
   ```bash
   cd backend
   mvn spring-boot:run
   ```
   *The server will start at `http://localhost:8080`.*

### 3. Frontend Setup (`/frontend`)

1. Install dependencies:
   ```bash
   cd frontend
   npm install
   ```
2. Start the development server:
   ```bash
   npx ng serve
   ```
   *Access the application at `http://localhost:4200`.*

---

## 🔐 Default Login Credentials

| Role | Email | Password |
|------|-------|----------|
| **Admin** | `admin@revworkforce.com` | `Admin@123` |

*Once logged in as Admin, you can create Managers and Employees through the Admin Dashboard.*
*This prateek and darshan are created by admin thorugh add employee feature with deafult password given below*
| **Employee** | `darshanraval@revworkforce.com` | `Welcome@123` |
| **Manager** | `prateekagrawal@revworkforce.com` | `Welcome@123` |
---

## ✨ Features

- **🔐 Secure Authentication**: JWT-based login with role-aware routing.
- **🏠 Role-Aware Dashboards**: Unique views for Admins, Managers, and Employees.
- **📅 Leave Management**:
  - Employees can apply for leave using a multi-step stepper.
  - Managers can approve/reject team leave requests.
- **📈 Performance & Goals**:
  - Structured self-assessments and manager ratings.
- **⚙️ Admin Controls**:
  - Employee lifecycle management.
  - System configuration (Departments, Designations, Holidays).
- **🔔 Notifications**: Real-time alerts for application status changes.

---

## 🛠️ Build & Testing

- **Backend Tests**: `mvn test`
- **Frontend Production Build**: `ng build --configuration production`


## to run backend 
*managementproject\managementproject\revworkforce\backend*
1. open cmd
2. cd backend
3. mvn spring-boot:run

## to run frontend
*managementproject\managementproject\revworkforce\frontend*
1. open cmd
2. cd frontend
3. ng serve
