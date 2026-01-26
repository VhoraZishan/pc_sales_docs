# Adding New Reports

This guide explains how to add a new customized report to the system.

## Overview
Reports in this system are generated on the fly. They generally involve:
1.  **Router**: An endpoint to accept parameters (dates, filters).
2.  **Logic**: Aggregating data from Supabase.
3.  **Output**: Returning JSON (for charts) or Streaming PDF (for downloads).

## Step-by-Step Implementation

### 1. Define the Data Requirement
Decide what you need. Example: "Top Selling Products per District".

### 2. Implementation (`backend/routers/reports.py`)

Create a new endpoint. Use `Depends(get_db)` to access the database.

```python
@router.get("/top-products")
def get_top_products(
    district: Optional[str] = None,
    db: SupabaseClient = Depends(get_db)
):
    try:
        # Build Query
        query = db.table("sale_items").select("*, sales(customers(district))")
        
        # Execute
        data = query.execute()
        
        # Process in Python (pandas or native list comprehensions)
        # ... logic here ...
        
        return {"result": processed_data}
    except Exception as e:
        raise HTTPException(status_code=500, detail=str(e))
```

### 3. Adding PDF Generation (`backend/reports.py`)

If you need a PDF output, extend the `ReportGenerator` class.

**File**: `backend/reports.py`

```python
class ReportGenerator:
    # ... existing code ...
    
    def generate_product_report_pdf(self, data):
        # Create buffer
        buffer = io.BytesIO()
        doc = SimpleDocTemplate(buffer, pagesize=A4)
        
        # Add Tables/Text
        # ... reportlab logic ...
        
        doc.build(elements)
        return buffer.getvalue()
```

### 4. Wire it up
Update the router to call your new generator method and return a `StreamingResponse`.

```python
from fastapi.responses import StreamingResponse

@router.get("/top-products-pdf")
def get_top_products_pdf(db: SupabaseClient = Depends(get_db)):
    # ... fetch data ...
    pdf_bytes = report_generator.generate_product_report_pdf(data)
    
    return StreamingResponse(
        io.BytesIO(pdf_bytes),
        media_type="application/pdf"
    )
```

## Best Practices
1.  **Read-Only**: Ensure your report queries never modify data.
2.  **Date Filters**: Always confirm `start_date` and `end_date` formats to avoid database errors.
3.  **Performance**: For large datasets, use Supabase `.limit()` or perform aggregation in SQL logic (RPC calls) if possible, rather than Python loops.
