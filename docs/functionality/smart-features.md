# Intelligent Features

The PC Sales Platform includes "smart" features designed to automate manual tasks and identify sales opportunities.

## 1. Automated Calling Lists (`/automation/calling-list`)

This feature analyzes customer purchase history to generate a prioritized list of people to call.

### How it works
The system categorizes customers into three buckets based on urgency and value:

1.  **Inactive High-Value Customers**
    *   **Trigger**: Customer has not purchased in >30 days (configurable).
    *   **Priority Rule**:
        *   `High`: Lifetime Value > ₹10,000
        *   `Medium`: Lifetime Value > ₹5,000
    *   **Goal**: Retention.

2.  **Demo Follow-ups**
    *   **Trigger**: A Demo was given, and the `follow_up_date` is today or in the next 7 days.
    *   **Priority**: Always `High`.
    *   **Goal**: Conversion.

3.  **Outstanding Payments**
    *   **Trigger**: Customer has an outstanding balance > 0.
    *   **Priority**: `High` if > ₹5,000.
    *   **Goal**: Collection.

---

## 2. Demo Auto-Conversion

When a **Sale** is created, the system automatically checks if this sale relates to a pending **Demo**.

### The Logic
1.  **Trigger**: User submits a new Sale form.
2.  **Scan**: System looks for `Demo` records for this `customer_id` with status `Scheduled` or `Follow-up`.
3.  **Match**: It checks if the `product_id` in the Sale matches the `product_id` in the Demo.
4.  **Action**:
    *   Updates Demo status to `Converted`.
    *   Adds a note: *"Auto-converted: Sale {invoice_no} created on {date}"*.

**Benefit**: Field staff don't need to go back and manually close Demos after making a sale.

---

## 3. Intelligent Form Generation

### Invoice Numbering
*   **Format**: `INV-XXXXX`
*   **Logic**: Incremental. Finds the last invoice (e.g., `INV-00050`) and generates `INV-00051`.
*   **Fallback**: If DB read fails, uses Unix Timestamp to prevent collision.

### Sale Code (Seasonality Tracking)
*   **Format**: `MMyy####` (e.g., `01260001` for the first sale of Jan 2026).
*   **Purpose**: Allows quick visual identification of when a sale happened just by its ID.
