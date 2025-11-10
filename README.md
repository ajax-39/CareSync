# 🏥 **CareSync**

## **Description**
**CareSync** is a cloud-native microservices-based healthcare management system designed to streamline patient, billing, and analytics workflows. The platform integrates modular services for patient management, billing automation, analytics tracking, authentication, and API routing — all built with **Spring Boot**, **Docker**, **AWS ECS**, **Kafka**, and **gRPC**.  

Each service is independently deployable and communicates securely through standardized protocols, providing a scalable and resilient healthcare ecosystem.

## 📑 **Table of Contents**


  - [🧱 System Architecture](#-system-architecture)
  - [✨ Features Implemented](#-features-implemented)
    - [🧩 Architecture & Services](#-architecture--services)
    - [⚙️ Inter-Service Communication](#️-inter-service-communication)
    - [☁️ Cloud & Deployment](#️-cloud--deployment)
    - [🔐 Security & API Management](#-security--api-management)
  - [🧰 Technologies / Libraries Used](#-technologies--libraries-used)
  - [🧪 Local Setup](#-local-setup)
    - [🧩 Prerequisites](#-prerequisites)
    - [⚙️ Steps to Run Locally](#️-steps-to-run-locally)


---

## **System Architecture**

CareSync follows a **5-service microservices architecture**:

<table>
  <tr>
    <td align="center" width="50%">
      <img src="https://github.com/user-attachments/assets/dcab3f84-9d91-4a39-9fa4-cdf17ed88864" alt="CareSync Architecture Screenshot 1" width="450"/>
    </td>
    <td align="center" width="50%">
      <img src="https://github.com/user-attachments/assets/5a1201b4-1ac0-471f-a7e1-5de93f8f5391" alt="CareSync Architecture Screenshot 2" width="450"/>
    </td>
  </tr>
</table>

Each service uses its own **PostgreSQL** instance and communicates via **gRPC** and **Kafka**.

---

## **Features Implemented**

### 🧩 **Architecture & Services**
- **5 Modular Microservices:** `Patient`, `Billing`, `Analytics`, `Auth`, and `Gateway`.
- **Independent PostgreSQL Databases:** Ensuring full data isolation per service.
- **Centralized Authentication:** Secure token-based login using **JWT** with **Spring Security**.
- **Gateway-Level Authorization:** Policy-based route filtering with **Spring Cloud Gateway**.

### ⚙️ **Inter-Service Communication**
- **gRPC Integration:**  
  Used for synchronous, low-latency communication between `Patient` and `Billing` services.  
  ⏱ Improved latency by **40%** over traditional REST.
- **Kafka Integration:**  
  Enabled asynchronous, event-driven communication between `Patient` → `Analytics`.  
  Ensured fault-tolerant, scalable message streaming.

### ☁️ **Cloud & Deployment**
- **Containerization:** All microservices packaged with **Docker**.
- **Infrastructure as Code:** Managed AWS ECS, VPCs, MSK, and RDS using **CloudFormation**.
- **AWS ECS Deployment:** Deployed containerized services via **LocalStack** and ECS,  
  cutting setup time by **95%**.
- **Load Balancing:** Configured **Application Load Balancer (ALB)** for traffic routing.

### 🔐 **Security & API Management**
- Centralized JWT validation via **API Gateway**.
- Role-based access and custom Spring Security filters.
- End-to-end encryption for service-to-service communication.

---

## **Technologies / Libraries Used**

| **Category** | **Tools & Technologies** |
|---------------|--------------------------|
| **Backend Framework** | Spring Boot, Spring Cloud, Spring Security |
| **Database** | PostgreSQL |
| **Messaging Queue** | Apache Kafka |
| **Inter-Service Communication** | gRPC, Protocol Buffers (.proto) |
| **Containerization** | Docker |
| **Cloud Infrastructure** | AWS ECS, CloudFormation, LocalStack |
| **Authentication** | JWT (JSON Web Token) |
| **Build Tools** | Maven |
| **Testing** | JUnit, Mockito, Integration Tests |

---

## **Local Setup**

### 🧪 **Prerequisites**
- Docker  
- Docker Compose or LocalStack (for AWS emulation)  
- PostgreSQL  
- JDK 17+  
- Maven  
- Kafka Broker (Local or Cloud)  

---

### ⚙️ **Steps to Run Locally**

1. **Clone the Repository**
   ```bash
   git clone https://github.com/ajax-39/CareSync.git
   cd CareSync
   ```

2. **Configure Environment Variables**
   Create a `.env` file in the root:
   ```env
   DB_URL=jdbc:postgresql://localhost:5432/caresync_patient
   DB_USER=postgres
   DB_PASS=password
   JWT_SECRET=<your-secret>
   KAFKA_BROKER=localhost:9092
   ```

3. **Run Kafka & Databases via Docker Compose**
   ```bash
   docker-compose up -d
   ```

4. **Build and Run Each Service**
   ```bash
   cd patient-service
   mvn spring-boot:run
   # Repeat for billing, analytics, auth, and gateway
   ```

5. **Access the Services**
   | Service | Default Port |
   |----------|---------------|
   | API Gateway | 8080 |
   | Patient Service | 8081 |
   | Billing Service | 8082 |
   | Analytics Service | 8083 |
   | Auth Service | 8084 |

---


