# Microservices Backend System (Spring Boot + Kafka)


A production-style backend system inspired by BookMyShow, built using **Java Spring Boot microservices**, **Kafka-based asynchronous communication**, and **cloud-native infrastructure patterns**.

This project demonstrates how real-world distributed backend platforms are designed with scalability, fault isolation, and service ownership.


## Key Highlights

- Microservices architecture using Spring Boot
- Service discovery with Netflix Eureka
- API Gateway with authentication + validation
- Kafka-based event-driven messaging
- Dockerized local environment with Kafka support
- Clean separation of services (booking, payments, notifications)


## System Architecture

```
             Client
               |
               v
         +-------------+
         | API Gateway |
         +-------------+
               |
               v
   +--------------------------+
   | Service Registry (Eureka)|
   +--------------------------+
               |
  +-----------+-------------+-----------+
  |           |             |           |
  v           v             v           v
+---------+ +---------+ +--------------+
| Booking | | Payment | | Notification |
| Service | | Service | | Service      |
+---------+ +---------+ +--------------+
      \         |            /
       \        |           /
        v       v          v
   +----------------------------------+
   | Kafka Event Bus (Async Messaging)|
   +----------------------------------+

```


## Services Included

| Service | Description |
| --- | --- |
| **api-gateway** | Entry point for all requests, includes Basic Auth + request validation |
| **eureka-service-registry** | Service discovery and registration layer |
| **booking-service** | Handles ticket booking workflow and seat allocation |
| **payment-service** | Manages payment processing events |
| **notification-service** | Sends email notifications asynchronously |
| **kafka-infra** | Kafka + Zookeeper setup for local messaging infrastructure |


## Kafka Event Flow

Kafka is used to decouple services asynchronously:

- Booking emits events → Payment processes
- Payment emits success/failure → Notification triggers email
- Enables resilience and scalable event-driven backend design


## Tech Stack

- Java 17
- Spring Boot
- Spring Cloud Gateway
- Netflix Eureka
- Apache Kafka
- Docker + Docker Compose
- REST APIs
- Microservices Design Patterns


## Running the Project Locally

### Prerequisites

- Java 17+
- Maven
- Docker + Docker Compose


### Step 1 - Start Kafka Infrastructure

```bash
docker-compose up -d

```

This will start:

- Kafka Broker
- Zookeeper



### Step 2 - Start Eureka Registry

```bash
cd eureka-service-registry
mvn spring-boot:run

```

Access Eureka Dashboard:

```
http://localhost:8761

```


### Step 3 - Start API Gateway

```bash
cd api-gateway
mvn spring-boot:run

```

Gateway runs on:

```
http://localhost:8080

```


### Step 4 - Start Other Services

Run each in separate terminals:

```bash
cd booking-service
mvn spring-boot:run

```

```bash
cd payment-service
mvn spring-boot:run

```

```bash
cd notification-service
mvn spring-boot:run

```


## Features Implemented

- API Gateway with Basic Authentication
- Parameter validation at entry layer
- Kafka-driven async backend communication
- Email notification service
- Dockerized setup for complete local testing


## Future Improvements

Planned upgrades for production readiness:

- Distributed tracing (OpenTelemetry)
- Centralized logging (ELK)
- Retry + Dead-letter queues in Kafka
- Schema registry + event versioning
- Kubernetes deployment support


## Author

**Manasa Bhagwat**

Backend Engineer (Java + Spring Boot + AWS)
- GitHub: [https://github.com/manasa-bhagwat](https://github.com/manasa-bhagwat)
- LinkedIn: [https://www.linkedin.com/in/manasabhagwat](https://www.linkedin.com/in/manasabhagwat)
