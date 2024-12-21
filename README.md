# Hospital Management System Database Design

## Overview
This project involves designing a Hospital Management System database to efficiently manage information about doctors, patients, appointments, and departments. The database incorporates structured relationships and handles relevant data for the hospital management system.

## Requirements

### Entity Design
The database includes the following tables:

- **Doctors**
  - Fields: `doctor_id`, `name`, `specialization`, `phone`, `department_id`
- **Patients**
  - Fields: `patient_id`, `name`, `age`, `gender`, `phone`
- **Appointments**
  - Fields: `appointment_id`, `date`, `time`, `status`, `doctor_id`, `patient_id`
- **Departments**
  - Fields: `department_id`, `name`, `location`

### Relationships
- Each doctor belongs to a department (many-to-one).
- Each appointment is associated with one doctor and one patient (many-to-one relationships).

## Diagram Submission
An **Entity Relationship Diagram (ERD)** is required to visualize the relationships between tables, primary keys, and foreign keys. The diagram should:
- Show table relationships (e.g., one-to-many, many-to-one).
- Highlight primary and foreign key constraints.

## SQL Example Database Design
Below is the SQL code for creating the database tables:

```sql
-- Create Table Queries
CREATE TABLE `departments` (
    `department_id` INT PRIMARY KEY AUTO_INCREMENT,
    `name` VARCHAR(100) NOT NULL,
    `location` VARCHAR(255),
    `created_at` TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    `updated_at` TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
);

CREATE TABLE `doctors` (
    `doctor_id` INT PRIMARY KEY AUTO_INCREMENT,
    `name` VARCHAR(100) NOT NULL,
    `specialization` VARCHAR(100),
    `phone` VARCHAR(15),
    `department_id` INT,
    `created_at` TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    `updated_at` TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
    FOREIGN KEY (`department_id`) REFERENCES `departments`(`department_id`)
);

CREATE TABLE `patients` (
    `patient_id` INT PRIMARY KEY AUTO_INCREMENT,
    `name` VARCHAR(100) NOT NULL,
    `age` INT,
    `gender` VARCHAR(10),
    `phone` VARCHAR(15),
    `created_at` TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    `updated_at` TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
);

CREATE TABLE `appointments` (
    `appointment_id` INT PRIMARY KEY AUTO_INCREMENT,
    `date` DATE NOT NULL,
    `time` TIME NOT NULL,
    `status` VARCHAR(50),
    `doctor_id` INT,
    `patient_id` INT,
    `created_at` TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    `updated_at` TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
    FOREIGN KEY (`doctor_id`) REFERENCES `doctors`(`doctor_id`),
    FOREIGN KEY (`patient_id`) REFERENCES `patients`(`patient_id`)
);
