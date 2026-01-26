# System Architecture Overview

The system is built as a **FastAPI** backend serving a frontend application.

## High-Level Boundaries

- **Frontend**: Handles user interaction, data presentation, and state management.
- **Backend (FastAPI)**:
    - **Routers**: Entry points for HTTP requests. Divided by functional domain (see [Modules](modules.md)).
    - **Models (Pydantic)**: Data validation and schema definitions.
    - **Database**: interacting with Supabase/PostgreSQL.
    - **Services**: Business logic (e.g., Report generation, Excel export).

## Directory Structure Strategy
(Refer to the current codebase for exact paths)

```
backend/
  routers/      # HTTP Entry points
  models.py     # Data Schemas (Single Source of Truth)
  reports.py    # Logic for heavy reporting tasks
  sales.py      # Core business logic for Sales
  payments.py   # Core logic for Payments
```

## Key Decisions

1. **Separation of Concerns**: We separate the *definition* of data (Models) from the *handling* of data (Routers/Services).
2. **Regional Flexibility**: The system explicitly handles multi-state pricing (Gujarat, MP, MH) as a first-class concept.
