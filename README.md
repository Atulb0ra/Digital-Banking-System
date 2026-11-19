# Banking System – Microservices Architecture

A distributed banking platform built using **Java, Spring Boot, Spring Cloud, Apache Kafka, MySQL, Redis, and Razorpay**.

The system supports account management, money transfers, OTP verification, fraud detection, refunds, payment order creation, webhook processing, and notifications.

---

## 1. System Architecture

```text
Client / Swagger
        |
        v
   API Gateway :8080
        |
        +-------------------+-------------------+
        |                   |                   |
        v                   v                   v
Account Service      Transaction          Payment
:8081                Service :8082        Service :8083
        |                   |                   |
        |                   v                   v
        |               Redis OTP          Razorpay
        |                   |                   |
        +---------------- Kafka ----------------+
                            |
              +-------------+-------------+
              |                           |
              v                           v
      Fraud Detection               Notification
        Service :8084                 Service :8085

Communication
•
REST: Client → API Gateway → Microservices
•
OpenFeign: Transaction/Fraud services → Account Service
•
Kafka: Fraud, OTP, refund, transaction, and payment events
•
Redis: OTP storage and expiration
•
MySQL: Persistent account, transaction, and payment records
•
Razorpay: External payment gateway
