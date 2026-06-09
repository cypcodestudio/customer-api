# Customer API

A full CRUD REST API for managing customer data, built with OpenAPI 3.0.

## Overview

The Customer API provides endpoints to create, read, update, and delete customer records. It supports pagination, search, and partial updates, making it suitable for CRM systems, onboarding flows, and customer management dashboards.

## Base URL

```
http://localhost:8080/api/v1
```

## Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| `GET` | `/customers` | List all customers (paginated, searchable) |
| `POST` | `/customers` | Create a new customer |
| `GET` | `/customers/{id}` | Get a customer by ID |
| `PUT` | `/customers/{id}` | Replace a customer (full update) |
| `PATCH` | `/customers/{id}` | Partially update a customer |
| `DELETE` | `/customers/{id}` | Delete a customer |

## Customer Model

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `id` | UUID | Auto | Unique identifier |
| `firstName` | string | Yes | Customer first name |
| `lastName` | string | Yes | Customer last name |
| `email` | string (email) | Yes | Unique email address |
| `phone` | string | No | Contact phone number |
| `dateOfBirth` | date | No | Date of birth (YYYY-MM-DD) |
| `address` | object | No | Street, city, province, postal code, country |
| `status` | enum | No | `ACTIVE`, `INACTIVE`, or `SUSPENDED` (default: `ACTIVE`) |
| `createdAt` | date-time | Auto | Record creation timestamp |
| `updatedAt` | date-time | Auto | Last update timestamp |

## Example Request

**Create a customer**

```http
POST /api/v1/customers
Content-Type: application/json

{
  "firstName": "Jane",
  "lastName": "Doe",
  "email": "jane.doe@example.com",
  "phone": "+27821234567",
  "dateOfBirth": "1990-05-15",
  "address": {
    "street": "123 Main Street",
    "city": "Cape Town",
    "province": "Western Cape",
    "postalCode": "8001",
    "country": "South Africa"
  },
  "status": "ACTIVE"
}
```

**Response `201 Created`**

```json
{
  "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "firstName": "Jane",
  "lastName": "Doe",
  "email": "jane.doe@example.com",
  "phone": "+27821234567",
  "dateOfBirth": "1990-05-15",
  "address": {
    "street": "123 Main Street",
    "city": "Cape Town",
    "province": "Western Cape",
    "postalCode": "8001",
    "country": "South Africa"
  },
  "status": "ACTIVE",
  "createdAt": "2026-06-09T10:00:00Z",
  "updatedAt": "2026-06-09T10:00:00Z"
}
```

## API Specification

The full OpenAPI 3.0 spec is available in [`customer-api.yaml`](customer-api.yaml).

- **SwaggerHub:** [cypcode-656/customer-api/1.0.0](https://app.swaggerhub.com/apis/cypcode-656/customer-api/1.0.0)

## Error Responses

| Status | Description |
|--------|-------------|
| `400 Bad Request` | Invalid or missing required fields |
| `404 Not Found` | Customer with given ID does not exist |
| `409 Conflict` | A customer with this email already exists |

## Getting Started

1. Clone the repo:
   ```bash
   git clone https://github.com/cypcodestudio/customer-api.git
   ```

2. Import `customer-api.yaml` into your preferred API tool (Postman, Insomnia, SwaggerHub).

3. Use the SwaggerHub link above to explore and test the API interactively.
