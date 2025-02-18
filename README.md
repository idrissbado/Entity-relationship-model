# Gym Management System - Entity Relationship Model (ERD)

This README provides an **Entity Relationship Model (ERM)** for a gym management system based on the scenario described. The goal is to replace the outdated card-based system with a modern database solution to manage gymnasiums, members, sessions, and coaches efficiently.

---

## Problem Statement

A large gym chain is facing issues with manual registration and session management. The owner wants a digital solution to manage:

1. **Gymnasiums**: Each gym has a name, address, and phone number.
2. **Members**: Members register at a gym and provide personal details (unique ID, last name, first name, address, date of birth, gender).
3. **Sessions**: Each session has a type of sport, schedule, and a maximum capacity of 20 members. Sessions are led by up to two coaches.
4. **Coaches**: Coaches have personal details (last name, first name, age, specialty) and can lead multiple sessions.

---

## Entity Relationship Model (ERD)

Below is the **Entity Relationship Model (ERD)** for the gym management system:

### Entities and Attributes

1. **Gymnasium**
   - GymID (Primary Key)
   - Name
   - Address
   - PhoneNumber

2. **Member**
   - MemberID (Primary Key)
   - LastName
   - FirstName
   - Address
   - DateOfBirth
   - Gender
   - GymID (Foreign Key referencing Gymnasium)

3. **Session**
   - SessionID (Primary Key)
   - SportType
   - Schedule
   - MaxCapacity (default: 20)
   - GymID (Foreign Key referencing Gymnasium)

4. **Coach**
   - CoachID (Primary Key)
   - LastName
   - FirstName
   - Age
   - Specialty

5. **SessionCoach** (Many-to-Many Relationship between Session and Coach)
   - SessionID (Foreign Key referencing Session)
   - CoachID (Foreign Key referencing Coach)

6. **MemberSession** (Many-to-Many Relationship between Member and Session)
   - MemberID (Foreign Key referencing Member)
   - SessionID (Foreign Key referencing Session)

---

### Relationships

1. **Gymnasium - Member**: One-to-Many
   - One gym can have many members.
   - Each member belongs to one gym.

2. **Gymnasium - Session**: One-to-Many
   - One gym can host many sessions.
   - Each session belongs to one gym.

3. **Session - Coach**: Many-to-Many
   - One session can have up to two coaches.
   - One coach can lead multiple sessions.

4. **Member - Session**: Many-to-Many
   - One member can register for multiple sessions.
   - One session can have multiple members (up to 20).

---

### ERD Diagram (Using Mermaid)

Below is the **Entity Relationship Diagram (ERD)** represented using Mermaid syntax:

```mermaid
erDiagram
    GYMNASIUM ||--o{ MEMBER : "has"
    GYMNASIUM ||--o{ SESSION : "hosts"
    SESSION ||--o{ MEMBER : "accommodates"
    SESSION ||--o{ COACH : "led by"
    COACH ||--o{ SESSION : "leads"

    GYMNASIUM {
        int GymID PK
        string Name
        string Address
        string PhoneNumber
    }

    MEMBER {
        int MemberID PK
        string LastName
        string FirstName
        string Address
        date DateOfBirth
        char Gender
        int GymID FK
    }

    SESSION {
        int SessionID PK
        string SportType
        datetime Schedule
        int MaxCapacity
        int GymID FK
    }

    COACH {
        int CoachID PK
        string LastName
        string FirstName
        int Age
        string Specialty
    }

    SESSION_COACH {
        int SessionID FK
        int CoachID FK
    }

    MEMBER_SESSION {
        int MemberID FK
        int SessionID FK
    }
