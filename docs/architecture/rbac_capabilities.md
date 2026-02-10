# RBAC Capability Discovery - Parul Chemicals Sales System

This document outlines the granular capabilities identified within the Parul Chemicals Sales System (`pc_sales`). It maps user-facing actions to their corresponding backend API endpoints, serving as a foundation for Role-Based Access Control (RBAC) implementation.

## Authentication & Core
| Capability ID | Module | UI Location / Entry Point | Action Type | Description | Backend API Endpoint / Side Effect |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `auth:login` | Auth | Login Page | EXECUTE | User login and session creation | Supabase Auth (Client-side) |

## Dashboard
| Capability ID | Module | UI Location / Entry Point | Action Type | Description | Backend API Endpoint / Side Effect |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `dashboard:view_metrics` | Dashboard | Dashboard (Metric Cards) | VIEW | View Key Performance Indicators (Sales, Payments, Customers) | `GET /api/dashboard/metrics` |
| `dashboard:view_sales_trend` | Dashboard | Dashboard (Trend Chart) | VIEW | View sales performance trends over time | `GET /api/dashboard/sales-trend` |
| `dashboard:view_recent_sales` | Dashboard | Dashboard (Recent Activity) | VIEW | View list of most recent sales transactions | `GET /api/dashboard/recent-sales` |
| `dashboard:view_upcoming_demos` | Dashboard | Dashboard (Upcoming Demos) | VIEW | View list of scheduled product demonstrations | `GET /api/dashboard/upcoming-demos` |

## Customer Management
| Capability ID | Module | UI Location / Entry Point | Action Type | Description | Backend API Endpoint / Side Effect |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `customers:list` | Customers | Customers Page (Table) | VIEW | List all customers with pagination/search | `GET /api/customers/` |
| `customers:details` | Customers | Customers Page (Row Click) | VIEW | View detailed customer profile | `GET /api/customers/{id}` |
| `customers:create` | Customers | Customers Page ("Add Customer" Button) | CREATE | Create a new customer record | `POST /api/customers/` |
| `customers:update` | Customers | Customers Page (Edit Dialog) | UPDATE | Update existing customer details | `PUT /api/customers/{id}` |
| `customers:delete` | Customers | Customers Page (Delete Icon) | DELETE | Soft delete/Deactivate a customer | `DELETE /api/customers/{id}` |
| `customers:view_activities` | Customers | Customer Details (Activity Tab) | VIEW | View timeline of customer interactions | `GET /api/customers/{id}/activities` |

## Sales & Order Management
| Capability ID | Module | UI Location / Entry Point | Action Type | Description | Backend API Endpoint / Side Effect |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `sales:list` | Sales | Sales Page / Order Management | VIEW | List all sales/orders with status filters | `GET /api/sales/` |
| `sales:details` | Sales | Sales Page (Eye Icon) | VIEW | View full order details including line items | `GET /api/sales/{id}` |
| `sales:create` | Sales | Sales Page ("New Sale" Button) | CREATE | Create a new sale order | `POST /api/sales/` |
| `sales:update` | Sales | Order Management (Status Chip/Edit) | UPDATE | Update order status or details | `PUT /api/sales/{id}` |
| `sales:delete` | Sales | Sales Page (Delete Icon) | DELETE | remove a sale record | `DELETE /api/sales/{id}` |
| `sales:generate_invoice` | Sales | Sales Page (Print/Invoice Icon) | VIEW | Generate and view Invoice PDF | `GET /api/sales/{id}/invoice` |

## Payments
| Capability ID | Module | UI Location / Entry Point | Action Type | Description | Backend API Endpoint / Side Effect |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `payments:list` | Payments | Payments Page (Table) | VIEW | List all payment records | `GET /api/payments/` |
| `payments:create` | Payments | Payments Page ("Record Payment") | CREATE | Record a new payment against a customer/sale | `POST /api/payments/` |
| `payments:delete` | Payments | Payments Page (Delete Icon) | DELETE | Delete a payment record | `DELETE /api/payments/{id}` |
| `payments:view_stats` | Payments | Payments Page (Summary Cards) | VIEW | View payment efficiency statistics | `GET /api/payments/stats` |

