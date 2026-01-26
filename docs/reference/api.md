# API Reference

This reference documents the core endpoints available in the **Parul Chemicals Sales API**.

**Base URL**: `http://localhost:8000` (Local) or Production URL.

!!! info "Authentication"
    Most endpoints require the `x-user-email` header for activity logging and notifications.

## Sales Module (`/sales`)

| Method | Endpoint | Description |
| :--- | :--- | :--- |
| `GET` | `/` | Get all sales with enriched customer details. |
| `POST` | `/` | Create a new sale. **Triggers**: Auto-conversion of Demos, Notification, Activity Log. |
| `GET` | `/pending-payments` | Get sales with outstanding balances. Includes payment term logic. |
| `GET` | `/{sale_id}` | Get a single sale ID and its line items. |
| `PUT` | `/{sale_id}` | Update mutable sale fields. |
| `DELETE` | `/{sale_id}` | Delete a sale and its associated items. |
| `GET` | `/{sale_id}/invoice-pdf` | Stream a PDF invoice for the given sale. |

## Payments Module (`/payments`)

| Method | Endpoint | Description |
| :--- | :--- | :--- |
| `GET` | `/` | Get paginated list of all payments. |
| `POST` | `/` | Record a new payment. **Triggers**: Updates Sale `payment_status` (Pending/Partial/Paid). |
| `GET` | `/pending` | list of sales sorted by highest pending amount desc. |
| `GET` | `/{payment_id}` | Get single payment details. |
| `PUT` | `/{payment_id}` | Update a payment. **Triggers**: Recalculates Sale `payment_status`. |
| `DELETE` | `/{payment_id}` | Delete a payment. **Triggers**: Recalculates Sale `payment_status`. |

## Demos Module (`/demos`)

| Method | Endpoint | Description |
| :--- | :--- | :--- |
| `GET` | `/` | Get all demos (filterable by `status`). |
| `POST` | `/` | Schedule a new demo. **Triggers**: Notification. |
| `GET` | `/{demo_id}` | Get demo details with Customer/Product info. |
| `PUT` | `/{demo_id}` | Update demo details. |
| `PUT` | `/{demo_id}/status` | specific endpoint to update `conversion_status`. |
| `DELETE` | `/{demo_id}` | Delete a demo record. |

## Reports Module (`/reports`)

The reports module aggregates data for dashboards and exports.

| Method | Endpoint | Description |
| :--- | :--- | :--- |
| `GET` | `/sales-trend` | Sales aggregation by `daily`, `weekly`, or `monthly`. |
| `GET` | `/payment-trend` | Payment aggregation by `daily`, `weekly`, or `monthly`. |
| `GET` | `/sales-order-summary-pdf` | Generate PDF summary of sales within a date range. |
| `GET` | `/sales-summary` | Overall KPI summary (Total Sales, Total Revenue, Total Liters). |
