# Research-Project-Database

## 📚 Research Projects Database - NIAT 

This project implements a relational database for managing research projects, employees, and funding agencies using SQL. The schema is based on a real-world academic or corporate research setting where:

- Projects are funded by agencies.
- Employees can work on multiple projects.
- Each project is managed by a single employee (who is also an employee).
- Funding agencies support multiple projects.

---

### 📌 Key Features

- **Employee Management**: Tracks employees using their SSN, name, and salary.
- **Project Management**: Each project has a unique ID, name, duration, and budget.
- **Funding Agencies**: Stores agency details including name and address.
- **Project Assignment**: Tracks which employees are assigned to which projects, along with their respective project managers.
- **Manager Tracking**: Separately maintains the manager assigned to each project.

---

### 🧱 Database Schema Overview

- `Employee`: Contains all employee records.
- `FundingAgency`: Stores funding agency information.
- `Project`: Details about each research project.
- `Project_Manager`: Links each project with its managing employee.
- `Employee_Project`: Junction table mapping employees to projects they work on, including the project manager.

---

![image](https://github.com/user-attachments/assets/17ac5d7a-8aad-4164-8750-c7640f0b3920)
![image](https://github.com/user-attachments/assets/e100f06d-e5f8-466a-8cdd-453077786ead)


### 🧾 SQL Tables Used

```sql
CREATE TABLE Employee (
    SSN INT PRIMARY KEY,
    Emp_Name VARCHAR(50),
    Salary DECIMAL
);

CREATE TABLE FundingAgency (
    Agency_ID INT PRIMARY KEY,
    Name VARCHAR(100),
    Address VARCHAR(255)
);

CREATE TABLE Project (
    Project_ID INT PRIMARY KEY,
    Name VARCHAR(100),
    Duration INT,      -- in months or years
    Budget DECIMAL(12,2)
);

CREATE TABLE Employee_Project (
    SSN INT,
    Project_ID INT,
    Manager_SSN INT,
    PRIMARY KEY (SSN, Project_ID),
    FOREIGN KEY (SSN)        REFERENCES Employee(SSN),
    FOREIGN KEY (Project_ID) REFERENCES Project(Project_ID),
    FOREIGN KEY (Manager_SSN)REFERENCES Employee(SSN)
);

CREATE TABLE Project_Manager (
    Project_ID INT PRIMARY KEY,
    Manager_SSN INT,
    FOREIGN KEY (Project_ID) REFERENCES Project(Project_ID),
    FOREIGN KEY (Manager_SSN)REFERENCES Employee(SSN)
);
