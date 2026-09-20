<div align="center">

# कलाकृति · KALAKRITI

### **Production Handicraft Commerce & Provenance Platform**

**Multi-Vendor Commerce · GI-Aware Cataloguing · Cryptographic Provenance · QR Verification · RBAC · Async APIs · SSR · PostgreSQL · Production Cloud**

<br />

[![Live Application](https://img.shields.io/badge/Live-Production-success?style=for-the-badge)](https://kalakriti-frontend.vercel.app)
[![API](https://img.shields.io/badge/API-FastAPI-009688?style=for-the-badge)](https://kalakritiproductionreadyproject-complete-production.up.railway.app/docs)
[![Frontend](https://img.shields.io/badge/Frontend-Next.js-black?style=for-the-badge)](https://kalakriti-frontend.vercel.app)
[![Database](https://img.shields.io/badge/Database-PostgreSQL-336791?style=for-the-badge)](https://www.postgresql.org/)

<br />

**[Live Platform](https://kalakriti-frontend.vercel.app) · [GI Craft Catalogue](https://kalakriti-frontend.vercel.app/shop) · [API Documentation](https://kalakritiproductionreadyproject-complete-production.up.railway.app/docs)**

</div>

---

## System Definition

**Kalakriti** is a production-oriented digital commerce platform for India's traditional handicraft ecosystem.

The system combines **multi-vendor marketplace infrastructure**, **role-based access control**, **GI-aware craft classification**, **SHA-256 certificate generation**, **QR-based provenance verification**, and a **craft restoration workflow** within a single full-stack architecture.

The engineering objective is not simply to digitize product listings.

It is to establish a verifiable digital layer between:

```text
ARTISAN
   │
   │  Craft + Origin + Provenance
   ▼
KALAKRITI
   │
   ├── Identity & Access
   ├── Product Catalogue
   ├── Provenance Engine
   ├── Commerce Layer
   ├── Price Distribution
   └── Restoration Workflow
   │
   ▼
CUSTOMER
   │
   ├── Discover
   ├── Purchase
   ├── Verify
   └── Preserve
```

---

# Architecture at a Glance

```text
                         ┌──────────────────────────┐
                         │        CUSTOMER          │
                         │        ARTISAN           │
                         │         ADMIN            │
                         └────────────┬─────────────┘
                                      │
                                      ▼
                    ┌─────────────────────────────────┐
                    │         NEXT.JS APPLICATION     │
                    │                                 │
                    │  App Router · SSR · TypeScript │
                    │  Tailwind CSS · Auth State      │
                    └────────────────┬────────────────┘
                                     │
                                HTTPS / REST
                                     │
                                     ▼
                    ┌─────────────────────────────────┐
                    │           FASTAPI CORE           │
                    │                                 │
                    │  REST API · Pydantic · JWT      │
                    │  RBAC · Business Logic · DI     │
                    └────────────────┬────────────────┘
                                     │
              ┌──────────────────────┼──────────────────────┐
              │                      │                      │
              ▼                      ▼                      ▼
     ┌────────────────┐    ┌──────────────────┐    ┌────────────────┐
     │   PostgreSQL   │    │ Provenance Engine│    │  Craft Doctor  │
     │                │    │                  │    │                │
     │ SQLAlchemy 2.0 │    │ SHA-256          │    │ Damage         │
     │ asyncpg        │    │ Certificates     │    │ Assessment     │
     │                │    │ QR Verification  │    │ Restoration    │
     └────────────────┘    └──────────────────┘    └────────────────┘
```

---

# Engineering Stack

| Layer                 | Technology                 | Responsibility                |
| --------------------- | -------------------------- | ----------------------------- |
| **Presentation**      | Next.js, React, TypeScript | Application UI and routing    |
| **Rendering**         | App Router, SSR            | Server-side data rendering    |
| **Styling**           | Tailwind CSS               | UI system                     |
| **API**               | FastAPI                    | RESTful application layer     |
| **Validation**        | Pydantic v2                | Request / response schemas    |
| **Runtime**           | Python 3.11, Uvicorn       | ASGI application runtime      |
| **Persistence**       | PostgreSQL                 | Relational data store         |
| **ORM**               | SQLAlchemy 2.0 Async       | Database abstraction          |
| **Driver**            | asyncpg                    | Async PostgreSQL connectivity |
| **Authentication**    | JWT                        | Stateless authentication      |
| **Password Security** | Argon2                     | Credential hashing            |
| **Authorization**     | RBAC                       | Role-level access control     |
| **Provenance**        | SHA-256                    | Certificate integrity         |
| **Verification**      | QR Codes                   | Customer-facing verification  |
| **Containerization**  | Docker                     | Backend packaging             |
| **Frontend Cloud**    | Vercel                     | Production frontend           |
| **Backend Cloud**     | Railway                    | API + database infrastructure |

---

# Core Domain Architecture

## `Marketplace`

The commerce layer provides the foundation for the artisan/customer relationship.

### Primary capabilities

* Multi-vendor product catalogue
* Product publishing lifecycle
* Artisan-managed listings
* Product metadata
* Customer discovery
* Product pricing
* Role-aware operations

The marketplace is intentionally structured around **artisans as first-class entities**, rather than treating them as anonymous inventory suppliers.

---

## `ProvenanceEngine`

The provenance subsystem creates a deterministic digital representation of product authenticity metadata.

```text
Craft Metadata
      │
      ▼
Canonical Certificate Payload
      │
      ▼
SHA-256 Digest
      │
      ▼
Certificate Record
      │
      ▼
QR Encoding
      │
      ▼
Verification Endpoint
```

### Current craft domains

* Madhubani Painting
* Jaipur Blue Pottery
* Bastar Dhokra Bell Metal

The cryptographic layer provides **integrity verification of certificate data**.

It should not be interpreted as an independent proof that a physical product is authentic; that depends on the quality and verification of the underlying source information.

---

# GI-Aware Craft Catalogue

Kalakriti includes a dedicated catalogue layer for geographically associated Indian craft traditions.

The architecture separates:

```text
CRAFT
  │
  ├── Category
  ├── Region
  ├── Artisan
  ├── Product
  └── Provenance Certificate
```

This allows the catalogue to evolve beyond a conventional e-commerce taxonomy toward a system that retains **craft, geographical, artisan, and provenance relationships**.

---

# Authenticity Verification Pipeline

A customer-facing product can expose a QR verification path:

```text
┌──────────────┐
│ Physical     │
│ Product      │
└──────┬───────┘
       │
       │ QR
       ▼
┌──────────────┐
│ Verification │
│ Endpoint     │
└──────┬───────┘
       │
       ▼
┌──────────────┐
│ Certificate  │
│ Lookup       │
└──────┬───────┘
       │
       ▼
┌──────────────┐
│ SHA-256      │
│ Integrity    │
│ Verification │
└──────┬───────┘
       │
       ▼
┌──────────────┐
│ Certificate  │
│ Information  │
└──────────────┘
```

---

# Artisan Economics

## `85% Artisan Share`

Kalakriti's configured pricing model allocates **85% of the listed product value to the artisan**.

The platform is designed to make this distribution explicit rather than hiding the economics behind a single checkout amount.

```text
                    PRODUCT VALUE
                         │
             ┌───────────┴───────────┐
             │                       │
             ▼                       ▼
       ┌───────────┐           ┌──────────────┐
       │  ARTISAN  │           │  PLATFORM    │
       │    85%    │           │    REMAINDER │
       └───────────┘           └──────────────┘
```

---

# Craft Doctor

## `Post-Purchase Preservation Layer`

Craft Doctor extends the platform beyond transaction completion.

Instead of:

```text
Browse → Buy → Done
```

Kalakriti introduces:

```text
Browse
   ↓
Purchase
   ↓
Use
   ↓
Damage
   ↓
Assessment
   ↓
Restoration
   ↓
Preservation
```

### Restoration lifecycle

1. Customer submits a restoration request.
2. Damage information is evaluated.
3. A qualified artisan/specialist can review the case.
4. Restoration work is initiated.
5. Completion is recorded.

The intent is to create a **lifecycle model for traditional craft**, rather than treating the marketplace as a one-time transaction system.

---

# Identity & Access Architecture

Kalakriti uses **JWT-based authentication with role-based authorization**.

```text
                    AUTHENTICATION
                          │
                          ▼
                     JWT TOKEN
                          │
                          ▼
                    ROLE RESOLUTION
                          │
          ┌───────────────┼────────────────┐
          │               │                │
          ▼               ▼                ▼
       ADMIN           ARTISAN          CUSTOMER
          │               │                │
          ▼               ▼                ▼
     Platform        Craft / Product    Marketplace
     Operations        Operations        Operations
```

### Roles

| Role              | Scope                                     |
| ----------------- | ----------------------------------------- |
| `ADMIN`           | Platform-level operations                 |
| `MASTER_ARTISAN`  | Craft, product and restoration operations |
| `CUSTOMER_PATRON` | Discovery, purchasing and verification    |

### Security Controls

* JWT Bearer authentication
* Argon2 password hashing
* Role-based authorization
* Pydantic schema validation
* API-level access control
* Environment-based configuration

---

# API Layer

The backend is implemented as an asynchronous FastAPI service.

```text
HTTP Request
     │
     ▼
FastAPI Router
     │
     ▼
Authentication / Authorization
     │
     ▼
Pydantic Validation
     │
     ▼
Service Layer
     │
     ▼
SQLAlchemy Async
     │
     ▼
PostgreSQL
```

FastAPI also exposes the OpenAPI schema and interactive documentation through its standard documentation stack.

### Production API

**Base:**
`https://kalakritiproductionreadyproject-complete-production.up.railway.app`

**Swagger UI:**
`/docs`

**Health Probe:**
`/health`

---

# Frontend Architecture

The frontend uses the **Next.js App Router** with server-side rendering and TypeScript.

```text
App Router
    │
    ├── Route Segments
    │
    ├── Server Components
    │
    ├── Client Components
    │
    ├── Data Fetching
    │
    └── UI Components
```

The App Router is designed around modern React capabilities including Server Components and supports production-oriented rendering and data-fetching patterns.

---

# Production Infrastructure

```text
                         GitHub
                           │
              ┌────────────┴────────────┐
              │                         │
              ▼                         ▼
          Vercel                     Railway
              │                         │
              ▼                         ├──────────────┐
        Next.js App                    │              │
                                       ▼              ▼
                                    FastAPI       PostgreSQL
                                       │
                                       ▼
                                  OpenAPI / REST
```

### Frontend

```yaml
platform: Vercel
framework: Next.js
root_directory: frontend/
production_branch: main
```

### Backend

```yaml
platform: Railway
runtime: Python 3.11
server: Uvicorn
containerization: Docker
database: PostgreSQL
driver: asyncpg
production_branch: main
```

The frontend deployment follows the conventional Git-based Next.js deployment model, where repository changes can move through preview deployments before production.

---

# Production Endpoints

| Resource              | Endpoint                                                                          |
| --------------------- | --------------------------------------------------------------------------------- |
| **Web Application**   | https://kalakriti-frontend.vercel.app                                             |
| **GI Catalogue**      | https://kalakriti-frontend.vercel.app/shop                                        |
| **REST API**          | https://kalakritiproductionreadyproject-complete-production.up.railway.app        |
| **Swagger / OpenAPI** | https://kalakritiproductionreadyproject-complete-production.up.railway.app/docs   |
| **Health Probe**      | https://kalakritiproductionreadyproject-complete-production.up.railway.app/health |

---

# Deployment Reliability

## Repository Synchronization Incident — 01 September 2026

During production validation, the frontend returned:

```text
No published crafts found yet
```

while the backend was returning published products with:

```text
HTTP 200 OK
```

### Failure Mode

The frontend deployment was connected to:

```text
prabhat8420/kalakriti
```

while active development and backend deployment were connected to:

```text
prabhat8420/KalakritiProductionReadyProject-complete
```

This produced a **source-of-truth divergence** between frontend and backend deployments.

### Resolution

The production pipeline was re-aligned:

```text
GitHub
   │
   └── main
        │
        ├──► Vercel
        │     └── frontend/
        │
        └──► Railway
              ├── FastAPI
              └── PostgreSQL
```

The environment was then revalidated across:

**Frontend → API → Authentication → Database → Provenance → Product Rendering**

### Engineering Lesson

> **Deployment correctness is not only about whether a build succeeds; it is about whether every production service is executing the intended revision from the intended source of truth.**

---

# Repository Topology

```text
KalakritiProductionReadyProject-complete/
│
├── frontend/
│   ├── app/
│   ├── components/
│   ├── lib/
│   ├── public/
│   └── ...
│
├── backend/
│   ├── app/
│   ├── models/
│   ├── schemas/
│   ├── services/
│   └── ...
│
├── Dockerfile
├── docker-compose.yml
├── README.md
└── ...
```

---

# Engineering Characteristics

### `Asynchronous I/O`

FastAPI + SQLAlchemy Async + `asyncpg` provide an asynchronous request/database path.

### `Stateless Authentication`

JWT-based authentication keeps API authentication independent of server-side session state.

### `Schema-Driven API`

Pydantic models provide explicit request and response contracts, while FastAPI exposes the resulting OpenAPI specification.

### `Cryptographic Integrity`

SHA-256 is used as a deterministic integrity mechanism for provenance certificate data.

### `Role Isolation`

RBAC separates platform, artisan, and customer capabilities.

### `Independent Deployment`

Frontend and backend are independently deployable while sharing a canonical Git source.

### `Production Observability`

A dedicated health endpoint provides a lightweight mechanism for deployment/runtime verification.

---

# Roadmap

```text
[ ] Expanded GI craft catalogue
[ ] Advanced artisan verification
[ ] Provenance history & certificate versioning
[ ] Artisan analytics
[ ] Order lifecycle tracking
[ ] Multilingual interface
[ ] Craft preservation knowledge base
[ ] Expanded restoration network
[ ] Automated authenticity review
```

---

# Project Ownership

<div align="center">

### **Kalakriti**

**Designed, engineered and maintained by**

**Harsh Bhadoriya · Prabhat Jha · Aviral Bajpai · Piyush Kr. Sahu**

© 2026 Kalakriti Project Team. All rights reserved.

</div>

The source code, architecture, documentation, original designs, and project assets are owned by the above authors unless otherwise stated.

Unauthorized reproduction, redistribution, or commercial reuse is prohibited without prior permission from the project authors.

---

<div align="center">

## **KALAKRITI**

### *Digital infrastructure for living craft traditions.*

**Commerce · Provenance · Verification · Preservation**

</div>
