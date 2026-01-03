# Role Lifecycle Design

This document explains how user roles are managed across academic years
for the Udaan NGO Management Platform.
| Role        | Description                                |
| ----------- | ------------------------------------------ |
| VOLUNTEER   | Teaches students and manages classes       |
| COUNCIL     | Manages volunteers, timetables, and events |
| ALUMNI      | Past members with view-only access         |
| SUPER_ADMIN | System-level administrator (rare)          |
## Academic Year Concept

All roles in the system are associated with an academic year.
Only one academic year can be active at a time.

Examples:
- 2023–24
- 2024–25
## Role Status States

Each role assigned to a user follows a lifecycle:

| Status | Meaning |
|------|-------|
| ACTIVE | User is currently working |
| INACTIVE | Temporarily paused |
| LEFT | Left mid-year |
| COMPLETED | Completed full academic year |
## Role Lifecycle Scenarios

### 1. User Joins Mid-Year
- A new role entry is created
- Status = ACTIVE
- Start date = joining date

### 2. User Leaves Mid-Year
- Role status updated to LEFT
- End date recorded
- Access revoked immediately

### 3. User Rejoins in Same Year
- A new role entry is created
- Previous role remains unchanged
- History preserved

### 4. User Continues Full Year
- Status changed to COMPLETED at year end

### 5. User Becomes Alumni
- User has no ACTIVE role in current year
- Alumni access is granted automatically
## Role Lifecycle Scenarios

### 1. User Joins Mid-Year
- A new role entry is created
- Status = ACTIVE
- Start date = joining date

### 2. User Leaves Mid-Year
- Role status updated to LEFT
- End date recorded
- Access revoked immediately

### 3. User Rejoins in Same Year
- A new role entry is created
- Previous role remains unchanged
- History preserved

### 4. User Continues Full Year
- Status changed to COMPLETED at year end

### 5. User Becomes Alumni
- User has no ACTIVE role in current year
- Alumni access is granted automatically
## Access Resolution Logic

When a user logs in:

1. System identifies the active academic year
2. Fetches the user's role for that year
3. Grants access only if role status is ACTIVE

If no ACTIVE role is found:
- User is treated as Alumni or Guest

## Dashboard Strategy

The platform uses a single dashboard application with role-based rendering.

- Same routes
- Different UI components based on role
- Centralized access control
