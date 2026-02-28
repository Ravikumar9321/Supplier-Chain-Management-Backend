# Supplier Chain Management Backend System

Complete Spring Boot REST API managing **Suppliers → Products → Orders → Customers**.

## 🛠️ Tech Stack
- **Java 8+** (Streams, Lambdas, Collections)
- **Spring Boot** & **Spring MVC**
- **Hibernate/JPA** ORM
- **PostgreSQL** Database
- **Maven** Build Tool
- **Postman** API Testing

## ✨ Features
- Full CRUD for **Supplier**, **Product**, **Order**, **Customer** entities
- **Complex relationships**: One-to-Many, Many-to-Many with join tables
- RESTful APIs with proper HTTP status codes & JSON handling
- `@CreationTimestamp` for order tracking
- Unique constraints on contact, email, trackingNumber

## 🗄️ Database Schema & Relationships

**Entities & Key Fields:**

**Supplier:**
- id (PK)
- name, contact (unique), email (unique)
- Companyname
- products (One-to-Many)

**Product:**
- id (PK)
- name, price, stockQuantity
- supplier (Many-to-One)
- orders (Many-to-Many via order_products table)

**Customer:**
- id (PK)
- name, contact (unique), email (unique), address
- orders (One-to-Many)

**Order:**
- id (PK)
- orderDate (`@CreationTimestamp`), totalAmount, status
- trackingNumber (unique)
- customer (Many-to-One)
- products (Many-to-Many via order_products)

## 🚀 Quick Start

### Prerequisites
```bash
JDK 8+ | Maven | PostgreSQL
1. Database Setup
CREATE DATABASE supplier_chain_db;
2. Configure application.properties
spring.datasource.url=jdbc:postgresql://localhost:5432/supplier_chain_db
spring.datasource.username=postgres
spring.datasource.password=your_password
spring.jpa.hibernate.ddl-auto=update
3. Run Application
Right-click on project → Run As → java application
API available at: http://localhost:8080
📋 API Endpoints
| Method | Endpoint                     | Description                         |
| ------ | ---------------------------- | ----------------------------------- |
| POST   | /api/suppliers               | Create supplier w/ company details  |
| GET    | /api/suppliers/{id}/products | Get supplier products               |
| POST   | /api/products                | Add product w/ stock & supplier     |
| GET    | /api/products/stock/{min}    | Products with stock ≥ min quantity  |
| POST   | /api/customers               | Create customer                     |
| POST   | /api/orders                  | Create order w/ customer & products |
| GET    | /api/orders/{trackingNumber} | Track order by tracking number      |

🧪 Testing
100% CRUD coverage via Postman collections
Tested relationships & @JsonIgnore serialization
Validated unique constraints (contact, email, trackingNumber)
📁 Project Structure
src/main/java/com/supplyManagement/Entity/
├── Customer.java      (name, contact, email, address, orders)
├── Orders.java        (orderDate, totalAmount, status, trackingNumber)
├── Product.java       (name, price, stockQuantity, supplier)
└── Supplier.java      (name, contact, email, Companyname, products)
🔮 Future Enhancements
JWT Authentication (Admin/Customer roles)
Order status workflow
React frontend integration
