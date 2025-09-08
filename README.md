# AirBnB Clone Project

## 📌 Overview
This project is a simplified clone of the AirBnB platform. The goal is to practice full-stack development skills, starting from backend fundamentals to building a user-friendly frontend.

## 🎯 Project Goals
- Understand and implement object-oriented programming concepts.  
- Learn how to design and manage RESTful APIs.  
- Practice working with databases (SQL & ORM).  
- Build and style dynamic front-end pages.  
- Gain experience collaborating with peers on large projects.  

## 🛠 Tech Stack
- **Backend:** Python (Flask / Django), REST API  
- **Database:** MySQL / SQLite  
- **Frontend:** HTML, CSS, JavaScript  
- **Version Control:** Git & GitHub  

## 🚀 Progress
This repository will track the development of the AirBnB clone step by step.

## Team Roles

### Backend Developer
Responsible for building and maintaining the server-side logic of the application. Implements APIs, integrates with the database, and ensures the system is scalable, efficient, and secure.

### Frontend Developer
Focuses on creating the client-side of the application. Translates UI/UX designs into functional, responsive web pages using HTML, CSS, and JavaScript frameworks. Ensures a smooth and intuitive user experience.

### Database Administrator (DBA)
Designs, manages, and maintains the project’s database. Ensures data integrity, implements backup and recovery strategies, optimizes queries, and manages access permissions.

### Project Manager
Coordinates the overall progress of the project. Sets milestones, assigns tasks, monitors deadlines, and ensures smooth communication between all team members and stakeholders.

### Quality Assurance (QA) Engineer
Tests the system to identify bugs, inconsistencies, and performance issues. Ensures that the application meets requirements and maintains high standards before deployment.

### DevOps Engineer
Manages deployment pipelines, server configuration, and cloud infrastructure. Automates processes, monitors application performance, and ensures system reliability in production.

### UX/UI Designer
Designs the application’s look and feel. Creates wireframes, prototypes, and high-fidelity designs to ensure a user-friendly interface that meets both aesthetic and functional requirements.
  
## Technology Stack

### Django
A high-level Python web framework that simplifies building robust and scalable web applications.  
In this project, Django will be used to develop the backend logic, handle HTTP requests, manage authentication, and connect with the database.

### PostgreSQL
An advanced open-source relational database system.  
It will store user data, booking information, property details, and all persistent data for the AirBnB clone.

### GraphQL
A query language for APIs and runtime for executing those queries.  
It allows clients to request exactly the data they need, improving efficiency compared to REST.  
In this project, GraphQL will make data retrieval between frontend and backend more flexible and efficient.

### HTML, CSS, and JavaScript
The core frontend technologies.  
- **HTML** structures the web pages.  
- **CSS** styles and ensures responsiveness.  
- **JavaScript** adds interactivity and dynamic behavior for a smooth user experience.

### Bootstrap (optional if included in overview)
A frontend toolkit for building responsive and mobile-first web pages.  
It helps speed up UI development with pre-designed components.

### Docker (if part of overview)
A containerization tool that ensures the application runs consistently across different environments.  
It simplifies deployment and environment management.

### Git & GitHub
- **Git**: Version control system to track changes in the codebase.  
- **GitHub**: Hosting platform for collaboration, pull requests, and project management.

## Database Design

### Key Entities & Fields

#### 1) Users
- **id** (PK)
- **name**
- **email** (unique)
- **password_hash**
- **role** (guest | host | admin)
- **created_at**

#### 2) Properties
- **id** (PK)
- **host_id** (FK → Users.id)
- **title**
- **description**
- **address**
- **city**, **country**
- **price_per_night**
- **created_at**

#### 3) Bookings
- **id** (PK)
- **property_id** (FK → Properties.id)
- **guest_id** (FK → Users.id)
- **check_in_date**
- **check_out_date**
- **total_price**
- **status** (pending | confirmed | canceled)
- **created_at**

#### 4) Reviews
- **id** (PK)
- **property_id** (FK → Properties.id)
- **author_id** (FK → Users.id)
- **rating** (1–5)
- **comment**
- **created_at**

#### 5) Payments
- **id** (PK)
- **booking_id** (FK → Bookings.id)
- **amount**
- **currency**
- **status** (initiated | succeeded | failed | refunded)
- **provider_ref** (transaction/reference id)
- **created_at**

> *(PK = Primary Key, FK = Foreign Key)*

### Relationships

- **User (host)** 1 — *N* **Properties**  
  A host can list many properties; each property belongs to one host.

- **User (guest)** 1 — *N* **Bookings**  
  A guest can make many bookings; each booking is made by one guest.

- **Property** 1 — *N* **Bookings**  
  A property can have many bookings; each booking belongs to one property.

- **Property** 1 — *N* **Reviews**  
  A property can have many reviews; each review is authored by one user.

- **User** 1 — *N* **Reviews**  
  A user can write many reviews.

- **Booking** 1 — 1 **Payment** *(typical case)*  
  Each booking has one payment record (or one latest active payment).

### Quick ER Diagram (text)

Users (id) ──< Properties (host_id)  
Users (id) ──< Bookings (guest_id)  
Properties (id) ──< Bookings (property_id)  
Properties (id) ──< Reviews (property_id)  
Users (id) ──< Reviews (author_id)  
Bookings (id) ──  Payments (booking_id)

## Feature Breakdown

### 1. User Management
Handles user registration, login, and authentication. Users can sign up as guests or hosts, manage their profiles, and securely log in and out of the system.

### 2. Property Management
Allows hosts to list properties with details such as title, description, address, pricing, and availability. Hosts can also edit or remove their listings at any time.

### 3. Booking System
Enables guests to search for properties, check availability, and make reservations. This system ensures that booking dates are validated and prevents double bookings.

### 4. Review System
Guests can leave reviews and ratings for properties they have stayed in. This builds trust between users and provides feedback for hosts to improve their services.

### 5. Payment Integration
Processes secure payments for bookings, including tracking payment status. Ensures that guests can pay safely and hosts receive their funds efficiently.

### 6. Search and Filtering
Provides powerful search options with filters such as location, price range, property type, and amenities. Helps users quickly find the most suitable property.

### 7. Admin Dashboard (optional/advanced)
Provides administrators with tools to manage users, properties, and bookings. Ensures smooth operation of the platform by monitoring system activity.
