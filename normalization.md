# 🧠 Airbnb Database Normalization Report

## 🎯 Goal
Normalize the Airbnb database schema to **Third Normal Form (3NF)** to eliminate redundancy and ensure data integrity.

---

## 🔍 1. Initial Schema Overview

### Entity: **User**
- **Primary Key**: `user_id`
- **Attributes**: first_name, last_name, email, password_hash, phone_number, role, created_at
- ✅ All fields are atomic.
- ✅ All attributes depend directly and solely on the primary key.

**Conclusion**: Already in 3NF.  
**Action**: No changes required.

---

### Entity: **Property**
- **Primary Key**: `property_id`
- **Foreign Key**: `host_id` → User(user_id)
- **Attributes**: name, description, location, pricepernight, created_at, updated_at
- ✅ All fields are atomic.
- ✅ All attributes depend directly on `property_id`.

**Conclusion**: No normalization issues.  
**Action**: No changes required.

---

### Entity: **Booking**
- **Primary Key**: `booking_id`
- **Foreign Keys**: `property_id` → Property(property_id), `user_id` → User(user_id)
- **Attributes**: start_date, end_date, total_price, status, created_at

#### ⚠ Issue Identified:
- `total_price` is **derived** from `Property.pricepernight × number of nights`.
- This introduces **redundancy** and violates **3NF**, as it is dependent on another non-key attribute (`Property.pricepernight`).

#### 🛠 Normalization Step:
- **Remove `total_price`** from the `Booking` table.
- Calculate it dynamically using:
  ```sql
  DATEDIFF(end_date, start_date) * Property.pricepernight
