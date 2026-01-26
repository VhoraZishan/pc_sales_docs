# Extending the System

## "Where do I add...?"

### A New Report?
1. **Frontend**: Add the UI trigger in the Reports page.
2. **Backend Router**: Add an endpoint in `backend/routers/reports.py`.
3. **Business Logic**: Implement the aggregation logic in `backend/reports.py`.
   - *Do not put heavy calculation logic in the router.*

### A New Product Category?
- This is a data entry task, not a code change. Use the `Products` management UI.
- However, if the category implies **new pricing logic** (e.g., "Export Rate"), modify `backend/models.py` to add the field and `backend/sales.py` to handle the calculation.

### A New Notification Trigger?
- Go to `backend/notifications.py`.
- Define the new event type.
- Call the notification service from the relevant source module (e.g., from `sales.py` when a high-value order is placed).

## Creating New API Endpoints
1. Create the router function in the appropriate `routers/` file.
2. Define the Request/Response models in `models.py` (keep it shared).
3. Ensure the router is included in `main.py` if it's a new file.
