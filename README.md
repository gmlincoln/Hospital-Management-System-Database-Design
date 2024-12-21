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

### ER Diagram
Below is an example of the ER diagram for the system:

![ER Diagram](./path/to/your/ER-diagram-image.jpg)

## SQL Database Queries
Below is the SQL code for creating the database tables with the updated foreign key constraints:

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
    ON DELETE RESTRICT ON UPDATE CASCADE
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
    FOREIGN KEY (`doctor_id`) REFERENCES `doctors`(`doctor_id`)
    ON DELETE RESTRICT ON UPDATE CASCADE,
    FOREIGN KEY (`patient_id`) REFERENCES `patients`(`patient_id`)
    ON DELETE RESTRICT ON UPDATE CASCADE
);

-- Insert Dummy Data


-- Departments
INSERT INTO `departments` (`name`, `location`) VALUES 
('Cardiology', 'First Floor'),
('Neurology', 'Second Floor'),
('Pediatrics', 'Third Floor'),
('Orthopedics', 'Fourth Floor'),
('General Medicine', 'Ground Floor');

-- Doctors
INSERT INTO `doctors` (`name`, `specialization`, `phone`, `department_id`) VALUES 
('Dr. Smith', 'Cardiologist', '1234567890', 1),
('Dr. Jane', 'Neurologist', '0987654321', 2),
('Dr. Miller', 'Pediatrician', '5678901234', 3),
('Dr. Johnson', 'Orthopedic', '2345678901', 4),
('Dr. Brown', 'General Practitioner', '3456789012', 5);

-- Patients
INSERT INTO `patients` (`name`, `age`, `gender`, `phone`) VALUES 
('John Doe', 45, 'male', '1112223333'),
('Jane Roe', 29, 'female', '4445556666'),
('Sam Smith', 12, 'male', '7778889999'),
('Alice White', 34, 'female', '1233211234'),
('Bob Black', 60, 'male', '9876543210');

-- Appointments
INSERT INTO `appointments` (`date`, `time`, `status`, `doctor_id`, `patient_id`) VALUES 
('2024-12-22', '10:00:00', 'Scheduled', 1, 1),
('2024-12-22', '11:00:00', 'Scheduled', 2, 2),
('2024-12-22', '12:00:00', 'Completed', 3, 3),
('2024-12-23', '10:30:00', 'Scheduled', 4, 4),
('2024-12-23', '11:30:00', 'Cancelled', 5, 5);

