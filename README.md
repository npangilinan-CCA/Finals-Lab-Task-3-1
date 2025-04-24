# [Finals Lab Task 3-1 - Using MYSQL Clause](https://github.com/user-attachments/files/19625279/pangilinan_FinalsLabTask1.docx)
This portfolio is a demonstration of applying MySQL clauses to solve common database query tasks. It showcases the use of SELECT, WHERE, GROUP BY, SUM, and ORDER BY statements to retrieve, group, filter, and sort data from a table of online courses. Each query addresses a specific scenario, such as identifying under-enrolled or fully enrolled courses, calculating total student enrollments by category and overall, and ordering data based on enrollment numbers.

## Step by Step Process
### Task 1: Retrieve all courses where students enrolled is less than the enrollment_limit
- Use select and from statement to choose the courses table
- Use where statement to choose the following values from courses table (students_enrolled and enrollment limit) and adding the '>' conditional statement to complete the process the process
  
### Task 2: Group courses by category and calculate the total number of students enrolled for each category
- Define department_id as a unique integer, auto-increment, and primary key.
- Define department_name as a VARCHAR (up to 255 characters), and make it not null.
  
### Task 3: Retrieve the courses that are fully enrolled
- Define employee_id as an integer, which will be a foreign key referencing employee_id in the employees table.
- Define department_id as an integer, which will be a foreign key referencing department_id in the departments table.
- Set a composite primary key on the combination of employee_id and department_id.
  
### Task 4: Create the employee projects table
- Define employee_id as an integer, which will be a foreign key referencing employee_id in the employees table.
- Define project_name as a VARCHAR (up to 255 characters), and make it not null.
  
### Task 5: Create the managers table
- Define manager_id as a unique integer, auto-increment, and primary key.
- Define employee_id as an integer, which will be a foreign key referencing employee_id in the employees table.

## Query Statements and Table Structures
### Task 1
![Image](https://github.com/user-attachments/assets/54f2649a-21ef-4599-a55e-3a9a20f662d3)

### Task 2
![Image](https://github.com/user-attachments/assets/d9495404-9ea9-4c1d-a755-fe8a8c6b50e7)

### Task 3
![Image](https://github.com/user-attachments/assets/d921b6e8-ff68-42ac-9dbd-55fb8c29b5e5)

### Task 4
![Image](https://github.com/user-attachments/assets/b7cadc5d-3099-415e-be3a-44e0e96fa749)

### Task 5
![Image](https://github.com/user-attachments/assets/d0d45768-960a-43ea-86cf-657361b3dcc6)


