# Database Design

This document describes the core database schema for the Udaan NGO Management Platform.
The design focuses on role lifecycle tracking, academic year transitions, and NGO operations.
## users

Stores permanent user information. A user may have multiple roles across different academic years.

Fields:
- id (UUID, Primary Key)
- name
- email (unique)
- password
- joined_at
## roles

Stores predefined roles in the system.

Fields:
- id (Primary Key)
- name (VOLUNTEER, COUNCIL, ALUMNI, SUPER_ADMIN)
## academic_years

Controls role assignment boundaries.

Fields:
- id (Primary Key)
- year_label (e.g., 2024-25)
- is_active (boolean)
- start_date
- end_date
## user_roles

Tracks role assignments for users across academic years.

Fields:
- id (Primary Key)
- user_id (Foreign Key → users)
- role_id (Foreign Key → roles)
- academic_year_id (Foreign Key → academic_years)
- status (ACTIVE, INACTIVE, LEFT, COMPLETED)
- start_date
- end_date
- left_reason (optional)
## students

Stores information about students attending classes.

Fields:
- id (Primary Key)
- name
- age
- village
- enrolled_year_id (FK → academic_years)
## classes

Represents class groups handled by volunteers.

Fields:
- id (Primary Key)
- class_name (e.g., Class 6, Class 7)
- academic_year_id (FK → academic_years)
## timetables

Defines class schedules.

Fields:
- id (Primary Key)
- class_id (FK → classes)
- volunteer_role_id (FK → user_roles)
- day_of_week
- start_time
- end_time
## attendance

Tracks daily attendance for students.

Fields:
- id (Primary Key)
- student_id (FK → students)
- class_id (FK → classes)
- date
- status (PRESENT / ABSENT)
- marked_by_role_id (FK → user_roles)
## events

Stores NGO events and activities.

Fields:
- id (Primary Key)
- title
- description
- event_date
- created_by_role_id (FK → user_roles)
## volunteer_applications

Stores applications from outsiders.

Fields:
- id (Primary Key)
- name
- email
- message
- applied_at
- status (PENDING / APPROVED / REJECTED)
## Key Relationships

- A user can have multiple roles across academic years
- Each role belongs to exactly one academic year
- Attendance and timetables are linked to roles, not users
- Alumni is a derived role based on role history
