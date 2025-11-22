# 🏡 Airbnb Clone — Backend System

## 📘 Overview
This project is a backend clone of **Airbnb**, designed to handle user authentication, property management, bookings, payments, reviews, notifications, and administrative functions.

It provides a scalable and secure RESTful API for frontend integration (web or mobile).

---

## 🧩 Core Features

### 👤 User Management
- Register as **Guest** or **Host**
- Secure login (JWT + OAuth)
- Role-based access control (RBAC)
- Profile updates (photo, bio, contact info)
- Password reset and email verification

### 🏠 Property Listings
- Hosts can create, edit, delete listings
- Add property details, photos, amenities, and rules
- Manage availability and seasonal pricing
- Upload property images (local or cloud storage)

### 🔍 Search & Filtering
- Search by location, price, date, and amenities
- Pagination and sorting (price, rating, popularity)
- Caching with Redis for frequently searched locations

### 📅 Booking Management
- Guests can book available properties
- Prevent double bookings using date validation
- Booking lifecycle: `pending → confirmed → completed → canceled`
- Host approval (optional)
- Cancellation and refund handling

### 💳 Payment System
- Integration with **Stripe** or **PayPal**
- Secure guest payments and host payouts
- Multiple currency support
- Webhooks for payment success/failure
- Refund and transaction management

### ⭐ Reviews & Ratings
- Guests leave ratings and reviews after confirmed stays
- Hosts can respond to reviews
- Prevent fake reviews (only linked to completed bookings)

###  Notifications
- Email & in-app notifications:
  - Booking confirmation or cancellation
  - Payment updates
  - Review responses
- Email service integration: **SendGrid** or **Mailgun**

###  Admin Dashboard
- Manage users, properties, and bookings
- Moderate listings and reviews
- View platform metrics and reports
- Handle refunds and disputes

---

##  Technical Stack

| Layer | Technology |
|-------|-------------|
| **Language** | Python / Node.js / TypeScript |
| **Framework** | FastAPI / Express.js / Django |
| **Database** | PostgreSQL / MySQL |
| **Authentication** | JWT (JSON Web Tokens) + OAuth |
| **Caching** | Redis |
| **File Storage** | Local / AWS S3 / Cloudinary |
| **Payments** | Stripe / PayPal |
| **Email** | SendGrid / Mailgun |
| **Testing** | pytest / Jest |
| **Logging** | Winston / Loguru |
| **Containerization** | Docker (optional) |

---

## 🗄️ Database Schema (ERD)

Below is the Entity-Relationship Diagram representing the core database structure:

![ERD](A_vector-based_Entity-Relationship_Diagram_(ERD)_i.png)

**Entities:**
- **Users**
- **Properties**
- **Bookings**
- **Payments**
- **Reviews**
- **Availability**
- **Notifications**

**Relationships:**
- A **User** can be a **Host** or **Guest**
- A **Host** owns multiple **Properties**
- A **Guest** can make multiple **Bookings**
- A **Booking** links a **Guest**, **Host**, and **Property**
- A **Booking** has one or more **Payments**
- A **Review** is tied to a **Booking**
- A **Property** has multiple **Availability** entries
- A **User** receives multiple **Notifications**

---

##  API Overview

| Endpoint | Method | Description |
|-----------|--------|-------------|
| `/api/auth/register` | POST | Register new user |
| `/api/auth/login` | POST | Login and receive JWT |
| `/api/properties` | POST | Create new property (Host only) |
| `/api/properties/:id` | PUT | Update property details |
| `/api/bookings` | POST | Create a new booking |
| `/api/bookings/:id/cancel` | POST | Cancel booking |
| `/api/payments/checkout` | POST | Initiate payment |
| `/api/reviews` | POST | Submit review |
| `/api/notifications` | GET | Retrieve notifications |
| `/api/admin/users` | GET | Admin list of users |

---

## 🧱 Authentication & Authorization

- **JWT Tokens** for secure sessions  
- **Role-based Access Control (RBAC)**:  
  - `guest`: browse, book, review  
  - `host`: create/edit listings, manage bookings  
  - `admin`: full control

---

##  Error Handling & Logging
- Centralized error middleware for API responses  
- Unified error format:
  ```json
  {
    "success": false,
    "error": "ValidationError",
    "message": "Email already exists"
  }
