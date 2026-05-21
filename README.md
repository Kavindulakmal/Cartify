# Cartify
<div align="center">

<img src="https://img.shields.io/badge/Spring%20Boot-3.x-6DB33F?style=for-the-badge&logo=springboot&logoColor=white"/>
<img src="https://img.shields.io/badge/Java-17+-ED8B00?style=for-the-badge&logo=openjdk&logoColor=white"/>
<img src="https://img.shields.io/badge/PostgreSQL-316192?style=for-the-badge&logo=postgresql&logoColor=white"/>
<img src="https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white"/>
<img src="https://img.shields.io/badge/AWS-FF9900?style=for-the-badge&logo=amazonaws&logoColor=white"/>

<br/><br/>

# 🛒 Spring Boot E-Commerce REST API

### A production-ready, industry-level backend built with Spring Boot — covering everything from fundamentals to cloud deployment.

<br/>

[![GitHub Stars](https://img.shields.io/github/stars/KAVINDU/ecommerce-api?style=social)](https://github.com/KAVINDU)
[![GitHub Forks](https://img.shields.io/github/forks/KAVINDU/ecommerce-api?style=social)](https://github.com/KAVINDU)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](CONTRIBUTING.md)

</div>

---

## 📌 Table of Contents

- [Overview](#-overview)
- [Tech Stack](#-tech-stack)
- [Features](#-features)
- [Project Structure](#-project-structure)
- [Getting Started](#-getting-started)
- [API Endpoints](#-api-endpoints)
- [Docker Setup](#-docker-setup)
- [AWS Deployment](#-aws-deployment)
- [Environment Variables](#-environment-variables)
- [Contributing](#-contributing)
- [Copyright](#-copyright)

---

## 🧭 Overview

This project is a **full-featured e-commerce REST API** built following **industry-level backend architecture** principles. It demonstrates real-world development practices including clean layered architecture, DTO patterns, relational database design, paginated filtering, image handling, reviews, orders, and end-to-end deployment with Docker and AWS.

> Built as a comprehensive reference project — every pattern here is production-ready and interview-worthy.

---

## 🛠 Tech Stack

| Layer | Technology |
|---|---|
| Language | Java 17+ |
| Framework | Spring Boot 3.x |
| Security | Spring Security + JWT |
| Database | PostgreSQL |
| ORM | Spring Data JPA / Hibernate |
| Validation | Jakarta Bean Validation |
| Image Storage | AWS S3 |
| Containerization | Docker & Docker Compose |
| Cloud Deployment | AWS EC2 + RDS |
| API Docs | Springdoc OpenAPI (Swagger UI) |
| Build Tool | Maven |

---

## ✨ Features

### 🔷 Spring Boot REST API Fundamentals
- RESTful endpoint design with proper HTTP methods and status codes
- Global exception handling with `@ControllerAdvice`
- Structured error responses
- Request/response logging

### 🔷 Entity & Relational Database Design
- Fully normalized relational schema
- JPA entity relationships: `@OneToMany`, `@ManyToOne`, `@ManyToMany`
- Cascade operations and fetch strategies
- Database migrations with Flyway

### 🔷 Pagination, Search & Filtering APIs
- Paginated responses using Spring's `Pageable`
- Dynamic search by keyword, category, price range
- Sorting by multiple fields
- Custom `Page<DTO>` response wrappers

### 🔷 DTO Pattern & Validation
- Strict separation between entity and API layer
- Request DTOs with `@Valid` annotations
- Response DTOs with `ModelMapper` / manual mapping
- Nested DTO structures for related entities

### 🔷 Product Reviews & Orders System
- Star-rating reviews per product per user
- Average rating aggregation
- Full order lifecycle: `PENDING → CONFIRMED → SHIPPED → DELIVERED`
- Order item management with inventory deduction

### 🔷 Image Handling in REST APIs
- Multipart file upload endpoints
- File type and size validation
- AWS S3 integration for cloud image storage
- Image URL generation and binding to product entities

### 🔷 Deployment using Docker & AWS
- Multi-stage `Dockerfile` for optimized image size
- `docker-compose.yml` for local development stack
- AWS EC2 instance deployment walkthrough
- AWS RDS PostgreSQL as production database
- Environment-based configuration profiles (`dev`, `prod`)

### 🔷 Industry-Level Project Structure
- Layered architecture: Controller → Service → Repository
- Interface-based service contracts
- Custom exceptions and centralized error handling
- Security with JWT authentication and role-based access control

---

## 📁 Project Structure

```
src/
└── main/
    ├── java/com/kavindu/ecommerce/
    │   ├── config/                  # Security, Swagger, AWS config
    │   ├── controller/              # REST controllers
    │   │   ├── AuthController.java
    │   │   ├── ProductController.java
    │   │   ├── OrderController.java
    │   │   ├── ReviewController.java
    │   │   └── ImageController.java
    │   ├── dto/                     # Request & Response DTOs
    │   │   ├── request/
    │   │   └── response/
    │   ├── entity/                  # JPA entities
    │   │   ├── User.java
    │   │   ├── Product.java
    │   │   ├── Order.java
    │   │   ├── OrderItem.java
    │   │   ├── Review.java
    │   │   └── Category.java
    │   ├── exception/               # Custom exceptions + global handler
    │   ├── repository/              # Spring Data JPA repositories
    │   ├── service/                 # Service interfaces + implementations
    │   │   ├── impl/
    │   │   └── S3ImageService.java
    │   ├── security/                # JWT filter, UserDetailsService
    │   └── util/                    # Mappers, helpers
    └── resources/
        ├── application.yml
        ├── application-dev.yml
        ├── application-prod.yml
        └── db/migration/            # Flyway SQL scripts
```

---

## 🚀 Getting Started

### Prerequisites

- Java 17+
- Maven 3.8+
- PostgreSQL 14+
- Docker (optional, for containerized setup)

### 1. Clone the Repository

```bash
git clone https://github.com/Kavindulakmal/Cartify.git
cd ecommerce-api
```

### 2. Configure the Database

Create a PostgreSQL database:

```sql
CREATE DATABASE ecommerce_db;
```

Update `src/main/resources/application-dev.yml`:

```yaml
spring:
  datasource:
    url: jdbc:postgresql://localhost:5432/ecommerce_db
    username: your_username
    password: your_password
```

### 3. Set Environment Variables

```bash
export JWT_SECRET=your_jwt_secret_here
export AWS_ACCESS_KEY=your_aws_access_key
export AWS_SECRET_KEY=your_aws_secret_key
export AWS_BUCKET_NAME=your_s3_bucket_name
```

### 4. Run the Application

```bash
mvn spring-boot:run -Dspring-boot.run.profiles=dev
```

The API will start at `http://localhost:8080`
Swagger UI available at `http://localhost:8080/swagger-ui.html`

---

## 📡 API Endpoints

### Authentication
| Method | Endpoint | Description |
|--------|----------|-------------|
| `POST` | `/api/v1/auth/register` | Register a new user |
| `POST` | `/api/v1/auth/login` | Login and receive JWT token |

### Products
| Method | Endpoint | Description |
|--------|----------|-------------|
| `GET` | `/api/v1/products` | Get all products (paginated, filterable) |
| `GET` | `/api/v1/products/{id}` | Get product by ID |
| `POST` | `/api/v1/products` | Create product (Admin) |
| `PUT` | `/api/v1/products/{id}` | Update product (Admin) |
| `DELETE` | `/api/v1/products/{id}` | Delete product (Admin) |
| `GET` | `/api/v1/products/search?q=&category=&minPrice=&maxPrice=` | Search & filter |

### Orders
| Method | Endpoint | Description |
|--------|----------|-------------|
| `POST` | `/api/v1/orders` | Place a new order |
| `GET` | `/api/v1/orders/my` | Get current user's orders |
| `GET` | `/api/v1/orders/{id}` | Get order details |
| `PATCH` | `/api/v1/orders/{id}/status` | Update order status (Admin) |

### Reviews
| Method | Endpoint | Description |
|--------|----------|-------------|
| `POST` | `/api/v1/products/{id}/reviews` | Add review to product |
| `GET` | `/api/v1/products/{id}/reviews` | Get product reviews |
| `DELETE` | `/api/v1/reviews/{id}` | Delete review |

### Images
| Method | Endpoint | Description |
|--------|----------|-------------|
| `POST` | `/api/v1/products/{id}/images` | Upload product image |
| `DELETE` | `/api/v1/products/{id}/images/{imageId}` | Delete product image |

---

## 🐳 Docker Setup

### Run with Docker Compose (Recommended for local dev)

```bash
docker-compose up --build
```

`docker-compose.yml` spins up:
- Spring Boot application on port `8080`
- PostgreSQL on port `5432`

### Build Docker Image Manually

```bash
docker build -t kavindu/ecommerce-api:latest .
docker run -p 8080:8080 --env-file .env kavindu/ecommerce-api:latest
```

---

## ☁️ AWS Deployment

### Architecture

```
Internet → EC2 (Spring Boot App) → RDS PostgreSQL
                ↕
           S3 Bucket (Images)
```

### Step-by-Step Deployment

**1. Launch EC2 Instance**
- AMI: Ubuntu 22.04 LTS
- Instance type: `t2.micro` (free tier) or higher
- Security group: allow ports `22`, `80`, `8080`

**2. Set up RDS**
- Engine: PostgreSQL 14
- Set DB name, master username/password
- Note the endpoint URL

**3. Configure S3 Bucket**
- Create bucket for image storage
- Set up IAM user with `AmazonS3FullAccess`
- Save Access Key & Secret Key

**4. Deploy on EC2**

```bash
# SSH into EC2
ssh -i your-key.pem ubuntu@your-ec2-ip

# Install Java
sudo apt update && sudo apt install -y openjdk-17-jdk

# Transfer JAR
scp -i your-key.pem target/ecommerce-api.jar ubuntu@your-ec2-ip:/home/ubuntu/

# Set environment variables
export SPRING_PROFILES_ACTIVE=prod
export DB_URL=jdbc:postgresql://<rds-endpoint>:5432/ecommerce_db
export DB_USERNAME=your_rds_username
export DB_PASSWORD=your_rds_password
export JWT_SECRET=your_secret
export AWS_ACCESS_KEY=your_key
export AWS_SECRET_KEY=your_secret
export AWS_BUCKET_NAME=your_bucket

# Run
java -jar ecommerce-api.jar
```

---

## 🔐 Environment Variables

| Variable | Description | Required |
|----------|-------------|----------|
| `DB_URL` | JDBC URL for PostgreSQL | ✅ |
| `DB_USERNAME` | Database username | ✅ |
| `DB_PASSWORD` | Database password | ✅ |
| `JWT_SECRET` | Secret key for JWT signing | ✅ |
| `JWT_EXPIRATION` | Token expiry in ms (default: 86400000) | ❌ |
| `AWS_ACCESS_KEY` | AWS IAM Access Key | ✅ |
| `AWS_SECRET_KEY` | AWS IAM Secret Key | ✅ |
| `AWS_BUCKET_NAME` | S3 bucket name for images | ✅ |
| `AWS_REGION` | AWS region (e.g., `us-east-1`) | ✅ |

---

## 🤝 Contributing

Pull requests are welcomed!

For major changes, please open an issue first to discuss what you would like to change.

1. Fork the repository
2. Create your feature branch: `git checkout -b feature/amazing-feature`
3. Commit your changes: `git commit -m 'Add some amazing feature'`
4. Push to the branch: `git push origin feature/amazing-feature`
5. Open a Pull Request

Thanks! 🙌

---

<div align="center">

**Happy Coding!!! 🚀**

<br/>

## Copyright

© **KAVINDU™** 2026 — All rights reserved.

<br/>

<img src="https://img.shields.io/badge/Made%20with-%E2%9D%A4%EF%B8%8F-red?style=for-the-badge"/>
<img src="https://img.shields.io/badge/Spring%20Boot-Powered-6DB33F?style=for-the-badge&logo=springboot"/>

</div>
