# [Finals Lab Task 3-1 - Using MYSQL Clause](https://github.com/user-attachments/files/19895050/pangilinan_FinalsLabTask3-1.docx)
This portfolio is a demonstration of applying MySQL clauses to solve common database query tasks. It showcases the use of SELECT, WHERE, GROUP BY, SUM, and ORDER BY statements to retrieve, group, filter, and sort data from a table of online courses. Each query addresses a specific scenario, such as identifying under-enrolled or fully enrolled courses, calculating total student enrollments by category and overall, and ordering data based on enrollment numbers.

## Step by Step Process
### 1. Create a database named online course_DB

### 2. Copy and paste the initial query provided in the google classroom

### 3. Retrieve all courses where students enrolled is less than the enrollment_limit
- Use select and from statement to choose the courses table
- Use where statement to choose the following values from courses table (students_enrolled and enrollment limit) and adding the '>' conditional statement to complete the process
  
### 4. Group courses by category and calculate the total number of students enrolled for each category
- Use the select statement to choose the category from the courses table
- Use the sum statement to calculate the sum of  of students_enrolled followed by the as statement to give it an alias as total_students_enrolled
- Use the group by statement to group the sum of students_enrolled within each group by category
  
### 5. Retrieve the courses that are fully enrolled
- Use the select statement followed by the from statement to choose the courses table
- Use the where statement followed by inserting the values students_enrolled and enrollment_limit with the conditional statement '=' in between to filter courses that does not follow the condition
  
### 6. Calculate the total number of students enrolled across all courses
- Use the select statement to choose the students enrolled with the sum statement to calculate the sum
- Use the as statement on student_enrolled to give it an alias as total_students_all_courses
- Use the from statement to choose courses table
  
### 7. Sort courses by students_enrolled in ascending order
- Use the select statement followed by from statement to choose the courses table
- Use the order by statement followed by the asc statement to arrange the students_enrolled in ascending order

## Table Structures and Query Statements
### Task 1
![QT1](https://github.com/user-attachments/assets/f74da6c0-b283-4a7c-8f8b-50821e18c79d)

### Task 2
![QT2](https://github.com/user-attachments/assets/78cd984f-0b47-4646-8ff8-2cdec6d6c6e0)

### Task 3
![QT3](https://github.com/user-attachments/assets/584bf376-b472-46bb-939a-dd0c33e27beb)

### Task 4
![QT4](https://github.com/user-attachments/assets/47f7b5f5-023b-4ce0-87a0-8596b55be6ed)

### Task 5
![QT5](https://github.com/user-attachments/assets/acb78e5b-903d-4490-a2df-33dc89bfde62)




