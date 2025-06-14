# 🧠 Research Projects Database

This project is a relational database model designed to manage information about **research projects**, their **employees**, **funding agencies**, and **project managers**. The database supports tracking of project details, employee assignments, and the funding structure using a normalized schema derived from an Entity-Relationship (ER) diagram.

## 📁 Project Overview

The system models:
- Employees with their personal and professional details.
- Projects with duration, budget, and funding details.
- Funding agencies that support projects.
- Assignment of employees to projects (many-to-many).
- Assignment of one manager per project. 
![{5518210E-AFA7-4DDC-AF60-1C350BFF9E32}](https://github.com/user-attachments/assets/8396d89a-b3ef-41ce-8791-d00d686c830a)
![{663C52AD-2EC3-4AB1-AF6A-E5B1EAB07258}](https://github.com/user-attachments/assets/b466a03a-31b0-4fd1-900b-1c990e94d428)




## 🔧 Technologies Used
- **MySQL / SQL**
- **ERD Tool** (MySQL Workbench or similar)
- **GitHub** for version control

## 🗃️ Database Schema

### 1. `Employee`
Stores details about employees.

```sql
CREATE TABLE Employee (
    SSN INT PRIMARY KEY,
    Emp_Name VARCHAR(50),
    Salary DECIMAL(10, 0)
);
 
2. FundingAgency
Stores information about agencies funding the projects.
CREATE TABLE FundingAgency (
    Agency_ID INT PRIMARY KEY,
    Name VARCHAR(100),
    Address VARCHAR(255)
);

3. Project
Contains project-specific information and the funding agency reference.
CREATE TABLE Project (
    Project_ID INT PRIMARY KEY,
    Name VARCHAR(100),
    Duration INT,
    Budget DECIMAL(12, 2),
    Agency_ID INT,
    FOREIGN KEY (Agency_ID) REFERENCES FundingAgency(Agency_ID)
);

4. Project_Manager
Maps a single manager to each project.
CREATE TABLE Project_Manager (
    Project_ID INT PRIMARY KEY, 
    Manager_SSN INT,
    FOREIGN KEY (Project_ID) REFERENCES Project(Project_ID),
    FOREIGN KEY (Manager_SSN) REFERENCES Employee(SSN)
);

5. Employee_Project
Maps employees to the projects they are working on.
CREATE TABLE Employee_Project (
    SSN INT,
    Project_ID INT,
    PRIMARY KEY (SSN, Project_ID),
    FOREIGN KEY (SSN) REFERENCES Employee(SSN),
    FOREIGN KEY (Project_ID) REFERENCES Project(Project_ID)
);
📊 Sample Data Insertion 
-- Employees
INSERT INTO Employee (SSN, Emp_Name, Salary) VALUES
(101, 'John Doe', 55000),
(102, 'Jane Smith', 65000),
(103, 'Alice Brown', 72000);

-- Funding Agencies
INSERT INTO FundingAgency (Agency_ID, Name, Address) VALUES
(201, 'Tech Research Fund', '123 Tech Ave, Silicon Valley, CA'),
(202, 'Innovation Grants Inc.', '456 Innovation Dr, New York, NY'),
(203, 'Global Funding Group', '789 Global St, London, UK');

-- Projects
INSERT INTO Project (Project_ID, Name, Duration, Budget, Agency_ID) VALUES
(301, 'AI Research', 12, 200000.00, 201),
(302, 'Cloud Migration', 18, 300000.00, 202),
(303, 'Blockchain Platform', 24, 400000.00, 203);

-- Project Managers
INSERT INTO Project_Manager (Project_ID, Manager_SSN) VALUES
(301, 101),
(302, 102),
(303, 103);

-- Employees working on projects
INSERT INTO Employee_Project (SSN, Project_ID) VALUES
(101, 301),
(102, 302),
(103, 303);

