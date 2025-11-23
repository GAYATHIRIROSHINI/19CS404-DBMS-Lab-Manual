# ER Diagram Workshop – Submission Template

## Objective
To understand and apply ER modeling concepts by creating ER diagrams for real-world applications.

## Purpose
Gain hands-on experience in designing ER diagrams that represent database structure including entities, relationships, attributes, and constraints.

---

# Scenario A: City Fitness Club Management

**Business Context:**  
FlexiFit Gym wants a database to manage its members, trainers, and fitness programs.

**Requirements:**  
- Members register with name, membership type, and start date.  
- Each member can join multiple programs (Yoga, Zumba, Weight Training).  
- Trainers assigned to programs; a program may have multiple trainers.  
- Members may book personal training sessions with trainers.  
- Attendance recorded for each session.  
- Payments tracked for memberships and sessions.

### ER Diagram:
<img width="825" height="654" alt="Screenshot 2025-09-27 090823" src="https://github.com/user-attachments/assets/2fa1a40d-6e43-4ea3-b894-d2218ab859fc" />


### Entities and Attributes
| Entity         | Attributes (PK, FK)                                       | Notes                                    |
| -------------- | --------------------------------------------------------- | ---------------------------------------- |
|   Member       | MemberID (PK), Name, MembershipType, StartDate            | Stores gym member details.               |
|   Program      | ProgramID (PK), ProgramName, ProgramType                  | Examples: Yoga, Zumba, Weight Training.  |
|   Trainer      | TrainerID (PK), Name, Specialization                      | Trainers conduct programs.               |
|   Session      | SessionID (PK), Date, Time, MemberID (FK), TrainerID (FK) | Represents personal training/attendance. |
|   Attendance   | AttendanceID (PK), SessionID (FK), MemberID (FK), Status  | Tracks presence of members in sessions.  |
|   Payment      | PaymentID (PK), Amount, Date, MemberID (FK)               | Payments for memberships and sessions.   |


### Relationships and Constraints
| Relationship                | Cardinality               | Participation      | Notes                                                                             
| --------------------------- | ------------------------- | ------------------ | --------------------------------------------------------------------------------- 
| Member–Program              | M:N                       | Total (Member)     | A member can join many programs, and a program has many members.                  
| Program–Trainer             | M:N                       | Total (Program)    | A program may have multiple trainers, and a trainer can handle multiple programs. 
| Member–Trainer (Session)    | M:N via **Session**       | Partial            | Members can book personal training sessions with trainers.                        
| Member–Session (Attendance) | 1:N (Member → Attendance) | Total (Attendance) | Attendance recorded per session for each member.                                  
| Member–Payment              | 1:N (Member → Payment)    | Total              | A member makes multiple payments.                                                 


### Assumptions
- Each member has one active membership.
A member can join multiple programs; programs can have many members.
Trainers may handle multiple programs; a program may have multiple trainers.
Sessions are uniquely identified and must include at least one trainer and one member.
Attendance is tracked per member per session.
Payments are always linked to members (for membership or sessions).
All entities have unique IDs; M:N relationships use associative entities.

# Scenario B: City Library Event & Book Lending System

**Business Context:**  
The Central Library wants to manage book lending and cultural events.

**Requirements:**  
- Members borrow books, with loan and return dates tracked.  
- Each book has title, author, and category.  
- Library organizes events; members can register.  
- Each event has one or more speakers/authors.  
- Rooms are booked for events and study.  
- Overdue fines apply for late returns.

### ER Diagram:
<img width="848" height="563" alt="Screenshot 2025-09-27 092005" src="https://github.com/user-attachments/assets/af66658a-0d18-4e7f-ba97-454565ccbd05" />

### Entities and Attributes
| Entity  | Attributes (PK, FK)                                           | Notes                                |
| ------- | ------------------------------------------------------------- | ------------------------------------ |
| Member  | MemberID (PK), Name, Contact                                  | Library members.                     |
| Book    | BookID (PK), Title, Author, Category                          | Books available for borrowing.       |
| Loan    | LoanID (PK), LoanDate, ReturnDate, MemberID (FK), BookID (FK) | Tracks borrowed/returned books.      |
| Event   | EventID (PK), EventName, Date, RoomID (FK)                    | Cultural events held in the library. |
| Speaker | SpeakerID (PK), Name, Expertise                               | Speakers/authors in events.          |
| Room    | RoomID (PK), RoomName, Capacity                               | Rooms for events/study use.          |
| Fine    | FineID (PK), Amount, DueDate, MemberID (FK)                   | Overdue charges for late returns.    |


