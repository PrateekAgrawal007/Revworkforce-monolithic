# Phase 7: End-to-End Testing & Polish

Run the full RevWorkforce stack, fix any remaining issues, and verify the core workflows work end-to-end.

## User Review Required

> [!IMPORTANT]
> **Before anything can run, I need your answers to two things:**
> 1. **MySQL credentials** — The [application.properties](file:///e:/managementproject/revworkforce/backend/src/main/resources/application.properties) has `username=root` and `password=yourpassword`. What is your actual MySQL root password? (Or do you prefer a different user?)
> 2. **Tools on PATH** — `mysql` and `mvn` are not found on PATH. Please confirm:
>    - Is MySQL Server installed? If yes, what is the install path (e.g. `C:\Program Files\MySQL\MySQL Server 8.0\bin`)?
>    - Is Maven installed? If yes, what is the path to `mvn`?  
>    - Is Java 17+ installed? If yes, is [java](file:///e:/managementproject/revworkforce/backend/src/main/java/com/revworkforce/RevWorkforceApplication.java) on PATH?
>
> **Alternatively**: If you have XAMPP/WAMP, tell me and I'll provide commands using the bundled MySQL.

> [!WARNING]
> The seed Admin user in [schema.sql](file:///e:/managementproject/revworkforce/schema.sql) has a **dummy BCrypt hash** that won't authenticate. I will replace it with a real BCrypt hash of `Admin@123` before running the schema.

---

## Proposed Changes

### Database Setup

#### [MODIFY] [schema.sql](file:///e:/managementproject/revworkforce/schema.sql)
- Uncomment `CREATE DATABASE IF NOT EXISTS revworkforce_db;` and `USE revworkforce_db;`
- Replace the placeholder BCrypt hash with a valid BCrypt hash of `Admin@123`

---

### Backend Configuration

#### [MODIFY] [application.properties](file:///e:/managementproject/revworkforce/backend/src/main/resources/application.properties)
- Update `spring.datasource.password` to your actual MySQL root password
- Change `spring.jpa.hibernate.ddl-auto` from `validate` to `none` (schema created manually via SQL)

---

## Verification Plan

### Step 1 — Database Init (manual, 2 commands)
Once you confirm MySQL is running and provide credentials:
```sql
-- Run in MySQL shell or client:
SOURCE e:/managementproject/revworkforce/schema.sql
```
Or via command line:
```
mysql -u root -p < e:\managementproject\revworkforce\schema.sql
```

### Step 2 — Backend Unit Tests (automated)
```
cd e:\managementproject\revworkforce\backend
mvn test
```
Covers: [EmployeeServiceImplTest](file:///e:/managementproject/revworkforce/backend/src/test/java/com/revworkforce/service/impl/EmployeeServiceImplTest.java#25-97), [LeaveServiceImplTest](file:///e:/managementproject/revworkforce/backend/src/test/java/com/revworkforce/service/impl/LeaveServiceImplTest.java#28-118), `PerformanceServiceImplTest` (Mockito, no DB needed).

### Step 3 — Start Backend
```
cd e:\managementproject\revworkforce\backend
mvn spring-boot:run
```
Backend runs on `http://localhost:8080`. Verify: `GET http://localhost:8080/api/auth/login` returns HTTP 405 (Method Not Allowed — correct, POST only).

### Step 4 — Start Frontend
```
cd e:\managementproject\revworkforce\frontend
npx ng serve
```
Frontend runs on `http://localhost:4200`.

### Step 5 — Manual E2E flows

| Flow | Steps |
|------|-------|
| **Admin login** | Go to `localhost:4200/login`, enter `admin@revworkforce.com` / `Admin@123`, verify dashboard loads |
| **Add Manager** | Admin → Employee List → Add Employee (role: Manager) |
| **Add Employee** | Admin → Employee List → Add Employee (role: Employee, manager = just-created manager) |
| **Leave flow** | Login as Employee → Apply Leave → Login as Manager → Approve → verify dashboard balances |
| **Performance flow** | Login as Employee → Submit self-assessment → Login as Manager → Add review/rating |
| **Notifications** | Verify bell icon shows new notification after leave approval |
