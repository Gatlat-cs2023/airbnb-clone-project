The Airbnb Clone Project is a comprehensive, real-world application designed to simulate the development of a robust booking platform like Airbnb. It involves a deep dive into full-stack development, focusing on backend systems, database design, API development, and application security. This project enables learners to understand complex architectures, workflows, and collaborative team dynamics while building a scalable web application.

Technology Stack
- Django: A high-level Python web framework that simplifies building RESTful APIs and web applications.
- PostgreSQL: A powerful open-source relational database used to store and manage data.
- GraphQL: A query language for APIs that enables clients to request exactly the data they need.

Database Design
Key Entities
1. Users
- `id` (Primary Key)
- `name`
- `email`
- `password`
- `role` (e.g., guest, host)

2. Properties
- `id` (Primary Key)
- `user_id` (Foreign Key referencing Users)
- `title`
- `location`
- `price_per_night`

3. Bookings
- `id` (Primary Key)
- `user_id` (Foreign Key referencing Users)
- `property_id` (Foreign Key referencing Properties)
- `check_in_date`
- `check_out_date`

4. Reviews
- `id` (Primary Key)
- `user_id` (Foreign Key referencing Users)
- `property_id` (Foreign Key referencing Properties)
- `rating`
- `comment`

5. Payments
- `id` (Primary Key)
- `booking_id` (Foreign Key referencing Bookings)
- `amount`
- `payment_date`
- `status`

Entity Relationships

- A **User** can list multiple **Properties**.
- A **User** can make multiple **Bookings**.
- A **Booking** is associated with one **Property** and one **User**.
- A **Review** is given by a **User** for a specific **Property**.
- A **Payment** is linked to a specific **Booking**.

Feature Breakdown

1. User Management
Users can register, log in, and manage their profiles. The system supports role-based access control, distinguishing between guests and property hosts.

2. Property Management
Hosts can list properties with detailed information such as title, description, location, price, and images. They can also update or remove listings as needed.

3. Booking System
Guests can search for available properties, select dates, and make bookings. The system ensures no double-booking and tracks booking history for both users and hosts.

4. Review & Rating System
Guests can leave reviews and ratings for properties they’ve stayed in. This feedback helps other users make informed decisions and encourages quality service from hosts.

5. Payment Integration
Secure payment processing for bookings is handled within the app. It tracks payment status, ensures proper invoicing, and confirms successful transactions.

6. Admin Dashboard (Optional)
Admins can monitor user activities, manage content, and ensure compliance with platform policies. This feature adds an extra layer of control and transparency.

API Security

Security is a top priority in this project to protect sensitive user data, ensure trust, and maintain system integrity. The following key measures are implemented:

1. Authentication
The system uses token-based authentication (e.g., JWT) to verify the identity of users accessing the API. This ensures that only registered and logged-in users can perform certain actions, protecting user accounts from unauthorized access.

2. Authorization
Role-based access control is enforced to restrict access to specific endpoints. For example, only hosts can manage property listings, and only authenticated users can make bookings or post reviews.

3. Rate Limiting
Rate limiting is applied to prevent abuse of the API through excessive requests (e.g., brute force attacks). This ensures fair use of resources and improves application performance and reliability.

4. Input Validation & Sanitization
All user inputs are validated and sanitized to prevent injection attacks (e.g., SQL injection, XSS). This is crucial for maintaining data integrity and protecting the backend systems.

5. Secure Payment Handling
Payments are processed through trusted third-party services (e.g., Stripe or PayPal) with secure protocols. This protects financial data and ensures compliance with industry standards like PCI-DSS.