### Relationships and Constraints
| Relationship  | Cardinality | Participation | Notes                                 |
| ------------- | ----------- | ------------- | ------------------------------------- |
| Member–Loan   | 1:N         | Total         | A member can borrow many books.       |
| Book–Loan     | 1:N         | Total         | A book can be borrowed many times.    |
| Member–Event  | M:N         | Partial       | Members register for multiple events. |
| Event–Speaker | M:N         | Total         | An event can have multiple speakers.  |
| Event–Room    | 1:1         | Total         | Each event is booked in one room.     |
| Member–Fine   | 1:N         | Partial       | Members may have fines.               |

### Assumptions
-Each member has a unique ID.
A book can be borrowed by one member at a time.
Events may occur even if no members register.
Each event uses exactly one room, but a room can host multiple events over time.
Fines are only for late book returns. 

---

# Scenario C: Restaurant Table Reservation & Ordering

**Business Context:**  
A popular restaurant wants to manage reservations, orders, and billing.

**Requirements:**  
- Customers can reserve tables or walk in.  
- Each reservation includes date, time, and number of guests.  
- Customers place food orders linked to reservations.  
- Each order contains multiple dishes; dishes belong to categories (starter, main, dessert).  
- Bills generated per reservation, including food and service charges.  
- Waiters assigned to serve reservations.

### ER Diagram:
<img width="877" height="659" alt="Screenshot 2025-09-27 092425" src="https://github.com/user-attachments/assets/5ad73bac-4ddc-434c-b443-e9d1f991ff1a" />

### Entities and Attributes
| Entity      | Attributes (PK, FK)                                                       | Notes                                |
| ----------- | ------------------------------------------------------------------------- | ------------------------------------ |
| Customer    | CustomerID (PK), Name, Contact                                            | Guests of the restaurant.            |
| Reservation | ReservationID (PK), Date, Time, NoOfGuests, CustomerID (FK), TableID (FK) | Table bookings.                      |
| Table       | TableID (PK), Capacity                                                    | Restaurant tables.                   |
| Order       | OrderID (PK), ReservationID (FK), OrderTime                               | Orders linked to reservations.       |
| Dish        | DishID (PK), DishName, Price, Category                                    | Food items (starter, main, dessert). |
| OrderItem   | OrderItemID (PK), OrderID (FK), DishID (FK), Quantity                     | Dishes included in each order.       |
| Bill        | BillID (PK), ReservationID (FK), Amount, ServiceCharge                    | Billing details.                     |
| Waiter      | WaiterID (PK), Name                                                       | Staff serving tables.                |


| Relationship         | Cardinality       | Participation | Notes                                       |
| -------------------- | ----------------- | ------------- | ------------------------------------------- |
| Customer–Reservation | 1:N               | Total         | A customer can make many reservations.      |
| Reservation–Table    | 1:1               | Total         | A reservation is linked to one table.       |
| Reservation–Order    | 1:N               | Partial       | One reservation can have multiple orders.   |
| Order–Dish           | M:N via OrderItem | Total         | An order contains multiple dishes.          |
| Reservation–Bill     | 1:1               | Total         | Each reservation has one bill.              |
| Reservation–Waiter   | 1:N               | Partial       | One waiter may serve multiple reservations. |

### Assumptions
- A table can be reserved by one customer at a time slot.
Walk-in customers are entered as reservations at booking time.
Each order belongs to exactly one reservation.
Bills are always generated per reservation (not per dish).
One waiter may serve many reservations, but each reservation is served by only one waiter.
- 
- 

---

## Instructions for Students

1. Complete **all three scenarios** (A, B, C).  
2. Identify entities, relationships, and attributes for each.  
3. Draw ER diagrams using **draw.io / diagrams.net** or hand-drawn & scanned.  
4. Fill in all tables and assumptions for each scenario.  
5. Export the completed Markdown (with diagrams) as **a single PDF**
