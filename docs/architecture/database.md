# Database Schema & Architecture

The database is hosted on **Supabase** (PostgreSQL). Below is the schema representation and key relationships derived from the production database.

## Entity Relationship Diagram

```mermaid
erDiagram
    Sales ||--|{ SaleItems : contains
    Sales ||--|{ Payments : has
    Customers ||--|{ Sales : places
    Customers ||--|{ Demos : requests
    Products ||--|{ SaleItems : "is sold as"
    Products ||--|{ Demos : "is sampled in"
    Distributors ||--|{ Demos : "participates in"

    Sales {
        int sale_id PK
        string invoice_no
        int customer_id FK
        float total_amount
        string payment_status
        string order_status
        string shipment_status
    }

    SaleItems {
        int sale_item_id PK
        int sale_id FK
        int product_id FK
        int quantity
        float rate
        float amount
    }

    Products {
        int product_id PK
        string product_name
        float rate_gujarat
        float rate_maharashtra
        float rate_mp
        string capacity_ltr
    }

    Customers {
        int customer_id PK
        string name
        string mobile
        string village
        string district
    }

    Payments {
        int payment_id PK
        int sale_id FK
        float amount
        string payment_method
    }

    Demos {
        int demo_id PK
        int customer_id FK
        int product_id FK
        string conversion_status
    }
```

## Table Responsibilities

### Core Transactional Data
- **`sales`**: The central table for all revenue-generating transactions.
- **`sale_items`**: Granular line items for each sale. Links products to sales at a specific historical rate.
- **`payments`**: Ledger of all incoming money. One sale can have multiple partial payments.

### Master Data
- **`customers`**: The end-users (Farmers/Buyers).
- **`products`**: Catalog of items with **region-specific pricing columns** (`rate_gujarat`, `rate_mp`, `rate_maharashtra`).
- **`distributors`**: Groups or cooperatives that manage multiple customers.

### Operational Data
- **`demos`**: Pre-sales marketing activity. Tracks where free samples went and if they converted.
- **`activity_logs`**: Audit trail of who did what (security & debugging).
- **`notifications`**: System alerts for users.
