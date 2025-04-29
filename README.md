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
