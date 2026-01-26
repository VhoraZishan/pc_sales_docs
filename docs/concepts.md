# Product Concepts

**Last Updated:** January 26, 2026

These are the core business entities that drive the system. Understanding these is prerequisite to understanding the code.

---

## Core Entities

### 1. Sale
A **Sale** represents a transaction with a [Customer](#3-customer).

!!! info "Key Responsibility"
    Tracks the exchange of goods (Liters/Products) for efficiency and revenue.

*   **Dependencies**: A Sale requires a `Customer` and `Products`.
*   **Status Lifecycle**:
    ```mermaid
    stateDiagram-v2
        [*] --> Pending
        Pending --> Confirmed: Admin Approves
        Confirmed --> Shipped: Logistics
        Shipped --> Delivered: Customer Receives
        Delivered --> [*]
    ```

### 2. Demo
A **Demo** is a pre-sales activity where product is provided for trial.

*   **Purpose**: To convert a potential customer (or distributor member) into a buyer.
*   **Key Metrics**: `conversion_status`
*   **Workflow**:
    1.  Provide Product
    2.  Schedule Follow-up
    3.  Record Outcome (`Converted` / `Lost`)

### 3. Customer
The end-buyer or entity receiving the product.

*   **Identity**: Tracked by `customer_code`.
*   **Location**: Critical for logistics (`Village`, `Taluka`, `District`).
*   **Segments**: Can be individual farmers or part of a Distributor network.

### 4. Distributor
An organizational entity (e.g., a cooperative or local group).

*   **Role**: Aggregates multiple end-users (`sabhasad_count`).
*   **Key Contact**: `mantri_name`.

### 5. Payment
A financial record linked to a **Sale**.

!!! warning "Constraint"
    A Sale can have **multiple** partial payments. Never assume `One Sale = One Payment`.

---

## Regional Logic

Pricing is not global. It is regional. The system must decide which rate to apply based on the customer's location.

| Rate Type | Applicable Region | Validation |
| :--- | :--- | :--- |
| **Gujarat Rate** | Gujarat State | Default |
| **Maharashtra Rate** | Maharashtra | Manual Override possible |
| **MP Rate** | Madhya Pradesh | Manual Override possible |

!!! warning "Implementation Detail"
    Code handling rate selection exists in the `products` or `sales` module logic. **Do not hardcode these values in the frontend.**
