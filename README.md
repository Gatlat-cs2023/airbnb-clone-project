## 🏠 Airbnb Clone Project

The Airbnb Clone Project is a comprehensive, real-world application designed to simulate the development of a robust booking platform like Airbnb. It involves a deep dive into full-stack development, focusing on backend systems, database design, API development, and application security. This project enables learners to understand complex architectures, workflows, and collaborative team dynamics while building a scalable web application.

---

## 👥 Team Roles

This section outlines the key roles within the project team and their responsibilities, inspired by typical agile software development practices and references like the ITRexGroup blog.

1. **Backend Developer**
   Responsible for developing and maintaining the server-side logic of the application. Handles API creation, database integration, authentication, and overall system performance.

2. **Frontend Developer**
   Builds the user interface and ensures the application is responsive, accessible, and user-friendly. Works closely with designers to implement UI/UX designs using modern frameworks.

3. **Database Administrator (DBA)**
   Manages the database systems, including schema design, query optimization, data backups, and security. Ensures data integrity and availability.

4. **DevOps Engineer**
   Builds and manages the CI/CD pipeline, automates deployments, monitors infrastructure, and ensures system scalability and reliability using tools like Docker, Kubernetes, and GitHub Actions.

5. **UI/UX Designer**
   Designs intuitive interfaces and improves user experience by creating wireframes, prototypes, and visual designs. Collaborates with developers to bring designs to life.

6. **Project Manager**
   Coordinates the project’s timeline, team communication, task assignments, and ensures the project stays aligned with business goals. Acts as a bridge between stakeholders and the development team.

7. **QA Engineer**
   Responsible for ensuring the quality of the product through automated and manual testing. Identifies bugs, verifies fixes, and maintains testing documentation.

---

## 🧰 Technology Stack

* **Django**: A high-level Python web framework that simplifies building RESTful APIs and web applications.
* **PostgreSQL**: A powerful open-source relational database used to store and manage data.
* **GraphQL**: A query language for APIs that enables clients to request exactly the data they need.

---

### 📦 Database Design

#### 🔑 Entities and Attributes

**User**  
- `user_id`: Primary Key, UUID, Indexed  
- `first_name`: VARCHAR, NOT NULL  
- `last_name`: VARCHAR, NOT NULL  
- `email`: VARCHAR, UNIQUE, NOT NULL  
- `password_hash`: VARCHAR, NOT NULL  
- `phone_number`: VARCHAR, NULL  
- `role`: ENUM (guest, host, admin), NOT NULL  
- `created_at`: TIMESTAMP, DEFAULT CURRENT_TIMESTAMP  

**Property**  
- `property_id`: Primary Key, UUID, Indexed  
- `host_id`: Foreign Key, references User(user_id)  
- `name`: VARCHAR, NOT NULL  
- `description`: TEXT, NOT NULL  
- `location`: VARCHAR, NOT NULL  
- `pricepernight`: DECIMAL, NOT NULL  
- `created_at`: TIMESTAMP, DEFAULT CURRENT_TIMESTAMP  
- `updated_at`: TIMESTAMP, ON UPDATE CURRENT_TIMESTAMP  

**Booking**  
- `booking_id`: Primary Key, UUID, Indexed  
- `property_id`: Foreign Key, references Property(property_id)  
- `user_id`: Foreign Key, references User(user_id)  
- `start_date`: DATE, NOT NULL  
- `end_date`: DATE, NOT NULL  
- `total_price`: DECIMAL, NOT NULL  
- `status`: ENUM (pending, confirmed, canceled), NOT NULL  
- `created_at`: TIMESTAMP, DEFAULT CURRENT_TIMESTAMP  

**Payment**  
- `payment_id`: Primary Key, UUID, Indexed  
- `booking_id`: Foreign Key, references Booking(booking_id)  
- `amount`: DECIMAL, NOT NULL  
- `payment_date`: TIMESTAMP, DEFAULT CURRENT_TIMESTAMP  
- `payment_method`: ENUM (credit_card, paypal, stripe), NOT NULL  

**Review**  
- `review_id`: Primary Key, UUID, Indexed  
- `property_id`: Foreign Key, references Property(property_id)  
- `user_id`: Foreign Key, references User(user_id)  
- `rating`: INTEGER, CHECK: rating >= 1 AND rating <= 5, NOT NULL  
- `comment`: TEXT, NOT NULL  
- `created_at`: TIMESTAMP, DEFAULT CURRENT_TIMESTAMP  

