# Airbnb Clone – Backend Feature Requirements

## Overview

This document specifies the **technical and functional requirements** for the core backend features of the Airbnb Clone application.  
It provides API endpoints, input/output specifications, validation rules, and performance criteria for each feature.

---

## 1. User Authentication

**Purpose:** Enable secure registration, login, and access control for users (guests and hosts).

### **API Endpoints**

- `POST /api/users/register` – Register a new user
- `POST /api/users/login` – Authenticate an existing user
- `GET /api/users/profile` – Retrieve logged-in user profile
- `PUT /api/users/profile` – Update user profile

### **Input / Output Specifications**

#### Registration (`POST /api/users/register`)

- **Input**

```json
{
  "name": "John Doe",
  "email": "john@example.com",
  "password": "Password123!",
  "role": "guest"
}
