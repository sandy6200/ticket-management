# Complaint / Ticket Management System

A Ruby on Rails based web application that enables customers to raise complaints, track ticket status, upload supporting files, and communicate with administrators through a comment system.

## 📌 Project Overview

The Complaint / Ticket Management System is designed to streamline complaint handling and support ticket management. It provides separate interfaces for Customers and Admins, ensuring efficient communication and ticket resolution.

## 🎯 Objectives

* Create support tickets
* Track complaint progress
* Upload screenshots and supporting files
* Communicate through comments
* Search and manage tickets efficiently

---

## 🚀 Features

### Authentication

* User Registration
* User Login
* User Logout
* Role-Based Access Control

### Ticket Management

* Create Tickets
* View Tickets
* Edit Tickets
* Delete Tickets
* Automatic Ticket Number Generation

### Comment System

* Customer Comments
* Admin Comments
* Comment History

### File Upload

* Multiple Image Upload
* Active Storage Integration

### Dashboard

#### Customer Dashboard

* Total Tickets
* Open Tickets
* Closed Tickets
* In Progress Tickets

#### Admin Dashboard

* Total Tickets
* Open Tickets
* Closed Tickets
* High Priority Tickets

### Search Functionality

Search tickets by:

* Title
* Status
* Priority
* Ticket Number

---

## 🛠 Technologies Used

### Backend

* Ruby
* Ruby on Rails 8

### Database

* SQLite3

### Frontend

* HTML
* CSS
* Bootstrap 5
* ERB Templates

### Authentication

* Devise Gem

### File Storage

* Active Storage

### Version Control

* Git
* GitHub

---

## 👥 User Roles

### Customer

* Register/Login
* Create Tickets
* Edit Own Tickets
* View Own Tickets
* Add Comments
* Upload Images

### Admin

* View All Tickets
* Update Ticket Status
* Update Ticket Priority
* Add Comments
* Monitor Dashboard

---

## 🗄 Database Schema

### Customer

```ruby
has_many :tickets
has_many :comments
```

Attributes:

* id
* email
* encrypted_password
* role

### Ticket

```ruby
belongs_to :customer
has_many :comments, dependent: :destroy
has_many_attached :images
```

Attributes:

* ticket_number
* title
* description
* status
* priority
* customer_id

### Comment

```ruby
belongs_to :customer
belongs_to :ticket
```

Attributes:

* content
* customer_id
* ticket_id

## ✅ Validations

### Ticket

```ruby
validates :title, presence: true
validates :description, presence: true,
          length: { minimum: 10 }
validates :status, presence: true
validates :priority, presence: true
```

### Comment

```ruby
validates :content, presence: true
```

### Customer

Handled automatically by Devise:

* Email Validation
* Password Validation

---

## 🔄 Callbacks

### Automatic Ticket Number Generation

```ruby
before_create :generate_ticket_number

def generate_ticket_number
  self.ticket_number = "TKT-#{SecureRandom.hex(4).upcase}"
end
```

### Ticket Closure Logging

```ruby
after_update :log_closed_ticket
```

Logs a message whenever a ticket status changes to **Closed**.

---

## 🔍 Search Implementation

Case-insensitive ticket searching using:

```ruby
ILIKE
```

Filters:

* Title
* Status
* Priority
* Ticket Number

---

## ⚡ Challenges & Solutions

### 1. Role-Based Authentication

**Problem:**
Different dashboards were required for Admin and Customer.

**Solution:**

```ruby
current_customer.admin?
```

Used role-based authorization and conditional rendering.

### 2. Ticket Number Generation

**Problem:**
Each ticket needed a unique identifier.

**Solution:**

```ruby
before_create
SecureRandom.hex
```

Generated unique ticket numbers automatically.

### 3. Search Functionality

**Problem:**
Users needed quick ticket lookup.

**Solution:**
Implemented dynamic search using `ILIKE` queries.

### 4. Comment System

**Problem:**
Communication was needed between Admins and Customers.

**Solution:**
Created a Comment model associated with both Ticket and Customer.

---

## 📚 Learning Outcomes

Through this project, I learned:

* MVC Architecture
* Ruby on Rails Development
* Devise Authentication
* Active Storage
* Rails Associations
* Model Validations
* Callbacks
* Bootstrap Integration
* Search Functionality
* Role-Based Authorization
* Database Design
* CRUD Operations

---

## 🏃 Installation

### Clone Repository

```bash
git clone https://github.com/your-username/complaint-ticket-management-system.git
cd complaint-ticket-management-system
```

### Install Dependencies

```bash
bundle install
```

### Setup Database

```bash
rails db:create
rails db:migrate
```

### Start Server

```bash
rails server
```

Visit:

```text
http://localhost:3000
```

---

## 📷 Screenshots

Add screenshots of:

* Login Page
* Registration Page
* Customer Dashboard
* Admin Dashboard
* Ticket Creation Form
* Ticket Details Page
* Comment Section

---

## 📄 License

This project is developed for educational and learning purposes.

---

## 👨‍💻 Author

**Sandeep Kumar Yadav**

Software Engineering Student | Ruby on Rails Developer