## Demos & Pre-sales
| Capability ID | Module | UI Location / Entry Point | Action Type | Description | Backend API Endpoint / Side Effect |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `demos:list` | Demos | Demos Page (Table) | VIEW | List all product demonstrations | `GET /api/demos/` |
| `demos:details` | Demos | Demos Page (Row Click) | VIEW | View single demo details | `GET /api/demos/{id}` |
| `demos:create` | Demos | Demos Page ("Schedule Demo") | CREATE | Schedule a new product demo | `POST /api/demos/` |
| `demos:update` | Demos | Demos Page (Edit) | UPDATE | Update demo time or details | `PUT /api/demos/{id}` |
| `demos:update_status` | Demos | Demos Page (Status Chip) | UPDATE | Update demo status (e.g., Scheduled -> Converted) | `PUT /api/demos/{id}/status` |
| `demos:delete` | Demos | Demos Page (Delete Icon) | DELETE | Cancel/Delete a demo | `DELETE /api/demos/{id}` |

## Products & Inventory
| Capability ID | Module | UI Location / Entry Point | Action Type | Description | Backend API Endpoint / Side Effect |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `products:list` | Products | Product Pricing Page | VIEW | View full product catalog | `GET /api/products/` |
| `products:create` | Products | Product Pricing Page ("Add" Button) | CREATE | Add a new product to catalog | `POST /api/products/` |
| `products:update_price` | Products | Product Pricing Page (Edit) | UPDATE | Update individual product price/details | `PUT /api/admin/update-product-price/{id}` |
| `products:bulk_update` | Products | Product Pricing Page ("Save All") | UPDATE | Bulk update multiple product prices | `POST /api/admin/update-product-prices-bulk` |

## Distributors
| Capability ID | Module | UI Location / Entry Point | Action Type | Description | Backend API Endpoint / Side Effect |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `distributors:list` | Distributors | Distributors Page (Table) | VIEW | List all distributors | `GET /api/distributors/` |
| `distributors:create` | Distributors | Distributors Page ("Add" Button) | CREATE | Register a new distributor | `POST /api/distributors/` |
| `distributors:update` | Distributors | Distributors Page (Edit) | UPDATE | Update distributor profile | `PUT /api/distributors/{id}` |
| `distributors:delete` | Distributors | Distributors Page (Delete) | DELETE | Remove a distributor | `DELETE /api/distributors/{id}` |

## Reports & Analytics
| Capability ID | Module | UI Location / Entry Point | Action Type | Description | Backend API Endpoint / Side Effect |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `reports:generate` | Reports | Reports Page | VIEW | Generate Sales/Payment reports (PDF/Excel) | `POST /api/reports/generate` (e.g., payments/sales) |
| `reports:view_trends` | Reports | Reports Page (Charts) | VIEW | View analytical charts and trends | `GET /api/dashboard/sales-trend` (Shared with Dashboard) |

## Automation (CRM)
| Capability ID | Module | UI Location / Entry Point | Action Type | Description | Backend API Endpoint / Side Effect |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `automation:my_assignments` | CRM / Calling | Calling List Page | VIEW | View assigned daily calling tasks | `GET /api/automation/my-assignments` |
| `automation:distribute` | CRM / Calling | Calling List Page (Admin Button) | EXECUTE | Trigger daily call distribution algorithms | `POST /api/automation/run-distribution` |
| `automation:view_master` | CRM / Calling | (Admin View - API) | VIEW | View unassigned master calling list | `GET /api/automation/calling-list` |

## Notifications
| Capability ID | Module | UI Location / Entry Point | Action Type | Description | Backend API Endpoint / Side Effect |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `notifications:list` | Notifications | Notifications Page | VIEW | View user notifications | `GET /api/notifications/` |
| `notifications:count` | Notifications | App Header (Badge) | VIEW | Get unread notification count | `GET /api/notifications/unread-count` |
| `notifications:mark_read` | Notifications | Notifications Page | UPDATE | Mark notification as read | `PUT /api/notifications/{id}/mark-read` |
| `notifications:mark_all` | Notifications | Notifications Page | UPDATE | Mark all notifications as read | `PUT /api/notifications/mark-all-read` |
| `notifications:delete` | Notifications | Notifications Page | DELETE | Delete a notification | `DELETE /api/notifications/{id}` |

## Data Import
| Capability ID | Module | UI Location / Entry Point | Action Type | Description | Backend API Endpoint / Side Effect |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `import:excel` | Import | Data Import Page | CREATE | Bulk import data from Excel | `POST /api/imports/excel` |

## System Admin
| Capability ID | Module | UI Location / Entry Point | Action Type | Description | Backend API Endpoint / Side Effect |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `admin:view_logs` | Admin | Admin Page | VIEW | View system audit/activity logs | `GET /api/admin/activity-logs` |
| `admin:create_user` | Admin | Admin Page | CREATE | Create and provision new system users | `POST /api/admin/users` |
