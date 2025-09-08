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

## API Security

Securing the backend API is critical for protecting user data, ensuring trustworthy payments, and maintaining platform integrity. Below are the key measures we will implement and why they matter for this project.

### 1) Authentication (Who are you?)
- **Approach:** Token-based auth (e.g., JWT) or session-based; password hashing with Argon2/bcrypt; optional OAuth2 for social login.
- **Why it matters:** Prevents unauthorized access to user accounts, protects personal information, and ensures only verified users can create bookings or manage listings.

### 2) Authorization (What are you allowed to do?)
- **Approach:** Role- and resource-based access control (RBAC): admin, host, guest; enforce ownership checks (e.g., a host may only edit their own property).
- **Why it matters:** Protects critical actions and data. A user should not be able to modify another user’s booking or a property they don’t own.

### 3) Transport Security (HTTPS/TLS)
- **Approach:** Enforce HTTPS everywhere (redirect HTTP → HTTPS), HSTS headers in production.
- **Why it matters:** Encrypts data in transit (logins, payment tokens, personal info), preventing credential theft and man-in-the-middle attacks.

### 4) Input Validation & Sanitization
- **Approach:** Validate request bodies, query strings, and headers; server-side schema validation (e.g., pydantic/DRF serializers); sanitize strings to prevent XSS/SQLi.
- **Why it matters:** Blocks injection attacks (SQLi, XSS) and malformed requests that could crash the API or leak data.

### 5) Rate Limiting & Abuse Protection
- **Approach:** Global and per-route rate limits (e.g., `/auth/login` stricter), bot detection, IP throttling, and account lockout for brute-force attempts.
- **Why it matters:** Prevents credential stuffing, brute-force login attempts, and denial-of-service from abusive clients.

### 6) CORS & CSRF Protections
- **Approach:** Restrictive CORS (allow-list known origins), SameSite cookies (if session-based), CSRF tokens for state-changing requests from browsers.
- **Why it matters:** Stops cross-origin attacks and protects authenticated browser sessions from unwanted actions.

### 7) Secrets & Config Management
- **Approach:** Store secrets (DB creds, API keys, JWT secrets) in environment variables or a secret manager (never in Git); rotate keys; principle of least privilege in cloud/DB.
- **Why it matters:** Leaked secrets compromise the entire system—DB dumps, token forgery, payment fraud.

### 8) Data Protection (At Rest & Minimization)
- **Approach:** Encrypt sensitive fields at rest where appropriate, store only what we need (minimization), strict retention policies, GDPR-friendly practices.
- **Why it matters:** Limits blast radius if a breach occurs and respects users’ privacy.

### 9) Secure Payments
- **Approach:** Use a PCI-compliant provider; never store raw card data; verify webhook signatures; idempotent payment endpoints.
- **Why it matters:** Reduces legal exposure and protects users’ financial data.

### 10) Logging, Monitoring & Auditing
- **Approach:** Centralized structured logs (no PII), audit trails for critical actions (login, booking, payment, property changes), anomaly alerts.
- **Why it matters:** Enables incident response, fraud detection, and compliance evidence.

### 11) Dependency & Platform Hardening
- **Approach:** Pin and scan dependencies (SCA), regular security updates, container image scanning, minimal base images, security headers (CSP, X-Frame-Options, X-Content-Type-Options).
- **Why it matters:** Third-party packages and defaults are common attack vectors; hardening reduces risk.

### 12) Error Handling & Safe Defaults
- **Approach:** Standardized error responses without stack traces; safe timeouts; deny-by-default access; robust 4xx/5xx handling.
- **Why it matters:** Prevents information leakage and avoids undefined behavior.

---

### Security Focus by Area

- **User Accounts:** Strong auth, password hashing, brute-force protection, secure sessions/JWTs → prevents account takeover.
- **Properties & Reviews:** Authorization and ownership checks → prevents unauthorized edits and data tampering.
- **Bookings:** Validation of dates and status transitions, idempotent operations → prevents logic abuse and double bookings.
- **Payments:** Provider-based flows, signed webhooks, no raw card storage → protects financial data and prevents charge manipulation.

## CI/CD Pipeline

Continuous Integration (CI) and Continuous Deployment/Delivery (CD) are key practices in modern software development.  

- **Continuous Integration (CI):** Automatically builds, tests, and validates code every time a change is pushed to the repository. This ensures that issues are caught early and the codebase remains stable.  
- **Continuous Deployment/Delivery (CD):** Automatically deploys tested changes to staging or production environments. This reduces manual work, speeds up release cycles, and makes deployments more reliable.

### Why CI/CD is Important for this Project
- **Reliability:** Ensures that new features and bug fixes don’t break existing functionality.  
- **Speed:** Automates repetitive tasks, reducing development bottlenecks.  
- **Quality:** Enforces testing, code linting, and security checks before changes are merged.  
- **Collaboration:** Makes it easier for multiple developers to contribute safely.  

### Tools We Could Use
- **GitHub Actions:** For automating workflows directly within GitHub (tests, builds, deployments).  
- **Docker:** For containerizing the application, ensuring consistency across development, testing, and production environments.  
- **Heroku / AWS / Azure:** For hosting and deployment.  
- **PostgreSQL migrations (via Django):** Ensuring database changes are applied consistently across environments.  

The CI/CD pipeline will help us move faster while maintaining high quality and security for the AirBnB Clone project.
