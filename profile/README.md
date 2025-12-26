# FitRang

**FitRang** is a fashion-tech platform and **shopping companion** built using a **microservice architecture**, designed to help users make better clothing choices while shopping online.

Users create their **profile and style dossier** in the FitRang web app, and the **FitRang Chrome Extension** uses this data—along with live product details—to query AI and determine **style suitability** for the user (or for someone they’re shopping for).

Each directory in this workspace represents an **independent service or client application with its own repository**, deployed and scaled separately.

---

## What FitRang Does (High Level)

1. User creates a **Profile & Style Dossier** in the FitRang app
2. User shops online (Amazon, Myntra, Ajio, etc.)
3. FitRang **Chrome Extension**:

   * Extracts product details from the page
   * Fetches the user’s style dossier
   * Queries AI for suitability, fit, and style advice
4. User gets **real-time recommendations** while shopping

---

## Architecture Overview

* **Frontend:** React (Web Apps)
* **Browser Client:** Chrome Extension
* **API Layer:** GraphQL (Federation)
* **Backend:** Go, Node.js, Python
* **Authentication:** Firebase Authentication
* **Async Messaging:** Kafka, RabbitMQ
* **Real-time:** WebSockets, gRPC
* **Caching / PubSub:** Redis
* **Infrastructure:** Docker, Kubernetes, Prometheus

---

## Client Applications

### FitRang Web App (User App)

Primary user-facing application.

* Profile creation
* Style dossier management
* Preferences & personalization
* Account management

🔗 Repository:
[https://github.com/FitRang/fitrang-web](https://github.com/FitRang/fitrang-web)

---

### FitRang Main

Repository to kick-start the project, just clone this and run:
```bash
docker compose buid --no-cache
docker compose up
```
🔗 Repository:
[https://github.com/FitRang/fitrang-main](https://github.com/FitRang/fitrang-main)

---

### FitRang Chrome Extension

The core shopping companion experience.

* Runs on shopping websites
* Extracts product details from the page
* Fetches user style dossier
* Queries AI for suitability & recommendations
* Displays results in-context while shopping

🔗 Repository:
[https://github.com/FitRang/fitrang-chrome-extension](https://github.com/FitRang/fitrang-chrome-extension)

---

## Backend Services & Repositories

### Profile Service

Manages user **Profiles** and **Style Dossiers** using **GraphQL** (primary) and **gRPC** (internal).

🔗 Repository:
[https://github.com/FitRang/profile-service](https://github.com/FitRang/profile-service)

---

### Analysis Service

Handles analytical processing and AI-related insights.

🔗 Repository:
[https://github.com/FitRang/analysis_service](https://github.com/FitRang/analysis_service)

---

### Notification Service

Handles notification persistence and business logic.

🔗 Repository:
[https://github.com/FitRang/notification-service](https://github.com/FitRang/notification-service)

---

### Delivery Service

Delivers notifications in **real-time**.

* Maintains WebSocket connections
* Subscribes to Redis Pub/Sub
* Pushes events to connected clients

🔗 Repository:
[https://github.com/FitRang/delivery-service](https://github.com/FitRang/delivery-service)

---

### Fanout Consumer

Kafka → Redis bridge.

* Listens to Kafka topics
* Publishes messages to Redis Pub/Sub channels

🔗 Repository:
[https://github.com/FitRang/fanout-consumer](https://github.com/FitRang/fanout-consumer)

---

### Indexing Worker

Indexes data for search and retrieval.

🔗 Repository:
[https://github.com/FitRang/indexing-worker](https://github.com/FitRang/indexing-worker)

---

## API & Federation

### Federation

GraphQL Federation layer composing all subgraphs into a single supergraph.

🔗 Repository:
[https://github.com/FitRang/federation](https://github.com/FitRang/federation)

---

## Infrastructure & DevOps

### Infrastructure

Shared infrastructure definitions and deployment tooling.

🔗 Repository:
[https://github.com/FitRang/infrastructure](https://github.com/FitRang/infrastructure)

---

### Load Tests

Performance and stress testing utilities.

🔗 Repository:
[https://github.com/FitRang/load-tests](https://github.com/FitRang/load-tests)

---

## Event & Recommendation Flow

1. User updates profile or dossier via Web App
2. Profile Service stores data
3. Chrome Extension:

   * Detects shopping context
   * Extracts product metadata
   * Fetches dossier data
4. AI is queried for:

   * Fit suitability
   * Style compatibility
   * Occasion relevance
5. Recommendations are shown instantly to the user

---

## Authentication Model

* Authentication handled by **Firebase Authentication**
* All clients use Firebase ID tokens
* Backend services trust verified tokens
* Username and email act as stable identifiers

---

## Development Philosophy

* Independent deployability
* API-first design
* Event-driven architecture
* Real-time user feedback
* Clear separation of concerns

---