**Message**  
- `message_id`: Primary Key, UUID, Indexed  
- `sender_id`: Foreign Key, references User(user_id)  
- `recipient_id`: Foreign Key, references User(user_id)  
- `message_body`: TEXT, NOT NULL  
- `sent_at`: TIMESTAMP, DEFAULT CURRENT_TIMESTAMP  

---

#### 🔐 Constraints

**User Table**  
- Unique constraint on email  
- Non-null constraints on required fields  

**Property Table**  
- Foreign key constraint on host_id  
- Non-null constraints on essential attributes  

**Booking Table**  
- Foreign key constraints on property_id and user_id  
- `status` must be one of `pending`, `confirmed`, or `canceled`  

**Payment Table**  
- Foreign key constraint on booking_id, ensuring payment is linked to valid bookings  

**Review Table**  
- Constraints on rating values (1–5)  
- Foreign key constraints on property_id and user_id  

**Message Table**  
- Foreign key constraints on sender_id and recipient_id  

---

#### ⚙️ Indexing

- Primary Keys: Indexed automatically  
- Additional Indexes:  
  - `email` in the User table  
  - `property_id` in the Property and Booking tables  
  - `booking_id` in the Booking and Payment tables  

---

## 🚀 Feature Breakdown 

1. **User Management**
   - Based on the `User` table.
   - Supports user registration, login, and profile management.
   - Role-based access via the `role` field (guest, host, admin).
   - Enforces unique email addresses and stores hashed passwords.

2. **Property Management**
   - Backed by the `Property` table linked to a `host_id` (User).
   - Hosts can create, update, or delete listings with `name`, `description`, `location`, `pricepernight`, and timestamps.
   - Foreign key constraints maintain data integrity.

3. **Booking System**
   - Powered by the `Booking` table linking `user_id` and `property_id`.
   - Guests can reserve properties for specific dates (`start_date`, `end_date`) and track booking `status` (pending, confirmed, canceled).
   - Calculates and stores `total_price`.

4. **Review & Rating System**
   - Based on the `Review` table.
   - Guests can leave `rating` (1–5) and `comment` for each property they've stayed in.
   - Linked via foreign keys to both `User` and `Property` tables.

5. **Payment Integration**
   - Uses the `Payment` table, which links to `Booking` via `booking_id`.
   - Stores `amount`, `payment_method` (credit_card, paypal, stripe), and `payment_date`.
   - Ensures every payment is associated with a valid booking.

6. **Messaging System**
   - Implemented with the `Message` table.
   - Allows users to send messages (`message_body`) to each other.
   - Stores `sender_id`, `recipient_id`, and `sent_at`.

7. **Admin Dashboard (Optional)**
   - Leverages user `role = admin` to grant elevated permissions.
   - Admins can oversee platform usage, manage listings or users, and enforce platform policies.

---

## 🔐 API Security

Security is a top priority in this project to protect sensitive user data, ensure trust, and maintain system integrity. The following key measures are implemented:

1. **Authentication**
   Token-based authentication (e.g., JWT) is used to verify the identity of users accessing the API. This ensures that only registered and logged-in users can perform certain actions.

2. **Authorization**
   Role-based access control restricts access to specific endpoints. For example, only hosts can manage property listings, and only authenticated users can make bookings or post reviews.

3. **Rate Limiting**
   Prevents abuse of the API through excessive requests (e.g., brute force attacks). This improves application performance and reliability.

4. **Input Validation & Sanitization**
   All user inputs are validated and sanitized to prevent injection attacks (e.g., SQL injection, XSS), maintaining data integrity and system protection.

5. **Secure Payment Handling**
   Payments are processed through trusted third-party services (e.g., Stripe or PayPal) with secure protocols, protecting financial data and ensuring compliance with PCI-DSS.

---

## ⚙️ CI/CD Pipeline

### What is CI/CD?

CI/CD stands for **Continuous Integration** and **Continuous Deployment/Delivery**. It automates testing, building, and deploying code. CI ensures changes are tested automatically; CD handles deploying those changes to production or staging environments.

### Why It’s Important

CI/CD pipelines increase development speed and code quality by catching issues early through automated testing. They ensure smooth deployments, reduce production bugs, and promote collaboration by maintaining a consistent workflow.

### Tools Used

* **GitHub Actions**: Automates workflows like running tests, linting code, and deploying the application.
* **Docker**: Ensures consistent environments across development, testing, and production using containerization.
* **Heroku / AWS / Netlify** *(optional)*: Hosting platforms for continuous deployment of backend or frontend services.
