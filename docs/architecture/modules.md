# Module Responsibilities

Each module has a clear definition of "What it owns". Adhering to these boundaries prevents spaghetti code.

## Sales Module (`backend/routers/sales.py`, `sales.py`)
- **Owns**: 
    - Creation and validation of Sales Orders.
    - Calculating totals (Amount, Liters) based on Rates.
    - Updating Stock/Inventory (implicitly via sales).
- **Does NOT Own**:
    - Processing Payments (Delegates to Payments module).
    - Customer Master Data (Delegates to Customers module).

## Payments Module (`backend/routers/payments.py`, `payments.py`)
- **Owns**:
    - Recording financial transactions.
    - Updating the `payment_status` of a Sale (e.g., flagging a Sale as "Paid" when balance is 0).
- **Coupling**: Strongly coupled to `Sales` but distinct.

## Demos Module (`backend/routers/demos.py`, `demos.py`)
- **Owns**:
    - Tracking non-revenue product usage (Marketing).
    - Follow-up scheduling.
    - Customer conversion tracking.

## Reports Module (`backend/routers/reports.py`, `reports.py`)
- **Owns**:
    - Aggregating data from Sales, Payments, and Demos.
    - Generating PDF/Excel artifacts.
!!! tip "Read-Only"
    Reports should strictly *read* data and never modify the state of Sales or Payments.

## Notification Module (`notifications.py`)
- **Owns**:
    - Alerting users to system events (e.g., "New Order Created").
    - **Extension Point**: If you need a new alert, add a trigger here, do not bury it deep in `sales.py`.
