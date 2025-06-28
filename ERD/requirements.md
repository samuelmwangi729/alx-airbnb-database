# 📘 Airbnb Database Specification

## 🧱 Entities and Attributes

### 1. **User**
- **Primary Key**: `user_id` (UUID, Indexed)
- **Attributes**:
  - `first_name`: VARCHAR, NOT NULL  
  - `last_name`: VARCHAR, NOT NULL  
  - `email`: VARCHAR, UNIQUE, NOT NULL  
  - `password_hash`: VARCHAR, NOT NULL  
  - `phone_number`: VARCHAR, NULL  
  - `role`: ENUM (`guest`, `host`, `admin`), NOT NULL  
  - `created_at`: TIMESTAMP, DEFAULT CURRENT_TIMESTAMP  

---

### 2. **Property**
- **Primary Key**: `property_id` (UUID, Indexed)
- **Attributes**:
  - `host_id`: Foreign Key → `User(user_id)`  
  - `name`: VARCHAR, NOT NULL  
  - `description`: TEXT, NOT NULL  
  - `location`: VARCHAR, NOT NULL  
  - `pricepernight`: DECIMAL, NOT NULL  
  - `created_at`: TIMESTAMP, DEFAULT CURRENT_TIMESTAMP  
  - `updated_at`: TIMESTAMP, ON UPDATE CURRENT_TIMESTAMP  

---

### 3. **Booking**
- **Primary Key**: `booking_id` (UUID, Indexed)
- **Attributes**:
  - `property_id`: Foreign Key → `Property(property_id)`  
  - `user_id`: Foreign Key → `User(user_id)`  
  - `start_date`: DATE, NOT NULL  
  - `end_date`: DATE, NOT NULL  
  - `total_price`: DECIMAL, NOT NULL  
  - `status`: ENUM (`pending`, `confirmed`, `canceled`), NOT NULL  
  - `created_at`: TIMESTAMP, DEFAULT CURRENT_TIMESTAMP  

---

### 4. **Payment**
- **Primary Key**: `payment_id` (UUID, Indexed)
- **Attributes**:
  - `booking_id`: Foreign Key → `Booking(booking_id)`  
  - `amount`: DECIMAL, NOT NULL  
  - `payment_date`: TIMESTAMP, DEFAULT CURRENT_TIMESTAMP  
  - `payment_method`: ENUM (`credit_card`, `paypal`, `stripe`), NOT NULL  

---

### 5. **Review**
- **Primary Key**: `review_id` (UUID, Indexed)
- **Attributes**:
  - `property_id`: Foreign Key → `Property(property_id)`  
  - `user_id`: Foreign Key → `User(user_id)`  
  - `rating`: INTEGER (CHECK rating >= 1 AND <= 5), NOT NULL  
  - `comment`: TEXT, NOT NULL  
  - `created_at`: TIMESTAMP, DEFAULT CURRENT_TIMESTAMP  

---

### 6. **Message**
- **Primary Key**: `message_id` (UUID, Indexed)
- **Attributes**:
  - `sender_id`: Foreign Key → `User(user_id)`  
  - `recipient_id`: Foreign Key → `User(user_id)`  
  - `message_body`: TEXT, NOT NULL  
  - `sent_at`: TIMESTAMP, DEFAULT CURRENT_TIMESTAMP  

---

## 🔗 Entity Relationships

| From Entity  | To Entity   | Relationship Description                  | Cardinality                        |
|--------------|-------------|--------------------------------------------|------------------------------------|
| User         | Property    | A host **owns** properties                 | 1 (host) → many (properties)       |
| User         | Booking     | A guest **makes** bookings                 | 1 (guest) → many (bookings)        |
| User         | Review      | A guest **writes** reviews                 | 1 (guest) → many (reviews)         |
| User         | Message     | A user **sends/receives** messages         | 1 ↔ many (messages)                |
| Property     | Booking     | A property **has** bookings                | 1 → many                           |
| Property     | Review      | A property **receives** reviews            | 1 → many                           |
| Booking      | Payment     | A booking **has** one payment              | 1 → 1 (or possibly 1 → 0..1)       |
| Booking      | Property    | A booking is **for** a property            | many → 1                           |
| Booking      | User        | A booking is **made by** a user            | many → 1                           |
| Message      | User        | Messages **connect** two users             | many → 1 (sender), 1 (recipient)   |

---

## ✅ Constraints and Indexes

### Constraints
- **User**
  - Unique constraint on `email`
  - Non-null constraints on required fields
- **Property**
  - Foreign key constraint on `host_id`
  - Non-null constraints on essential attributes
- **Booking**
  - Foreign key constraints on `property_id` and `user_id`
  - `status` must be one of `pending`, `confirmed`, `canceled`
- **Payment**
  - Foreign key constraint on `booking_id`
- **Review**
  - `rating` must be between 1 and 5
  - Foreign key constraints on `property_id` and `user_id`
- **Message**
  - Foreign key constraints on `sender_id` and `recipient_id`

### Indexes
- All **primary keys** are indexed automatically
- Additional indexes:
  - `User.email`
  - `Property.property_id`, `Booking.property_id`
  - `Booking.booking_id`, `Payment.booking_id`
