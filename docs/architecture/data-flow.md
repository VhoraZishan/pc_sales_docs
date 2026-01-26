# Data Flow Concepts

Understanding how data moves through the system helps in debugging and extending features.

## The Sales Lifecycle

1. **Initiation**: 
   - A generic "Order" is created via `Sales Module`.
   - **Impact**: `Sales` table entry created. Status: `Pending`.

2. **Fulfillment (Dispatch)**:
   - User updates Shipment Status.
   - **Impact**: Tracking number added. Delivery date estimated.

3. **Financial Settlement**:
   - Multiple `Payment` records can be added to the Sale.
   - **Trigger**: When `sum(payments) >= sale.total`, the Sale `payment_status` updates to `Paid`.

## The Demo-to-Sale Flow

1. **Demo Created**: Product given to `Customer`.
2. **Follow-up**: System prompts for follow-up on `follow_up_date`.
3. **Conversion**:
   - If User buys -> specific flow to create a `Sale`.
   - **Impact**: `Demo` marked as `Converted`.

## Reporting Flow
- **Source**: Reads from `Sales`, `Payments`, `Customers`.
- **Processing**: `reports.py` aggregates totals (e.g., "Total Liters Sold in Taluka X").
- **Output**: PDF/Excel download.
